# Nginx for proxy server with Let's Encrypt on docker

以下のDocker imageを使ったNginxの構築手順です。

- jwilder/nginx-proxy
- jrcs/letsencrypt-nginx-proxy-companion

## How to add app

アプリを追加するには、アプリ側のdoker-compose.ymlを修正します。

1. Add networks
2. Add encironment

ex: wordpress

```yml[docker-compose.yml]
sertivices:
  db:
    networks:
      - shared
    ...

  wordpress:
    networks:
      - shared
    environment:
      VIRTUAL_HOST: hoge.localhost
      LETSENCRYPT_HOST: hoge.localhost
      LETSENCRYPT_EMAIL: hoge@hoge.com
    ...

networks:
  default:
    external:
      name: bridge
  shared:
    name: shared
```

### docker-compose up -d

containerを起動すると自動でNginxが振り分けてくれます。
