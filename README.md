# Actividad 5.3

En esta actividad he creado un docker-compose.yml, este archivo usa las imagenes
- node
- php
- apache
- mariadb
- phpmyadmin

## Node
La configuración de node en el docker compose es el siguiente
```
  node:
    image: docker.io/bitnami/node:latest
    ports:
      - 3000:3000
    volumes:
      - ./www/:/var/www/html/
    tty: true
```

- node: es el nombre del servicio
- image: la imagen de node que uso es la ultima version de docker.io/bitnami/node
- ports: los puertos con los que se conecta el contenedor con la maquina host es el 3000:3000
- volumes: el lugar donde persisten los datos de node es en el directorio /var/www/html/
- tty: asigne un dispositivo de terminal al contenedor

## php
La configuración de php en el docker compose es el siguiente

```
  php:
    build: './php_docker/'
    volumes:
      - ./www/:/var/www/html/
```
- build: construye una imagen a partir de un dockerfile que se encuentra en /php_docker/
- volumes el lugar donde los archivos se guardarán será en /var/www/html/

## Apache
La configuracion de apache es el siguiente:  

```
  apache:
    build: './apache_docker/'
    depends_on:
      - php
    ports:
      - "80:80"
    volumes:
      - ./www/:/var/www/html/   
```

- depends on: depende del funcionamiento de php
- ports: los puertos con el que está conectado con el host es el 80:80
- volumes: apache mantiene sus datos en el directorio /var/www/html/

## mariadb
La configuración de mariadb es la siguiente:  
```
    mariadb:
    image: mariadb:10.11
    environment:
      MYSQL_ROOT_PASSWORD: password123
    volumes:
      - mysqldata:/var/lib/mysql
```
- image: la imagen que usa es la version 10.11 de mariadb
- enviorement: mariadb necesita la contraseña root de mysql, en este caso la contraseña es password123
- volumes: mariadb guarda sus datos en el directorio /var/lib/mysql

## phpmyadmin
La configuración de phpmyadmin es:

```
    phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    ports:
      - 8080:80
    environment:
      PMA_HOST: mariadb
    depends_on:
      - mariadb
```

- image: usa la ultima version de phpmyadmin/phpmyadmin
- ports: los puertos de comunicacion entre el contenedor y el host es el 8080:80
- environment: el host que usa php es el host de mariadb
- depends_on: depende del funcionamiento de mariadb
