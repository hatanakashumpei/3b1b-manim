# ============================
# 3b1b-manim / ManimGL 専用 Dockerfile
# ============================

FROM python:3.10-slim-bullseye

# 環境変数の設定
# Pythonのバッファリング無効化と、デフォルトのディスプレイ番号を指定
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    DISPLAY=:99

# パッケージインストール
RUN apt-get update && apt-get install -y --no-install-recommends \
    # 1. 基本ツール
    git \
    bash \
    vim \
    build-essential \
    pkg-config \
    wget \
    curl \
    ca-certificates \
    # 2. ManimGL に必要なシステムライブラリ
    ffmpeg \
    libgl1-mesa-glx \
    libgl1-mesa-dev \
    libglu1-mesa \
    libpango1.0-dev \
    libx11-dev \
    libxcursor-dev \
    libxrandr-dev \
    libxi-dev \
    libxxf86vm-dev \
    # 3. 仮想ディスプレイ（コンテナ内でGUIを動かすために必須）
    xvfb \
    xauth \
    # 4. LaTeX（3B1Bの数式レンダリングに必須のパッケージ群）
    texlive-latex-recommended \
    texlive-latex-extra \
    texlive-fonts-recommended \
    tipa \
    texlive-fonts-extra \
    texlive-science \
    dvipng \
    dvisvgm \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 作業ディレクトリの設定
WORKDIR /code

# pip 自体のアップグレード
RUN pip install --no-cache-dir --upgrade pip

# (オプション) リポジトリがマウントされる前提ですが、
# コンテナ起動時に自動でパスを通したい場合は以下を追加
ENV PYTHONPATH="/code:${PYTHONPATH}"

CMD ["bash"]
