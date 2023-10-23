# README.md

## Configurando o Docker para rodar Gazebo e ROS Foxy

Este guia tem como objetivo auxiliar na configuração do Docker para rodar o Gazebo e o ROS Foxy. 

### Pré-requisitos

- Docker instalado na máquina
- Conhecimento básico em Docker

### Criando a imagem

1. Clone o repositório do ROS Foxy:

### Executando
Criação da imagem:
```bash
sudo docker build -t turtlebot3 .
```

Execução do container:
```bash
sudo docker run -it turtlebot3
```