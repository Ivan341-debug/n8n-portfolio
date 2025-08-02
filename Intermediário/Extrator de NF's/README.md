# 🧠 Descrição do Workflow: Análise de Imagens ou PDFs com IA e Retorno Automatizado

Este workflow permite o envio de um arquivo (imagem ou PDF) via webhook, realiza a leitura do conteúdo e aplica um modelo de IA para gerar uma análise estruturada, que é então enviada automaticamente de volta ao usuário. 

Esse projeto está integrado à Evolution API, mas pode ser usado de outras formas com base na necessidade.

---

## 🔁 Fluxo Geral

### 🚀 Gatilho: Webhook

- O fluxo é iniciado por um webhook HTTP (POST).
- Ele recebe um arquivo (imagem ou PDF) como entrada.

### 🧭 Roteamento: Identificação do tipo de arquivo

- Um nó **Switch** detecta se o arquivo é imagem ou PDF e encaminha o fluxo para o ramo apropriado.

---

### 📄 Ramo PDF

Quando o arquivo recebido for um PDF:

- 📥 **Base64 para PDF**  
  Converte o arquivo PDF de base64 para binário utilizável.

- 📃 **Conteúdo PDF**  
  Extrai o texto do conteúdo do PDF.

- 🤖 **Agente de Análise (com OpenAI)**  
  Envia o conteúdo textual para um agente de IA com um prompt personalizado que extrai as informações necessárias em um objeto JSON.  
  Utiliza um nó de Agent (do pacote de IA do n8n) conectado a:  
  - OpenAI Chat Model (modelo de linguagem)  
  - Structured Output Parser para gerar o output em JSON

- 📤 **Enviar Análise PDF**  
  Envia a análise gerada via outro canal (nesse caso, via Evolution API).

---

### 🖼️ Ramo Imagem

Quando o arquivo recebido for uma imagem:

- 📥 **Base64 para Imagem**  
  Converte a imagem recebida para um formato adequado (binário) para processamento.

- 🤖 **Análise da Imagem (com IA)**  
  Envia a imagem para o modelo da OpenAI com um prompt de interpretação visual.

- 📤 **Enviar Análise**  
  Entrega o resultado da análise ao usuário, como texto.

---

## 📌 Destaques Técnicos

- Agente de IA modular com memória, parser e prompt específico.
- Compatibilidade com múltiplos formatos de entrada (PDF e imagem).
- Automação completa de entrada → análise → resposta.
- Pode ser usado para análises de documentos, inspeções visuais, OCR inteligente, triagem de arquivos, entre outros.

---

## 💡 Exemplos de uso

- Análise de laudos médicos (PDF) com sumário gerado por IA.
- Interpretação de imagens de produtos ou impressões com feedback automatizado.
- Triagem de documentos enviados por clientes.
