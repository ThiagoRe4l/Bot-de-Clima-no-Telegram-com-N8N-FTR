# 🌤️ Bot de Clima no Telegram

## 📖 Descrição

Este projeto é um chatbot interativo para o Telegram que fornece a previsão do tempo atualizada com base na cidade informada pelo usuário. Construído inteiramente com fluxos de automação no **n8n** e integrado com Inteligência Artificial, o bot processa o nome da cidade, consulta os dados climáticos em tempo real e retorna uma mensagem amigável e natural.

## 🚀 Funcionalidades

- Recebe o nome da cidade via mensagem do Telegram.
- Trata e normaliza o texto recebido para evitar erros de busca.
- Consulta a temperatura e a condição climática em tempo real via OpenWeatherMap.
- Utiliza um Agente de IA (Google Gemini) para reescrever os dados brutos de previsão do tempo, transformando-os em uma resposta humanizada e com emojis contextuais.
- Possui um sistema de _fallback_ (tratamento de erros) caso a IA não consiga processar a mensagem ou retorne formatos inesperados.

## 🛠️ Pré-requisitos e Variáveis de Ambiente

Para rodar este workflow localmente ou em um servidor próprio, você precisará configurar as credenciais no seu ambiente n8n. O sistema espera que você possua as seguintes chaves de acesso, que podem ser inseridas via variáveis de ambiente globais ou configuradas diretamente na interface do n8n:

- `TELEGRAM_BOT_TOKEN`: O token de acesso do seu bot gerado no [@BotFather](https://t.me/botfather).
- `OPENWEATHER_API_KEY`: A sua chave de API da [OpenWeatherMap](https://openweathermap.org/api).

## 📥 Como Importar o Workflow

1. Abra a interface web do seu **n8n**.
2. No menu lateral esquerdo, acesse a aba **Workflows** e clique no botão **Add Workflow** (canto superior direito).
3. Na tela do novo workflow, clique no ícone de três pontos `...` (canto superior direito) e selecione **Import from File**.
4. Selecione o arquivo `workflow-telegram-chatbot.json` disponibilizado neste repositório.
5. O fluxo será desenhado na sua tela. Não se esqueça de clicar em **Save**.

## 🔐 Configuração das Credenciais

Após importar o workflow, os nós que exigem conexão externa precisarão ser autenticados com as suas contas.

### 1. Telegram

- Dê um duplo clique no nó **Telegram Trigger**.
- No campo **Credential to connect with**, selecione _Create New Credential_.
- Insira o seu `TELEGRAM_BOT_TOKEN` e salve.
- Certifique-se de selecionar essa mesma credencial nos nós de ação chamados "Send a text message".

### 2. OpenWeatherMap

- Dê um duplo clique no nó **HTTP Request**.
- Vá até a seção **Authentication** e crie uma nova credencial ou ajuste o _Query Parameter_ `appid` para receber a sua `OPENWEATHER_API_KEY`.

### 3. Google Gemini (Agente de IA)

- Dê um duplo clique no nó **Google Gemini Chat Model** (ligado ao AI Agent).
- Crie ou selecione a sua credencial da Google Palm API / Gemini para habilitar a geração de texto automatizada.

## ▶️ Como Testar

Com as credenciais configuradas, ative o workflow alternando a chave **Active** (no canto superior direito) para a posição ligada, ou clique em **Test Workflow**. Em seguida, abra o seu bot no Telegram e envie o nome de uma cidade (ex: `Curitiba, PR, BR`, `São Paulo, SP, BR`) para receber a previsão do tempo!
