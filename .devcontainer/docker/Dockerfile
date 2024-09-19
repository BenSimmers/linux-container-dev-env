FROM debian:bookworm-slim

ARG user_id=1000
ARG group_id=$user_id

ARG usr=bensimmersdev
ARG workspace_env_name=workspace


RUN apt-get update && apt-get install -y \
  bash \
  bash-completion \
  sudo \
  git \
  ssh \
  vim \
  wget \
  curl \
  dpkg \
  gnupg \
  apt-transport-https \
  ca-certificates \
  build-essential \
  software-properties-common \
  libicu-dev \
  unzip \
  jq \
  htop \
  less \
  man \
  net-tools \
  iputils-ping \
  dnsutils \
  iproute2 \
  man-db \
  manpages \
  nano \
  tmux \
  locales \
  neofetch \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*

# Optional packages for c development
# ===================================
# RUN apt-get update && \
#   apt-get install -y libncurses5-dev libncursesw5-dev

# RUN apt-get update && \
#   apt-get install -y \
#   procps \
#   sysstat \
#   && apt-get clean -y \
#   && rm -rf /var/lib/apt/lists/*
# ===================================


# Optional packages for TypeScript development
# ===================================
# RUN apt-get update && \
#   apt-get install -y nodejs npm

# RUN npm install -g typescript
# ===================================

# Optional packages for Python development
# ===================================
# RUN apt-get update && \
#   apt-get install -y python3 python3-pip

# RUN pip3 install --upgrade pip
# ===================================

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
  locale-gen en_US.UTF-8 && \
  update-locale LANG=en_US.UTF-8

RUN groupadd --gid ${group_id} ${usr} \
  && useradd --uid ${user_id} --gid ${group_id} -m ${usr} \
  && echo "${usr} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/${usr} \
  && chmod 0440 /etc/sudoers.d/${usr} \
  && chown -R ${user_id}:${group_id} /home/${usr}

RUN mkdir -p /${workspace_env_name} && chown ${user_id}:${group_id} /${workspace_env_name}

USER ${usr}
WORKDIR /${workspace_env_name}

RUN mkdir -p ~/bin ~/scripts

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

ENV SHELL /bin/bash
