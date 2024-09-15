# ベースイメージとしてGoのバージョン1.21を使用
FROM golang:1.21

# 作業ディレクトリを `/usr/src/app` に設定
WORKDIR /usr/src/app

# `go.mod` と `go.sum` (依存関係の管理ファイル) をコンテナにコピー
COPY go.mod go.sum ./

# 依存関係をダウンロードし、キャッシュを利用してビルド
RUN go mod download

# プロジェクト全体をコンテナにコピー
COPY . /usr/src/app

# Goプログラムをビルド (CGOを無効化し、スタティックバイナリを作成)
# `CGO_ENABLED=0` は、C言語に依存しないビルドを意味する
# `-v` はビルドの詳細を表示し、`-o app` は出力ファイル名を `app` に指定
RUN CGO_ENABLED=0 go build -v -o app

# コンテナ実行時にビルドしたアプリケーションを起動
CMD ["./app"]