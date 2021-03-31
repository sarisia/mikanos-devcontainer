# MikanOS-devcontainer

[ゼロからのOS自作入門](https://zero.osdev.jp/) で開発するOS (MikanOS) の
開発環境が設定された [VSCode Devcontainer](https://code.visualstudio.com/docs/remote/containers) 設定ファイル.

ベースイメージの詳細については [github.com/sarisia/mikanos-docker](https://github.com/sarisia/mikanos-docker)
を参照してください.

# 使い方

## テンプレートからリポジトリを作成

1. 当リポジトリページの右上 "Use this template" からリポジトリを作成 ([GitHub Docs](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template))

2. ローカルにチェックアウト

3. VSCode で devcontainer を開く ([VSCode Docs](https://code.visualstudio.com/docs/remote/containers#_quick-start-open-an-existing-folder-in-a-container))

## 既存のリポジトリに追加

当リポジトリの `.devcontainer` ディレクトリ, 及び含まれるファイルをダウンロードし,
既存のリポジトリに追加してください.

# バグ, 要望

[Twitter (@A1ces)](https://twitter.com/A1ces) や [Issues](https://github.com/sarisia/mikanos-devcontainer/issues) で教えてくださると嬉しいです！

# 参考

- [Docker ではじめる "ゼロからのOS自作入門" | Zenn](https://zenn.dev/sarisia/articles/6b57ea835344b6)
- [「ゼロからのOS自作入門」の副読本的記事 | Zenn](https://zenn.dev/karaage0703/articles/1bdb8930182c6c)
  - devcontainer の起動方法や, macOS での X11 Server の設定などが大変分かりやすく説明されています
