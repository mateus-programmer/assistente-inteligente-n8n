# Assistente Inteligente de Atendimento com n8n, Telegram, Google Gemini e Google Sheets

Este projeto consiste na criação e automação de um **Assistente Inteligente de Atendimento ao Cliente** utilizando uma arquitetura moderna de baixo código (*low-code*). O sistema captura mensagens enviadas por usuários através de um bot no Telegram, processa o contexto conversacional utilizando inteligência artificial generativa, responde ao cliente em tempo real e registra todo o histórico de atendimento automaticamente em uma planilha do Google Sheets.

---

## 🚀 Arquitetura e Tecnologias Utilizadas

* **[n8n](https://n8n.io/):** Plataforma de automação de fluxo de trabalho (hospedada localmente) responsável por orquestrar todas as integrações.
* **[Telegram Bot API](https://core.telegram.org/bots):** Canal de interface conversacional com o usuário (`@m27ausbot`).
* **[Google AI Studio / Gemini](https://aistudio.google.com/):** Motor de inteligência artificial generativa (`models/gemini-3-flash-preview`) responsável pelo processamento de linguagem natural e formulação das respostas.
* **[Google Sheets API](https://developers.google.com/sheets/api):** Banco de dados em nuvem leve para auditoria, rastreabilidade e armazenamento estruturado do histórico de atendimentos.
* **[ngrok](https://ngrok.com/):** Ferramenta de tunelamento reverso para expor a instância local do n8n e receber webhooks externos do Telegram.

---

## ⚙️ Fluxo de Funcionamento (Workflow)

1. **Gatilho (`Telegram Trigger`):** O fluxo é acionado instantaneamente sempre que uma nova mensagem é enviada para o bot no Telegram.
2. **Processamento de IA (`Basic LLM Chain` + `Google Gemini Chat Model`):** A mensagem capturada é repassada para o modelo do Gemini, que interpreta a intenção do usuário e gera uma resposta coesa e contextualizada.
3. **Resposta Automática (`Send a text message`):** O n8n utiliza o ID do chat de origem para devolver a resposta da IA diretamente ao usuário no Telegram.
4. **Registro de Histórico (`Google Sheets - Append Row`):** Após o envio da resposta, o workflow grava automaticamente uma nova linha na planilha **Assistente de Atendimento Inteligente** contendo os seguintes dados:
   * `Data/Hora`: Timestamp exato do atendimento (`dd/MM/yyyy HH:mm:ss`).
   * `ID Usuário`: Identificador único do chat/usuário no Telegram.
   * `Nome`: Primeiro nome do cliente.
   * `Mensagem Cliente`: Texto original enviado pelo usuário.
   * `Resposta IA`: Resposta completa gerada pelo Google Gemini.

---

## 📦 Como Importar e Executar este Projeto

Para clonar ou importar este fluxo em sua própria instância do n8n, siga os passos abaixo:

### 1. Pré-requisitos
* Node.js e n8n instalados localmente.
* Conta ativa no [Telegram](https://telegram.org/) e um bot criado via `@BotFather`.
* Chave de API gratuita do [Google AI Studio](https://aistudio.google.com/).
* Conta Google com acesso ao Google Drive/Sheets e credencial OAuth2 configurada no n8n.

### 2. Preparação da Planilha
* Crie uma planilha no Google Sheets (ex.: `Assistente de Atendimento Inteligente`) com os seguintes cabeçalhos na linha 1 da aba `Página1`:
  `Data/Hora` | `ID Usuário` | `Nome` | `Mensagem Cliente` | `Resposta IA`

### 3. Importação no n8n
1. Baixe o arquivo `.json` do workflow disponível neste repositório.
2. Abra a sua instância local do n8n (`http://localhost:5678`).
3. No canto superior direito, clique em **Add Workflow** ➔ **Import from File** e selecione o arquivo `.json`.
4. Configure suas credenciais nos respectivos nós:
   * **Telegram API:** Insira o Token gerado pelo `@BotFather`.
   * **Google Gemini API:** Insira sua chave de API do Google AI Studio.
   * **Google Sheets OAuth2 API:** Conecte sua conta Google e selecione a planilha e a aba criadas.
5. Inicie o túnel do ngrok apontando para a porta do n8n:
   ```bash
   ngrok http 5678

## 💡 Demonstração Prática

O bot responde a saudações, dúvidas frequentes e interações de suporte de maneira fluida, servindo como uma excelente base para automações de atendimento ao cliente, captação de leads ou assistentes pessoais.

---

## 👤 Autor

Desenvolvido por **Mateus Iensen** ([mateus-programmer](https://github.com/mateus-programmer)).
