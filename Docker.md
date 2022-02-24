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
