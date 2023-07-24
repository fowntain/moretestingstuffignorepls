FROM ubuntu:20.04

# Install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        x11vnc \
        xvfb \
        fluxbox \
        net-tools \
        curl \
        ca-certificates \
        sudo \
        git \
        openssh-client \
        gnupg2 \
        apt-transport-https \
        lsb-release \
        wget \
        vim \
        nano \
        xterm

# Set up non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME && \
    useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL >/etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

# Set up display and Fluxbox
ENV DISPLAY :1
RUN mkdir -p /home/$USERNAME/.fluxbox && \
    echo 'xterm &\nfluxbox' > /home/$USERNAME/.fluxbox/startup && \
    chown -R $USERNAME:$USERNAME /home/$USERNAME/.fluxbox

# Set up VNC
RUN mkdir -p /home/$USERNAME/.vnc && \
    x11vnc -storepasswd 1234 /home/$USERNAME/.vnc/passwd && \
    chown -R $USERNAME:$USERNAME /home/$USERNAME/.vnc

# Switch to non-root user
USER $USERNAME

# Expose VNC port
EXPOSE 5900
