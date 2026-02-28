# ============================
# 3b1b-manim / ManimGL 専用 Dockerfile（高速版）
# ============================

FROM python:3.10-slim-bullseye

# 基本ツール
RUN apt-get update && apt-get install -y \
    git \
    bash \
    vim \
    build-essential \
    pkg-config \
    wget \
    curl \
    ca-certificates

# ManimGL に必要なライブラリ
RUN apt-get install -y \
    ffmpeg \
    libgl1-mesa-glx \
    libgl1-mesa-dev \
    libglu1-mesa \
    libpango1.0-dev \
    libx11-dev \
    libxcursor-dev \
    libxrandr-dev \
    libxi-dev \
    libxxf86vm-dev

# LaTeX（TexLive）最小構成 + dvipng
RUN apt-get install -y \
    texlive-latex-extra \
    texlive-fonts-recommended \
    texlive-latex-recommended \
    dvipng

WORKDIR /code

CMD ["bash"]
