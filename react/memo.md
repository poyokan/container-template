ディレクトリ構造
```
.
├─Dockerfile
├─docker-compose.yml
└─project(create-react-appで作成)
    ├─Dockerfile # 新規作成↓
    ├─docker-compose.yml 
    ├─package.json # 自動生成↓
    ├─package-lock.json
    ├─public
    ├─src
    └─node_modules

```

./Dockerfile
```
FROM node:16.15-alpine
WORKDIR /usr/src/app

```

./docker-compose.yml
```
version: '3.9'
services:
  <サービス名>:
    build:
      context: ./
      dockerfile: Dockerfile
    container_name: <コンテナ名>
    volumes:
      - ./:/usr/src/app
    ports:
      - "3000:3000"
```
reactプロジェクト作成コマンド
```
$ docker-compose run --rm サービス名 sh -c "npm install -g create-react-app && create-react-app <プロジェクト名>"
```

作成したreactプロジェクトディレクトリにDockerfile,docker-compose.ymlを追加する

./project/Dockerfile
```
FROM node:16.15-alpine

WORKDIR /<プロジェクト名>/

COPY package*.json /<プロジェクト名>/

RUN npm install

COPY ./ /<プロジェクト名>/

EXPOSE 3000

CMD ["npm", "start"]

```

./project/docker-compose.yml
```
version: '3.9'
services:
  <サービス名>:
    build:
      context: ./ # Dockerfileのある場所指定
      dockerfile: Dockerfile
    container_name: <コンテナ名>
    volumes:
      - ./:/<プロジェクト名>
    ports:
      - "3000:3000"
```