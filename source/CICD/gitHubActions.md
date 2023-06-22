# GitHub Actions

## 概要
GitHub Actionsは、GitHubが提供するCI/CDツールである。ユーザーはGitHubのリポジトリ内で直接、ビルド、テスト、デプロイなどのタスクを自動化できる。

## 特徴
- **ワークフロー自動化**: GitHub Actionsを使用すると、リポジトリにプッシュしたり、プルリクエストを作成したりするなどのGitHubのイベントに基づいて、様々なワークフローを自動的に実行できる。
- **言語とプラットフォームの幅広いサポート**: GitHub Actionsは、多くの主要な言語とプラットフォームをサポートしている。
- **組み込みの秘密情報管理**: 秘密情報はGitHubのリポジトリ設定で管理でき、ワークフロー内で安全に使用することができる。
- **アーティファクトとログの保存**: ワークフローの実行結果は自動的に保存され、後で確認できる。

## 利用シーン
GitHub Actionsは以下のようなシーンで有効である。

- **CI/CDパイプラインの自動化**: GitHub Actionsを使用して、コードのビルド、テスト、デプロイなどのタスクを自動化し、ソフトウェア開発プロセスを効率化できる。
- **コードレビューとブランチ管理**: プルリクエストやブランチに対する操作をトリガーとした自動化タスクを設定できる。
- **イシューやプルリクエストのトリアージ**: GitHub Actionsを用いて、イシューやプルリクエストの管理を自動化することができる。

## 設定手順
### 1. ワークフローの作成
まずはGitHubリポジトリ内に`.github/workflows`ディレクトリを作成する。このディレクトリ内にワークフローを定義するYAMLファイルを配置する。

### 2. ワークフローの定義
YAMLファイル内にワークフローを定義する。以下に基本的な構造を示す。

```yaml
name: ワークフロー名

on: [push, pull_request] # ワークフローのトリガーとなるイベントを指定

jobs:
  build: # ジョブの名前
    runs-on: ubuntu-latest # ジョブを実行するランナーを指定

    steps:
    - uses: actions/checkout@v2 # アクションを使用

    - name: Run a script # ステップの名前
      run: echo "Hello, world!" # 実行するコマンド
```
### 3. ワークフローの実行
ワークフローは指定したイベント（例えば、リポジトリへのプッシュやプルリクエストの作成）によって自動的に実行される。ワークフローの実行結果はGitHubの「Actions」タブで確認することができる。