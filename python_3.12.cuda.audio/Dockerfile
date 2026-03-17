FROM nzvio/python:3.12.cuda

# Системные зависимости для звука
RUN apt-get update && apt-get install -y \
    portaudio19-dev \
    ffmpeg \
    libsndfile1 \
    && rm -rf /var/lib/apt/lists/*

# В ключаем игнорирование системных ограничений pip (PEP 668), чтобы внутри контейнера всё ставилось без лишних флагов
ENV PIP_BREAK_SYSTEM_PACKAGES=1
