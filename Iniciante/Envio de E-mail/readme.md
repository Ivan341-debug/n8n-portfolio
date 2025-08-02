# Workflow: Cadastro via Webhook com Validação e Notificação por Email

Este workflow recebe dados de cadastro enviados via webhook, verifica se o email já está cadastrado em uma planilha do Google Sheets e, caso não esteja, envia um email de confirmação para o usuário. Se ocorrer algum erro no envio do email, o erro é registrado na mesma planilha junto com os dados do cadastro.

---

## Fluxo Geral

### 1. Receber cadastro via webhook

- O fluxo inicia com um nó **Webhook** que recebe os dados do cadastro (ex: nome, email, telefone, etc).

### 2. Verificar se o email já está cadastrado

- Consulta a planilha Google Sheets onde ficam os cadastros.
- Verifica se o email recebido já existe na planilha.

### 3. Condicional: Email já cadastrado?

- Se **sim**:  
  - O fluxo pode terminar ou enviar uma mensagem informando que o email já está cadastrado.
- Se **não**:  
  - Prossegue para o envio do email de confirmação.

### 4. Enviar email de confirmação

- Tenta enviar um email para o email recebido no cadastro, usando o node Gmail (ou outro serviço de email).

### 5. Tratamento de erro no envio de email

- Se o envio do email **falhar**:  
  - Registra o erro em uma nova linha da planilha Google Sheets, junto com os dados do cadastro e detalhes do erro.

---

## Detalhes Técnicos

- **Webhook**  
  - Recebe dados JSON via HTTP POST.

- **Google Sheets**  
  - Planilha usada para armazenar os cadastros e também os erros.  
  - Busca e comparação para validar emails já cadastrados.  
  - Adição de linhas novas (cadastros ou erros).

- **Envio de email**  
  - Usado para notificar o usuário que o cadastro foi realizado com sucesso.  
  - Pode ser integrado via Gmail, SMTP ou outro serviço.

- **Tratamento de erros**  
  - Captura falhas no node de envio de email.  
  - Insere linha com dados do erro na planilha para monitoramento.

---

## Exemplos de uso

- Cadastro simples de usuários em landing pages.  
- Inscrição para newsletters com validação de emails duplicados.  
- Processos automáticos de onboarding com registro de falhas para acompanhamento.

---

## Melhorias possíveis

- Adicionar confirmação via webhook para o front-end.  
- Enviar notificações para administradores em caso de erro.  
- Implementar remoção ou atualização de cadastro.

---