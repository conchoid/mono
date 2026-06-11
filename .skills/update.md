# Dockerfile ベースイメージ更新手順

## 概要
mono/6.12.0-bookworm/Dockerfileのベースイメージを `debian:bookworm-slim` (Debian 12) から `debian:trixie-slim` (Debian 13) に更新する。

## 更新手順

### 1. ベースイメージの更新
Dockerfileの1行目を以下のように変更する：

**変更前:**
```dockerfile
FROM debian:bookworm-slim
```

**変更後:**
```dockerfile
FROM debian:trixie-slim
```

### 2. 動作確認
以下のコマンドでDockerイメージをビルドし、正常に動作することを確認する：

```bash
cd mono/6.12.0-bookworm
docker build -t conchoid/mono:6.12.0-trixie .
```

### 3. 互換性チェック
Debian 13への更新により、以下の点を確認する：

- パッケージの互換性（apt-getでインストールしているパッケージが利用可能か）
- Mono 6.12.0の動作確認
- GPGキーリングの設定が正常に動作するか
- Mono公式リポジトリ（stable-buster）の互換性
- ロケール設定の確認

### 4. テスト実行
実際のMonoプロジェクトでイメージを使用し、以下を確認する：

- ビルドが正常に完了するか
- Monoランタイムが正常に動作するか
- 依存関係の解決が正常に行われるか
- 実行時エラーが発生しないか

## 注意事項
- Debian 13 (trixie) は比較的新しいリリースのため、一部のパッケージやツールのバージョンが変更されている可能性がある
- Mono公式リポジトリが`stable-buster`を指定しているため、Debian 13との互換性を確認する必要がある
- 問題が発生した場合は、パッケージのバージョン指定や代替パッケージの検討が必要になる場合がある
- GPGキーリングの設定方法が変更されている可能性があるため、キー取得方法の確認が必要

