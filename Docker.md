# Docker

## Conceito

Pradrão de unidade de software que empacota código e todas as dependências de uma aplicação, fazendo que a mesma seja executada rapidamente de forma confiável de um ambiente computacional para o outro.


## Containers vs VMs

- Nas VMs, em cima da camada de virtualização, instala-se diversos SOs (Guest) para rodar dentro deles as aplicações.
- Nos Containers, o Docker usa o SO (Host) como base para rodar as aplicações, sendo assim mais leve.


## Pontos Importantes

### Namespaces

- Garante o isolamento dos containers no sistema

### CGroups

- Permite a limitação dos recursos disponíveis para cada container (memoria, cpu)

### File System

- OFS (Overlay File System)
- Aproveitamento de dependências entre os containers


## Imagem

- Todos os containers são baseados em uma imagem, onde imagem "zerada" é chamada de Scratch.
- Estado imutável: a imagem não se modifica.
- Camada Read/Write
  - Permite acessar, rodar comandos, gravar e ler arquivos.
  - Se derrubar o container e criar um outro com a mesma imagem, os dados desta camada são perdidos.
- Podem ser criados volumes nos containers a partir de pastas locais do computador
- hub.docker.com, repositório com várias imagens

## Dockerfile

- Arquivo Dockerfile define as características da imagem a ser criada.
- Exemplo do arquivo:

      FROM: ImageName
      
      RUN: Comandos
      
      EXPOSE: 8000 (porta)

## Registry

- Repositório de imagens do docker.
- Podem ser usados comandos pull e push.

## Comandos

### docker ps

- Lista os containers que estão rodando.
- `-a` Lista os containers que rodaram recentemente.

### docker run

- Executa uma imagem do docker.
- Se não houver a imagem localmente, ele realiza um pull do repositório remoto da imagem e suas dependências.
- `-p 8080:80` Quando acessar a porta 8080 do meu computador, irá acesar a porta 80 do meu container.
