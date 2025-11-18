FROM mysql:8.0

# ARGを使用してビルド時に環境変数を受け取る
ARG MYSQL_DATABASE \
    MYSQL_USER \
    MYSQL_PASSWORD

# ENVを使用してコンテナ実行時に環境変数を設定
ENV MYSQL_DATABASE=${MYSQL_DATABASE} \
    MYSQL_USER=${MYSQL_USER} \
    MYSQL_PASSWORD=${MYSQL_PASSWORD} \
    MYSQL_ROOT_PASSWORD=${MYSQL_PASSWORD}

# タイムゾーンの設定
ENV TZ=Asia/Tokyo

COPY ./my.cnf /etc/my.cnf
RUN chmod 644 /etc/my.cnf

