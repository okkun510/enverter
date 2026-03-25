# enverter

`enverter` は macOS 環境を設定するためのスクリプトです。

## 新しいPCのセットアップ手順

### 0. 事前準備

Xcode Command Line Tools をインストールします。

```bash
xcode-select --install
```

SSH キーを作成し、GitHub に登録します。

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

表示された公開鍵を https://github.com/settings/keys から登録してください。

### 1. dotfiles のセットアップ

```bash
git clone git@github.com:okkun510/dotfiles.git ~/ghq/github.com/okkun510/dotfiles
cd ~/ghq/github.com/okkun510/dotfiles
git checkout personal
sh init.sh
```

`.Brewfile` や `.zshrc` などの設定ファイルがシンボリックリンクで配置されます。
初回実行時に Git の名前とメールアドレスの入力を求められます。

### 2. enverter のセットアップ

```bash
git clone git@github.com:okkun510/enverter.git ~/ghq/github.com/okkun510/enverter
cd ~/ghq/github.com/okkun510/enverter
sh src/init.sh
```

Homebrew、Zinit、Mise がインストールされ、`.Brewfile` に記載されたパッケージが一括インストールされます。

### 3. ターミナルを再起動

## Brewfile

### 動作仕様

`~/.Brewfile` を使用して以下のように動作します：

#### Brewfile が存在する場合
1. Homebrew をインストール（未インストールの場合）
2. `brew doctor` / `brew update` / `brew upgrade` を実行
3. `brew bundle` で Brewfile からパッケージをインストール
4. `brew bundle dump` で最新状態を Brewfile に記録（更新）

#### Brewfile が存在しない場合
1. Homebrew をインストール（未インストールの場合）
2. `brew bundle dump` で現在インストールされているパッケージを Brewfile として作成
3. `brew doctor` / `brew update` / `brew upgrade` を実行

### Brewfile の手動更新

パッケージを追加・削除した後、Brewfile を手動で更新する場合：

```bash
brew bundle dump --force --describe --file ~/.Brewfile
```

## ライセンス

このプロジェクトは [MIT ライセンス](LICENSE) のもとにライセンスされています。
