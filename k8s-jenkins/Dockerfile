
FROM jenkins/jenkins:lts

USER root

# Update the package list and install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        gnupg \
        software-properties-common

# Use HTTP instead of HTTPS
RUN echo "deb http://packagecloud.io/github/git-lfs/debian bookworm InRelease" > /etc/apt/sources.list.d/git-lfs.list

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu focal stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null


# Install Docker but do not start it in the Dockerfile
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        docker-ce \
        docker-ce-cli \
        containerd.io


# Allow the Jenkins user to run Docker
RUN usermod -aG docker jenkins


# Switch back to the Jenkins user
USER jenkins
