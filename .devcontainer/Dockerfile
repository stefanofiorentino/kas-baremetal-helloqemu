FROM ubuntu:22.04

RUN mkdir -p /opt/tmp

# Install system packages
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    python3 python3-pip python3-setuptools python3-wheel \
    git \
    gawk wget diffstat unzip texinfo gcc build-essential chrpath socat \
    cpio python3-pexpect xz-utils debianutils iputils-ping \
    python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint xterm \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install kas
RUN pip3 install kas

# Install required packages and set locale
RUN apt-get update && \
    apt-get install -y locales && \
    locale-gen en_US.UTF-8 \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    file \
    lz4 \
    zstd \
    && apt-get clean && rm -rf /var/lib/apt/lists/*


# Set environment variables
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

# Optional: set default workdir
WORKDIR /workspace

# Create a non-root user
RUN useradd -ms /bin/bash builder

RUN chown -R builder:builder /opt/tmp

# Give necessary permissions (optional: sudo, if needed)
# RUN apt-get install -y sudo && echo "builder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Switch to non-root user
USER builder
WORKDIR /home/builder

# Entry point (optional)
CMD [ "bash" ]

