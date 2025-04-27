ARG VARIANT="noble"
FROM buildpack-deps:${VARIANT}-curl

LABEL dev.containers.features="common"

# Environment variables
ENV FRONTEND=noninteractive \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    SHELL=/bin/bash

# Delete default 'ubuntu' user if needed, install packages, setup locale, create new user
ARG user_id=1000
ARG group_id=${user_id}
ARG usr=bensimmersdev
ARG workspace_env_name=workspace

RUN if id "ubuntu" 2>/dev/null; then userdel -f -r ubuntu; fi && \
    apt-get update && apt-get install -y --no-install-recommends \
    bash bash-completion sudo git ssh vim wget curl dpkg gnupg apt-transport-https \
    ca-certificates build-essential software-properties-common libicu-dev unzip jq \
    htop less man net-tools iputils-ping dnsutils iproute2 man-db manpages nano tmux \
    locales neofetch && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen en_US.UTF-8 && update-locale LANG=en_US.UTF-8 && \
    groupadd --gid ${group_id} ${usr} && \
    useradd --uid ${user_id} --gid ${group_id} -m ${usr} && \
    echo "${usr} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/${usr} && chmod 0440 /etc/sudoers.d/${usr} && \
    mkdir -p /${workspace_env_name} /home/${usr}/bin /home/${usr}/scripts && \
    chown -R ${user_id}:${group_id} /home/${usr} /${workspace_env_name} && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

USER ${usr}
WORKDIR /${workspace_env_name}
