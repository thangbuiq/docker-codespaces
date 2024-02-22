FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04
LABEL maintainer=thangbuiq

# Dependencies install and update
RUN apt-get update && \
    apt-get -qy full-upgrade && \
    apt-get install -qy curl ca-certificates

# Add Docker's official GPG key
# I follow this document: https://docs.docker.com/engine/install/ubuntu/
RUN \
    apt-get update && \
    install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc && \
    chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
RUN \
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null
    
# Install Docker and Docker plugins
RUN \
    apt-get update && \
    apt-get install -qy \
    docker-ce docker-ce-cli docker-compose-plugin

# Install starship for vscode user with pure prompt
RUN \
    sh -c "$(curl -fsSL https://starship.rs/install.sh)" -- --yes && \
    echo 'eval "$(starship init bash)"' >> ~/.bashrc

USER vscode
RUN \
    mkdir -p ~/.config/ &&
    starship preset pure-preset -o ~/.config/starship.toml
  