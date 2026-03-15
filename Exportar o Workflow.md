# Como exportar o workflow do n8n para entregar no GitHub

Para realizar a entrega do desafio, você deverá **exportar o workflow criado no n8n em formato JSON** e enviá-lo para o repositório do GitHub.

Abaixo está o passo a passo.

---

## 1. Abrir o workflow no n8n

Acesse o n8n no navegador:
```text
http://localhost:5678
```

Abra o workflow que você criou para o desafio.

---

## 2. Exportar o workflow

No canto superior direito da interface do n8n:

1. Clique no botão de **três pontos (⋯)** ou no **menu do workflow**.
2. Selecione a opção **Download / Export**.
3. Escolha **Export as JSON**.

O arquivo será baixado no seu computador.

**Exemplo de nome do arquivo:**
```text
workflow.json
```

---

## 3. Adicionar o arquivo ao repositório

Coloque o arquivo exportado dentro do seu repositório do GitHub.

**Exemplo de estrutura recomendada:**
```text
projeto-inteli-academy/
│
├─ README.md
├─ workflow/
│   └─ workflow.json
```

---

## 4. Fazer commit e push

No terminal, execute:
```bash
git add .
git commit -m "Adiciona workflow do n8n"
git push
```

---

## 5. Verificar no GitHub

Após o push, confirme que o arquivo aparece no repositório.

> **Nota:** Esse será o arquivo utilizado pelos avaliadores para **importar e testar o seu workflow**.

---

# Dica importante

Antes de exportar o workflow:
- Verifique se ele **está funcionando** corretamente;
- Confirme se o fluxo retorna uma resposta válida.

> **Importante:** Isso garante que os avaliadores consigam executar o projeto perfeitamente.
