

# O que é uma chave de API de um LLM?

Uma **chave de API (API Key)** é um **identificador usado para autenticar e autorizar o acesso a um serviço de inteligência artificial hospedado na nuvem**, como modelos da OpenAI, Google ou Anthropic.

Esses modelos são chamados de **LLMs (Large Language Models)** e rodam em servidores dessas empresas.

Quando um programa quer utilizar um modelo como **Gemini ou Llama**, ele precisa **enviar uma requisição para a API do provedor**.

A **API Key funciona como uma credencial**, semelhante a uma senha, que informa ao servidor:

* quem está fazendo a requisição
* qual projeto está usando o serviço
* quais limites e permissões se aplicam
* como contabilizar o uso (rate limit, billing etc.)

Sem essa chave, o serviço **não permite o acesso ao modelo**.


# Como a chave de API funciona na prática

Quando um programa envia uma solicitação para um LLM, ele inclui a chave no **cabeçalho da requisição HTTP**.

Exemplo simplificado:

```http
POST /v1/chat/completions
Authorization: Bearer SUA_API_KEY
Content-Type: application/json
```

O servidor então:

1. valida a chave
2. identifica o usuário ou projeto
3. verifica limites de uso
4. processa a solicitação no modelo
5. retorna a resposta do LLM


# Recomendações para o case: API do Gemini ou Groq


# GEMINI

## 1. Acessar o Google AI Studio

Entre em:

[https://aistudio.google.com](https://aistudio.google.com)

Faça login com sua **conta Google**.


## 2. Criar a chave

Clique em **Create API key**.

Escolha **Gemini Default Project**.

Após confirmar, a **API Key será gerada**.


## 3. Copiar e guardar a chave

A chave terá formato parecido com:

```
AIzaSy**************
```

Guarde em um local seguro.

Ela será usada para **autenticar suas requisições à API**.


# GROQ

## 1. Criar conta

Acesse:

[https://console.groq.com](https://console.groq.com)

Clique em **Sign Up** e crie sua conta usando:

* Google
* GitHub
* Email


## 2. Criar API Key

No menu lateral clique em:

```
API Keys
```

Depois clique em:

```
Create API Key
```

Defina:

* nome da chave
* data de expiração

Clique em **Submit**.

A chave terá formato parecido com:

```
gsk_xxxxxxxxxxxxxxxxxxxxx
```

Copie e guarde, pois **não poderá visualizá-la novamente**.


# Exemplo prático: fluxo n8n + Gemini

Neste exemplo criaremos um fluxo onde:

1. um **Webhook** recebe uma requisição HTTP
2. a mensagem é enviada para o **Gemini**
3. o modelo processa a pergunta
4. a resposta é devolvida ao usuário

Arquitetura do fluxo:

```
Usuário → Webhook → Gemini → Resposta
```


# Passo 1 — Criar um workflow

Abra o workspace do n8n e crie um **novo workflow**.


# Passo 2 — Criar o Webhook

## O que é um Webhook?

Um **Webhook** é um endpoint HTTP que permite que sistemas externos enviem dados para um workflow.

Neste caso ele será responsável por **receber uma pergunta enviada pelo usuário**.


## Configuração

Adicionar node **Webhook** com os parâmetros:

```
HTTP Method: POST
Path: chat
Respond: Using Respond to Webhook Node
```


# Passo 3 — Adicionar node Gemini

Adicionar o node **Google Gemini → Message a model**.


## Configurar credenciais

Clique em:

```
Credentials → Create new credential
```

Insira sua **API Key do Gemini**.


## Configuração do node

```
Resource: Text
Model: gemini-3-pro-preview
```

No campo **Prompt** use a expressão:

```text
Responda a seguinte pergunta do usuário de forma clara e objetiva:

{{$json["body"]["message"]}}
```


# Passo 4 — Node de resposta

Adicionar o node:

```
Respond to Webhook
```

Configuração:

```
Respond With: JSON
```

Response Body:

```json
{
  "response": "{{$json.content.parts[0].text}}"
}
```


# Passo 5 — Publicar workflow

Clique em:

```
Publish
```

Depois:

```
Execute Workflow
```


# Passo 6 — Testar o fluxo

Endpoint gerado:

```
http://localhost:5678/webhook/chat
```

Exemplo de requisição:

```bash
curl -X POST http://localhost:5678/webhook/chat \
 -H "Content-Type: application/json" \
 -d '{"message":"Explique o que é um LLM em uma frase."}'
```


# Fluxo da requisição

1. Webhook recebe a pergunta
2. mensagem vai para o **Gemini**
3. o modelo gera uma resposta
4. o **Respond to Webhook** devolve o resultado


Se quiser, também posso te entregar **uma versão muito mais profissional dessa documentação (estilo README de projeto open-source)** com:

* **table of contents automático**
* **diagramas de arquitetura**
* **callouts (tips / warnings)**
* **melhor didática para alunos**

Ela fica **bem nível documentação oficial de projeto**.
