FROM opensuse/tumbleweed

ENV LANG=C
# libqt5-qtbase-devel skipped
RUN zypper --non-interactive install --no-recommends shadow sudo git patterns-devel-base-devel_basis gcc-c++ readline-devel libbz2-devel liblz4-devel bluez-devel python3-devel libopenssl-devel cross-arm-none-gcc14 cross-arm-none-newlib-devel gd-devel

#RUN zypper addrepo https://download.opensuse.org/repositories/home:wkazubski/openSUSE_Tumbleweed/home:wkazubski.repo && \
#    zypper --gpg-auto-import-keys refresh && \
#    zypper --non-interactive install cross-arm-none-eabi-gcc12 cross-arm-none-eabi-newlib

RUN zypper --non-interactive install cmake python311 python311-pip python311-virtualenv

RUN zypper --non-interactive install ocl-icd-devel

# Create rrg user
RUN useradd -ms /bin/bash rrg
RUN passwd -d rrg
ARG UART_GID
# dialout group may already exist on another numeric ID than on host
RUN if [ -n "${UART_GID}" ]; then \
    groupadd -g ${UART_GID} mydialout || true; \
    usermod -aG ${UART_GID} rrg; \
  fi
RUN printf 'rrg ALL=(ALL) NOPASSWD: ALL\n' | tee -a /etc/sudoers

USER rrg
WORKDIR "/home/rrg"

CMD ["/bin/bash"]
