# MikanOS-devcontainer

[ゼロからのOS自作入門](https://zero.osdev.jp/) で開発するOS (MikanOS) の
開発環境が設定された [VSCode Devcontainer](https://code.visualstudio.com/docs/remote/containers) 設定ファイル.

ベースイメージの詳細については [github.com/sarisia/mikanos-docker](https://github.com/sarisia/mikanos-docker)
を参照してください.

使用例: [github.com/sarisia/mikanos](https://github.com/sarisia/mikanos)

# 使い方

## テンプレートからリポジトリを作成

1. 当リポジトリページの右上 "Use this template" からリポジトリを作成 ([GitHub Docs](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template))

2. ローカルにチェックアウト

3. VSCode で devcontainer を開く ([VSCode Docs](https://code.visualstudio.com/docs/remote/containers#_quick-start-open-an-existing-folder-in-a-container))

4. 本の手順に従い [VcXsrv](https://sourceforge.net/projects/vcxsrv/) を導入, 起動することで,
QEMU での動作確認ができます

## 既存のリポジトリに追加

当リポジトリの `.devcontainer` ディレクトリ, 及び含まれるファイルをダウンロードし,
既存のリポジトリに追加してください.

# M1 Mac で使う

クロスコンパイル関連の追加の設定が必要です.
[`mikanos-docker` のドキュメント](https://github.com/sarisia/mikanos-docker#m1-mac-%E3%81%A7%E3%81%AE%E5%8B%95%E4%BD%9C%E3%81%AF) を参照して下さい.


# WSLg で動作確認

Windows 11, 及び Windows 10 21362以降では, [WSLg](https://github.com/microsoft/wslg) を
利用することで, VcXsrv などを導入せずに QEMU での動作確認が可能です.

## 設定

1. [WSLg ドキュメント](https://github.com/microsoft/wslg) に従い, WSLg を有効化
2. `.devcontainer/devcontainer.json` に設定を追加

    最新の [`.devcontainer/devcontainer.json`](https://github.com/sarisia/mikanos-devcontainer/blob/master/.devcontainer/devcontainer.json) を参考に, 以下の設定を追加:

    ```json
    "mounts": [
        "type=bind,source=/tmp/.X11-unix,target=/tmp/.X11-unix"
    ],
    "containerEnv": {
        "DISPLAY": "${localEnv:DISPLAY}"
    },
    ```


# VNC イメージ

VNC 設定を有効にすることで, ホストに X11 Server を用意すること無く, MikanOSの
動作確認をすることが可能です. また, [GitHub Codespaces](https://github.com/features/codespaces)
を利用することで, ブラウザのみでコーディング&動作確認を完結することができます.

## 設定

- 利用するイメージを `ghcr.io/sarisia/mikanos:vnc` に設定

    `.devcontainer/Dockerfile` を直接変更する, もしくは最新の
    [`.devcontainer/devcontainer.json`](https://github.com/sarisia/mikanos-devcontainer/blob/master/.devcontainer/devcontainer.json)と [`.devcontainer/Dockerfile`](https://github.com/sarisia/mikanos-devcontainer/blob/master/.devcontainer/Dockerfile) を参考に設定して下さい.

- devcontainer 設定を追加

    最新の [`.devcontainer/devcontainer.json`](https://github.com/sarisia/mikanos-devcontainer/blob/master/.devcontainer/devcontainer.json) を参考に, 以下の設定を追加して下さい:

    ```json
    "forwardPorts": [6080],
    "overrideCommand": false,
    "containerEnv": {
        // Port for noVNC Web Client & WebSocket
        "NOVNC_PORT": "6080",
        // VNC port QEMU listens. Default to 5900 + <display number>
        // If you run QEMU with "-vnc :1", then VNC_PORT should be 5901.
        "VNC_PORT": "5900",
        // QEMU launch options. Used in `run_image.sh`
        "QEMU_OPTS": "-vnc :0"
    },
    ```
  
## カスタマイズ

環境変数を通じてカスタマイズが可能です. 詳細は [mikanos-docker ドキュメント](https://github.com/sarisia/mikanos-docker#%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA)
を参照して下さい.

# トラブルシューティング

[`sarisia/mikanos-docker` の Wiki をご確認ください.](https://github.com/sarisia/mikanos-docker/wiki/Troubleshooting)

# バグ, 要望

[Twitter (@A1ces)](https://twitter.com/A1ces) や [Issues](https://github.com/sarisia/mikanos-devcontainer/issues) で教えてくださると嬉しいです！

# 参考

- [Docker ではじめる "ゼロからのOS自作入門" | Zenn](https://zenn.dev/sarisia/articles/6b57ea835344b6)
- [ブラウザだけでOS自作入門しよう | Zenn](https://zenn.dev/sarisia/articles/8dbe4fe2f1c656)
- [「ゼロからのOS自作入門」の副読本的記事 | Zenn](https://zenn.dev/karaage0703/articles/1bdb8930182c6c)
    - devcontainer の起動方法や, macOS での X11 Server の設定などが大変分かりやすく説明されています
