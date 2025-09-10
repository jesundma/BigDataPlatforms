# Start from Debian bullseye
FROM debian:bullseye

# Install core utilities, Python, pip, OpenJDK 17
RUN apt-get update && apt-get install -y \
        python3 python3-pip \
        openjdk-17-jdk \
        coreutils procps curl wget unzip git \
        bash sudo && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME for PySpark
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH:/usr/local/bin:/usr/bin:/bin

# Install Python packages
RUN python3 -m pip install --upgrade pip && \
    python3 -m pip install pyspark jupyterlab pandas matplotlib numpy

# Create vscode user
RUN useradd -m -s /bin/bash vscode && \
    echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER vscode
WORKDIR /home/vscode
