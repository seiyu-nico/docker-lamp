# ssl-docker

## 開発方法
- app:/var/www/htmlなのでappディレクトリ内にプロジェクトを設置しapache.confを書き換えて起動してください

## apache設定ファイル
- ./web/apache.conf


## 起動方法
```
docker-compose up -d
```

## ssl化の方法
```yml:docker-compose.yml
https-portal:
  image: steveltn/https-portal:1
  ports:
    - '80:80'
    - '443:443'
  links:
    - web
  environment:
    STAGE: 'local'
    # STAGE: 'staging'
    # STAGE: 'production'
    DOMAINS: 'test.localhost -> http://web:8080'
    # FORCE_RENEW: 'true'
```
- 複数ドメインが存在する場合は、カンマ区切りで複数記述すればいい
```
DOMAINS: >-
  sample.localhost -> http://web:8000, 
  test.localhost -> http://web:8000
```

## その他
- virtualboxで利用する場合は、ホストからvirtualboxのゲストにポートフォワーディングを行うようにしてください