# ビルド環境
FROM node:8.16.0 AS Builder

# GitHubよりソースコードを取得
RUN git clone https://github.com/ybkuroki/vuejs-webapp-sample.git

# 作業ディレクトリへ移動
WORKDIR /vuejs-webapp-sample

# パッケージのインストールとプロダクションビルド
RUN npm install \
  && npm run build


# 実行環境
FROM nginx:latest AS Runtime

# ビルド済みJavaScriptファイルとCSSファイルを追加
COPY --from=Builder /vuejs-webapp-sample/dist/ /usr/share/nginx/html/
# nginx.confを追加
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./server.conf /etc/nginx/conf.d/server.conf

EXPOSE 80 443
