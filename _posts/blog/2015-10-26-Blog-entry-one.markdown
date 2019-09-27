---
layout: post
title:  "Projeto Angular CLI com Docker"
date:   2019-09-27 14:00:00 -0300
categories: blog
---

---
#####Projeto Angular CLI com Docker
---
#####Pré-requisitos:
-	Node 8+
-	Angular CLI
-	Docker V18+
-	Preferencialmente: Linux

#####Instalar o node:
-   [https://nodejs.org](https://nodejs.org/en/download/)

#####Instalar o Angular(local):
```sh
    npm install -g @angular/cli
```

#####Criar novo projeto:
    ng new angularproject

#####Navegar ao projeto:
    cd angularproject

#####Criar uma imagem Docker:
    vim Dockerfile

#####Configurar imagem:
    FROM node:8
    RUN mkdir /usr/src/app
    WORKDIR /usr/src/app
    RUN npm install -g @angular/cli
    COPY . .

#####Criar docker-compose:
    cd ../
    vim docker-compose.yml

#####Configurar docker-compose:
    version: '3.5' # Definir versão atual
    services: # Definir services
      angular-service: # Nome da service
        container_name: angularcontainer # Nome do container
        build: ./angularproject # Localicação DockerfileW
        volumes: # Volumes
          - './angularproject:/usr/src/app'
        ports:
          - '4200:4200' # Porta
        command: >
          bash -c "npm install && ng serve --host 0.0.0.0 --port 4200"

#####Executar container e abrir o bash:
    docker exec -it nome_do_container /bin/bash

#####Rodar docker compose
    docker-compose up --build -d

#####Monitorar containers:
    docker ps

#####Monitorar imagens:
    docker images

#####Parar container:
    docker container stop nome_do_container

---