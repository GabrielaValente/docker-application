# Projeto Docker Compose
=====================

Um simples tracker de idade API construído com Flask (backend) e Nginx (proxy reverso) no Docker.

## Executando a Aplicação
-------------------------

Para iniciar a aplicação, basta executar o seguinte comando na sua terminal:

```bash
docker-compose up --build
```

Isso constrói as imagens do Docker para os serviços backend e frontend, e depois começa. A Aplicação estará disponível em `http://localhost`.

## Visão geral dos Arquivos de Docker
--------------------------------

O projeto consiste em três principais arquivos de Docker:

### Dockerfile (nginx:alpine)

- Usa uma imagem de base do nginx Linux Alpine
- Define um novo diretório para a aplicação web (`/usr/share/nginx/html`)
- Copia o diretório atual (`.`) nesse novo diretório, efetivamente deployando o frontend no diretório `html` de Nginx.
- Exibe a porta 80 para a aplicação
- Configura Nginx usando um arquivo de configuração externo (`nginx.conf`)

### Dockerfile (backend)

- Define a base da imagem como Python 3.12 slim.
- Copia o arquivo de requisições (requirements.txt) e instala as dependências necessárias para a aplicação.
- Copia outros arquivos importantes, incluindo um script que espera até que o serviço do MySQL esteja disponível.
- Define várias variáveis de ambiente para passar valores de configuração à aplicação.
- Expose a porta 5000 e define a ordem de execução para iniciar a aplicação.

### (db)

- Usa a imagem oficial do MySQL 8.0
- Configura o ambiente da base de dados usando segredos do arquivo `docker-compose.yml`
- Monta volumes do diretório `db-data-idade`

O arquivo `docker-compose.yml` coordena a construção e execução desses serviços.
