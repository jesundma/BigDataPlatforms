# Start from Debian bookworm (includes Python 3.11)
FROM debian:bookworm

# Install core utilities, Python, pip, and OpenJDK 17
RUN apt-get update && apt-get install -y \
        python3 python3-pip \
        openjdk-17-jdk \
        coreutils procps curl wget unzip git bash sudo && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME for PySpark
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH:/usr/local/bin:/usr/bin:/bin

# Upgrade pip and install Python packages
# The --break-system-packages flag avoids Debian Bookworm's PEP 668 restriction
RUN python3 -m pip install --upgrade pip --break-system-packages && \
    python3 -m pip install --break-system-packages pyspark jupyterlab pandas matplotlib numpy

# Create vscode user (default for Codespaces)
RUN useradd -m -s /bin/bash vscode && \
    echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER vscode
WORKDIR /home/vscode