# Actividad 5.3

En esta actividad he creado un docker-compose.yml, este archivo usa las imagenes
- node
- php
- apache
- mariadb
- phpmyadmin

## Node
La configuración del recurso en el docker compose es el siguiente
```
  node:
    image: docker.io/bitnami/node:latest
    ports:
      - 3000:3000
    volumes:
      - ./www/:/var/www/html/
    tty: true
```
