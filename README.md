Dockerización de Nginx en Ubuntu (VMware)
Este tutorial está diseñado para principiantes y cubre cómo crear una imagen Docker personalizada basada en Nginx, configurar un archivo
docker-compose.yml y persistir el fichero de configuración de Nginx en una máquina virtual de Ubuntu en VMware. Al final, tendrás un repositorio 
de GitHub con los archivos Dockerfile, index.html, docker-compose.yml y README.md.

Requisitos previos
Una máquina virtual de Ubuntu en VMware.
Docker instalado en la máquina virtual.
Docker Compose instalado en la máquina virtual.
Git instalado en la máquina virtual.
Una cuenta de GitHub.
Pasos
Paso 1: Crear un directorio para el proyecto
En la terminal de la máquina virtual de Ubuntu, crea un directorio para el proyecto y navega hacia él:

mkdir nginx-docker-example
cd nginx-docker-example
Paso 2: Crear el archivo Dockerfile
Crea un archivo llamado Dockerfile en el directorio del proyecto:

touch Dockerfile
Abre el archivo Dockerfile en un editor de texto y agrega lo siguiente:

FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
Esto indica que la imagen se basará en la última versión de Nginx y copiará el archivo index.html en la ubicación predeterminada de Nginx.

Paso 3: Crear el archivo index.html
Crea un archivo llamado index.html en el directorio del proyecto:

touch index.html
Abre el archivo index.html en un editor de texto y agrega el contenido que desees, por ejemplo:

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Nginx Docker Example</title>
</head>
<body>
  <h1>Hello, Docker and Nginx!</h1>
</body>
</html>
Paso 4: Crear el archivo docker-compose.yml
Crea un archivo llamado docker-compose.yml en el directorio del proyecto:

touch docker-compose.yml
Abre el archivo docker-compose.yml en un editor de texto y agrega lo siguiente:

version: "3.9"

services:
  nginx:
    build: .
    image: my-nginx:latest
    volumes:
      - nginx-config:/etc/nginx
    ports:
      - "8080:80"

volumes:
  nginx-config:
Este archivo indica que se construirá la imagen de Docker en base al Dockerfile presente en el directorio actual, se etiquetará como my-nginx:latest
y se montará un volumen llamado nginx-config en /etc/nginx para persistir la configuración de Nginx.
