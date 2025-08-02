# ☀️ Workflow de Previsão do Tempo com Open-Meteo (n8n)

Este workflow automatizado utiliza a API Open-Meteo para coletar a **previsão do tempo do dia atual** (máxima, mínima e chance de chuva) e envia as informações formatadas automaticamente para o canal configurado (como WhatsApp, Telegram, Slack, etc).

---

## 🔁 Fluxo do Workflow

1. **⏰ Gatilho**
   - Inicia a execução automaticamente em um intervalo pré-configurado (por exemplo, diariamente às 7h).
   - Pode usar o nó `Cron` do n8n.

2. **🗓️ Formata a Data do Dia**
   - Converte a data atual para o formato `YYYY-MM-DD`, necessário para usar na requisição da API.

3. **🧠 Data Real API (Set)**
   - Cria as variáveis `start_date` e `end_date` com a data atual, para ajustar os parâmetros da requisição.

4. **🌦️ Coleta Informações do Clima**
   - Faz a requisição HTTP para a **API da Open-Meteo** com os seguintes parâmetros:
     - Temperatura máxima (`temperature_2m_max`)
     - Temperatura mínima (`temperature_2m_min`)
     - Probabilidade máxima de chuva (`precipitation_probability_max`)
   - Exemplo de URL chamada:
     ```bash
     https://api.open-meteo.com/v1/forecast?latitude=-23.5505&longitude=-46.6333&daily=temperature_2m_max,temperature_2m_min,precipitation_probability_max&timezone=auto&start_date=YYYY-MM-DD&end_date=YYYY-MM-DD
     ```

5. **📤 Envia as Informações**
   - Formata os dados recebidos em uma mensagem legível.
   - Envia para o canal desejado (WhatsApp, e-mail, chatbot etc.) com os dados do dia:

     ```
     🌤️ Previsão para São Paulo (hoje):
     - Temperatura máxima: 28°C
     - Temperatura mínima: 17°C
     - Chance de chuva: 70%
     ```

---

## 📌 Requisitos

- Conta no [n8n](https://n8n.io/)
- Conexão com algum canal de envio (WhatsApp, Telegram, Email, etc.)
- Nenhuma autenticação necessária na Open-Meteo

---

## 📦 Tecnologias usadas

- n8n (Automação)
- Open-Meteo API (Clima)
- Formatação de data com JavaScript no n8n

---

## ✅ Exemplo de uso

Este fluxo pode ser agendado para rodar todos os dias de manhã e enviar automaticamente a previsão do tempo para seus contatos ou clientes, ideal para:

- Assistentes virtuais
- Sistemas de alerta meteorológico
- Agendas e rotinas automatizadas
