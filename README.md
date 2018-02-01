# NGINX Proxy build files

Example `docker-compose.yml` for your project:

```
version: '2'

services:

  web:
    image: nginx:1.13
    depends_on:
      - db
    environment:
      - VIRTUAL_HOST=www.127.0.0.1.xip.io
    networks:
      - default
      - nginx-proxy

  pma:
    image: phpmyadmin/phpmyadmin
    environment:
      - PMA_HOST=db
      - VIRTUAL_HOST=pma.127.0.0.1.xip.io
    networks:
      - default
      - nginx-proxy
    volumes:
      - /sessions
    depends_on:
      - db

  db:
    image: percona:5.7
    command: --character-set-server=utf8 --collation-server=utf8_general_ci


networks:
  nginx-proxy:
    external:
      name: nginx-proxy
```