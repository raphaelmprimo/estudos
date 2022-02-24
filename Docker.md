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
- Podem ser criados volumes nos containers a partir de pastas locais do computador.
  - Isso permite manter os arquivos mesmo removendo um container. 
- hub.docker.com, repositório com várias imagens.

## Dockerfile

Arquivo Dockerfile define as características da imagem a ser criada.

### Conteúdo do Dockerfile

#### FROM {imageName:imageVersion}

- Define a imagem a ser utilizada.

#### COPY

- Define os arquivos a serem copiados
- Ex.: `COPY . .`

#### RUN {commands}

- Define os comandos a serem executados dentro do container.

#### EXPOSE {port}

- Define a porta a ser associada ao container.

#### ENTRYPOINT [{file}]

- Define qual arquivo executar ao iniciar o container.


## Registry

- Repositório de imagens do docker.
- Podem ser usados comandos pull e push.

## Comandos

### docker ps

- Lista os containers que estão rodando.
- `-a` Lista os containers que rodaram recentemente.

### docker run {imageName}

- Cria um container e executa nele uma imagem do docker.
- Se não houver a imagem localmente, ele realiza um pull do repositório remoto da imagem e suas dependências.
- `-p {portaLocal}:{portaContainer}` Quando acessar a porta `portaLocal` do meu computador, irá acesar a porta `portaContainer` do meu container. Ex.: `-p 8080:80` 
- `-d` Rodar de forma detached, se bloquear o terminal.
- `--name NOME` nomeia o container.

### docker stop {containerID / containerName}

- Parar um container.

### docker start {containerID / containerName}

- Inicia um container.

### docker rm {containerID / containerName}

- Remove um container.

### docker exec {containerID / containerName} {command}

- Executa um comando dentro do container.
- `-it` Entra de forma "interativa" dentro do comando (Ctrl+D para sair)

      docker exec -it nginx bash
      
### docker images

- Lista imagens instaladas/cacheadas no pc.

### docker build {DockerFileLocation}

- Cria localmente uma imagem a partir do Dockerfile.
- Usa-se um ponto `.` para definir que o Dockerfile está na pasta atual.
- `-t NOME` Define o nome da imagem
- Ex.: docker build -t raphaelmprimo/imagem-php .

### docker rmi {imageName}

- Remove localmente uma imagem.
