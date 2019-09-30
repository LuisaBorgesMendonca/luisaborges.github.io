---
layout: post
title:  "Projeto Angular CLI com Docker"
date:   2019-09-27 14:00:00 -0300
categories: blog
---

---
## Projeto Angular CLI com Docker
---
## Pré-requisitos:
-	Node 8+
-	Angular CLI
-	Docker V18+
-	Preferencialmente: Linux

## Instalar o node:
-   [https://nodejs.org](https://nodejs.org/en/download/)

## Instalar o Angular(local):
```sh
    npm install -g @angular/cli
```

## Criar novo projeto:
```sh
    ng new angularproject
```

## Navegar ao projeto:
```sh
    cd angularproject
```

## Criar uma imagem Docker:
```sh
    vim Dockerfile
```

## Configurar imagem:
```docker
    FROM node:8
    RUN mkdir /usr/src/app
    WORKDIR /usr/src/app
    RUN npm install -g @angular/cli
    COPY . .
```

## Criar docker-compose:
```sh
    cd ../
    vim docker-compose.yml
```

## Configurar docker-compose:
```docker
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
```

## Executar container e abrir o bash:
```docker
    docker exec -it nome_do_container /bin/bash
```

## Rodar docker compose
```docker
    docker-compose up --build -d
```

## Monitorar containers:
```docker
    docker ps
```

## Monitorar imagens:
```docker
    docker images
```

## Parar container:
```docker
    docker container stop nome_do_container
```

---