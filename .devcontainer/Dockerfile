# Start from Debian Bookworm with Python 3.11
FROM python:3.11-bookworm

# Install system dependencies
RUN apt-get update && apt-get install -y \
        openjdk-17-jdk curl wget git unzip sudo bash procps coreutils && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME for PySpark
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH:/usr/local/bin:/usr/bin:/bin

# Upgrade pip and install Python packages
RUN python3 -m pip install --upgrade pip --break-system-packages && \
    python3 -m pip install --break-system-packages \
        pyspark jupyterlab pandas matplotlib numpy graphframes

# Download GraphFrames JAR (compatible with Spark 4.0.1 / Scala 2.12)
RUN mkdir -p /opt/spark/jars && \
    curl -L -o /opt/spark/jars/graphframes.jar \
        https://repos.spark-packages.org/graphframes/graphframes/0.8.3-spark4.0-s_2.12/graphframes-0.8.3-spark4.0-s_2.12.jar

# Configure PySpark to automatically use GraphFrames JAR
ENV PYSPARK_SUBMIT_ARGS="--jars /opt/spark/jars/graphframes.jar pyspark-shell"

# Create vscode user (default for Codespaces)
RUN useradd -m -s /bin/bash vscode && \
    echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER vscode
WORKDIR /home/vscode