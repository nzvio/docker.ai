# Одноплатформенный образ (билдится с помощью обычно build под каждую платформу, под CUDA нас пока интересует только x86)
FROM nvidia/cuda:12.6.3-devel-ubuntu24.04

# Не задавать вопросы при установке
ENV DEBIAN_FRONTEND=noninteractive

# Установка пакетов
# Принято использовать apt-get, а не apt - вроде как стабильнее и меньше мусорит в консоль.
RUN apt-get update && \
    apt-get install -y \
    curl \
    wget \
    ca-certificates \
    tzdata \    
    locales \
    gnupg \
    net-tools \
    zip \
    build-essential \
    htop \
    cron \
    git \
    python3.12 \
    python3-pip \
    python3.12-dev \
    python3.12-venv \
    ninja-build \
    && rm -rf /var/lib/apt/lists/*

# Установка watchexec
RUN wget https://github.com/watchexec/watchexec/releases/download/v2.5.0/watchexec-2.5.0-x86_64-unknown-linux-gnu.deb -O /tmp/watchexec.deb && \
    apt-get update && apt-get install -y /tmp/watchexec.deb && \
    rm /tmp/watchexec.deb && \
    rm -rf /var/lib/apt/lists/*
    
# Делаем python 3.12 системным
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3.12 1 && \
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1

# Poetry
ENV POETRY_HOME="/opt/poetry"
ENV PATH="$POETRY_HOME/bin:$PATH"
RUN curl -sSL https://install.python-poetry.org | python3 -
# Разрешаем установку в систему, если вдруг приспичит через pip
ENV PIP_BREAK_SYSTEM_PACKAGES=1  

# Установка кодировок
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

# При входе в консоль системы попадаем в эту папку.
# Если указать доп. команды в docker-compose, они будут выполняться из этой папки (билды, установки и т.д.).
# Саму папку можно подмонтировать на абсолютно разные реальные папки проекта, в зависимости от дальнейших операций.
# Я специально не называю ее app, чтобы не путаться с папкой, которую я обычно использую для приложений, это именно произвольная папка старта, которая для контейнера - /worker, а реально - всё что угодно.
WORKDIR /worker

# В dev-режиме контейнер с этим образом не будет выполнять никаких процессов, просто висеть как запущенная ОС.
# Чтобы он не завершился после запуска, выполняется эта команда.
CMD ["sleep", "infinity"]
