# Guia para Containerizar uma Aplicação Node.js com Docker

## Passo 1: Configurar o Dockerfile

Crie um arquivo chamado `Dockerfile` na raiz do projeto com o seguinte conteúdo:

```dockerfile
# Usa uma imagem base do Node.js
FROM node:18-alpine

# Define o diretório de trabalho no container
WORKDIR /app

# Copia os arquivos package.json e package-lock.json (se existir)
COPY package*.json ./

# Instala as dependências
RUN npm install

# Copia o restante do código da aplicação
COPY . .

# Exponha a porta em que a aplicação irá rodar
EXPOSE 3000

# Comando para rodar a aplicação em modo de desenvolvimento
CMD ["npm", "run", "dev"]
```

## Passo 2: Criar a Imagem Docker

docker build -t <namespace_remoto>/<nome_da_imagem>:<tag> .

exemplo: docker build -t gbeenard96/conversao-app:v1 .

## Passo 3: Rodar um Container para Teste

#### Para rodar um container da imagem criada, use um dos comandos abaixo:

### Opção 1: Rodar em Segundo Plano (Determinando a Porta)

docker container run -d -p 8080:3000 gbeenard96/conversao-app:v1

### Opção 2: Rodar e Mapear para uma Porta Diferente

docker run -p 3001:3000 gbeenard96/dietai-api:v1

### Opção 3: Rodar o Container com um Nome Específico

docker container run -d -p 8080:3000 --name meu-container gbeenard96/conversao-app:v1

exemplo: docker container run -d -p 8080:3000 --name conversao-app-container gbeenard96/conversao-app:v1

## Passo 4: Enviar a Imagem para o Docker Hub

docker push gbeenard96/dietai-api:v1

# Comandos Docker Úteis para Consulta

### Listar Imagens

docker images ls
docker images

### Deletar uma Imagem pelo ID

docker rmi <image_id>

##### Forçar a deleção (se a imagem estiver sendo usada):

docker rmi -f <image_id>

### Listar Containers em Execução

docker ps

### Listar Todos os Containers (Incluindo Parados)

docker ps -a

### Parar um Container

docker stop <container_id>

### Remover um Container

docker rm <container_id>

### Ver Logs de um Container

docker logs <container_id>

### Ver Detalhes de um Container

docker inspect <container_id>

### Acessar um Container em Execução

docker exec -it <container_id> /bin/bash

### Limpar Imagens e Containers Não Utilizados

##### Remover todas as imagens não utilizadas:

docker image prune

##### Remover todos os containers parados:

docker container prune

#### Remover todos os volumes não utilizados:

docker volume prune

### Construir e Rodar com Docker Compose

##### Para construir e rodar containers definidos em um docker-compose.yml:

docker-compose up --build

##### Para rodar os containers em segundo plano:

docker-compose up -d

##### Para parar os containers rodando pelo Docker Compose:

docker-compose down
