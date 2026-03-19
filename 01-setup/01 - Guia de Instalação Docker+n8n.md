# Instalação e Execução do n8n com Docker

## 1. Introdução

Este documento apresenta um passo a passo detalhado para instalar e executar o **n8n** localmente utilizando **Docker**. O objetivo é permitir que qualquer pessoa configure rapidamente um ambiente de automação local para **desenvolvimento, testes e experimentação com workflows e integrações**.

# O que é o n8n?

O **n8n** é uma plataforma de **automação de workflows** que permite integrar diferentes serviços, APIs e sistemas.

# O que é Docker?

O **Docker** é uma plataforma que permite executar aplicações dentro de **containers isolados**.

Um container contém tudo que a aplicação precisa para rodar:

- Código
- Dependências
- Configurações

# Instalação do Docker

## Instalação no Linux (Ubuntu / Debian)

### Passo 1 — Atualizar o sistema

```bash
sudo apt update
sudo apt upgrade -y
```

### Passo 2 — Instalar dependências

```bash
sudo apt install ca-certificates curl gnupg -y
```

### Passo 3 — Adicionar chave oficial do Docker

```bash
sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
 | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### Passo 4 — Adicionar repositório do Docker

```bash
echo \
"deb [arch=$(dpkg --print-architecture) \
signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo $VERSION_CODENAME) stable" \
| sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Passo 5 — Instalar Docker

```bash
sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Passo 6 — Verificar instalação

```bash
docker --version
```

**Exemplo de saída:**

```text
Docker version 27.x.x
```

### Passo 7 — Testar o Docker

```bash
sudo docker run hello-world
```

> **Nota:** Se aparecer uma mensagem de sucesso, o Docker foi instalado corretamente.

## Instalação no Windows ou macOS

### Passo 1

Acesse o site oficial do Docker:
[https://docs.docker.com/get-started/get-docker/](https://docs.docker.com/get-started/get-docker/)

### Passo 2

Baixe o **Docker Desktop**.

### Passo 3

Execute o instalador.

### Passo 4

Reinicie o computador se solicitado.

### Passo 5 — Verificar instalação

Abra o terminal e execute:

```bash
docker --version
```

# Inicializar o n8n

## 1. Criar o volume de dados

Esse comando cria o local onde serão armazenados os dados do n8n.

> **Importante:** Ele precisa ser executado **apenas uma vez**.

```bash
docker volume create n8n_data
```

## 2. Executar o n8n

Sempre que quiser iniciar o n8n novamente, execute:

```bash
docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -e GENERIC_TIMEZONE="America/Sao_Paulo" \
 -e TZ="America/Sao_Paulo" \
 -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
 -e N8N_RUNNERS_ENABLED=true \
 -v n8n_data:/home/node/.n8n \
 docker.n8n.io/n8nio/n8n
```

## 3. Verificar containers em execução

```bash
docker ps
```

**Saída esperada:**

```text
CONTAINER ID   IMAGE       PORTS
xxxxxxx        n8nio/n8n   0.0.0.0:5678->5678
```

# Acessar a interface do n8n

Abra o navegador e acesse:

```text
http://localhost:5678
```

No primeiro acesso será necessário criar:

- Usuário
- Senha
- Workspace inicial

> **Dica:** Depois disso a interface de criação de **workflows** aparecerá.

