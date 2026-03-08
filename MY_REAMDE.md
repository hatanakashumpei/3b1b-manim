# 3b1b ManimGL Development Environment

3Blue1Brown の動画制作エンジンである **ManimGL** を、WSL2 + Docker (Dev Container) 上で安定して動作させるための特製環境です。複雑な依存関係、OpenGLのディスプレイ接続、および LaTeX のパッケージ問題をすべて解決済みです。

## 📜 改訂履歴

| バージョン | 日付 | 内容 |
| --- | --- | --- |
| **v0.1.0** | **2026/03/08** | 初版リリース（完全安定版）：Debian Bullseyeベースの構成確立、xvfb/xauthによる仮想ディスプレイ構築、tipa/texlive-science等によるLaTeXエラー解消、Jupyter連携最適化。 |

---

## 🛠️ 技術スタックと導入済みツール

* **Engine:** ManimGL (v1.7.2+)
* **Base OS:** Python 3.10-slim-bullseye
* **Display Strategy:** Xvfb (Virtual Framebuffer) / DISPLAY=:99
* **Renderers:** FFmpeg, OpenGL (Mesa)

### 🧰 プリインストール・パッケージ

* **システム:** `build-essential`, `pkg-config`, `xvfb`, `xauth`
* **グラフィックス:** `ffmpeg`, `libgl1-mesa-dev`, `libpango1.0-dev`
* **LaTeX 完全セット (3B1B Scene 対応済):**
* `texlive-latex-extra` / `texlive-science` (`physics.sty` 等)
* `texlive-fonts-extra` / `texlive-fonts-recommended` (`dsfont.sty` 等)
* `tipa` (発音記号・特殊記号用)
* `dvisvgm` / `dvipng` (数式のベクトル変換用)



---

## 🚀 セットアップと実行

### 1. コンテナの起動

1. VS Code でリポジトリを開く。
2. コマンドパレット (`Ctrl+Shift+P`) から `Dev Containers: Rebuild and Reopen in Container` を選択。
3. 初回起動時に `pip install -e .` が自動実行され、環境が整います。

### 2. レンダリングの実行 (CLI)

仮想ディスプレイ経由で動画を書き出します。

```bash
# 例：OpeningManimExample をレンダリングする場合
xvfb-run manimgl example_scenes.py OpeningManimExample -w

```

### 3. インタラクティブ開発 (Jupyter)

VS Code 内の Jupyter Notebook (`.ipynb`) で以下を実行すると、セル内に直接プレビューが表示されます。

```python
from manimlib import *

class MyScene(Scene):
    def construct(self):
        text = Text("Setup Complete!", color=BLUE)
        self.play(Write(text))

```

---

## 💡 攻略 Tips: 解決済みのトラブル

* **`NoSuchDisplayException` / `xauth` error**: ManimGLは描画時にダミーウィンドウを要求するため、xvfbとxauthを組み合わせた仮想ディスプレイ環境により、ヘッドレス環境での動作を実現しています。
* **`LaTeX Error: File xxx.sty not found`**: 3B1Bのシーンは標準外パッケージを多用するため、tipa、physics、dsfont等の主要パッケージをプリインストールして解消しています。

---

## 📂 生成物の出力先

* **動画:** `/code/videos/`
* **画像:** `/code/images/`
