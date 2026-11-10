# Assistente Inteligente de Atendimento com n8n, Telegram e Google Gemini

Este projeto consiste na criação e automação de um **Assistente Inteligente de Atendimento ao Cliente** utilizando uma arquitetura moderna de baixo código (*low-code*). O sistema captura mensagens enviadas por usuários através de um bot no Telegram, processa o contexto conversacional utilizando inteligência artificial generativa e devolve respostas dinâmicas e humanizadas em tempo real.

---

## 🚀 Arquitetura e Tecnologias Utilizadas

* **[n8n](https://n8n.io/):** Plataforma de automação de fluxo de trabalho (hospedada localmente).
* **[Telegram Bot API](https://core.telegram.org/bots):** Canal de interface conversacional com o usuário (`@m27ausbot`).
* **[Google AI Studio / Gemini](https://aistudio.google.com/):** Motor de inteligência artificial generativa (`models/gemini-3-flash-preview`) responsável pelo processamento de linguagem natural.
* **[ngrok](https://ngrok.com/):** Ferramenta de tunelamento reverso para expor a instância local do n8n e receber webhooks externos.

---

## ⚙️ Fluxo de Funcionamento (Workflow)

1. **Gatilho (Telegram Trigger):** O fluxo é acionado instantaneamente sempre que uma nova mensagem é enviada para o bot no Telegram[cite: 5].
2. **Processamento de IA (Basic LLM Chain + Google Gemini):** A mensagem capturada é repassada para o nó de inteligência artificial do Gemini, que interpreta a intenção do usuário e formula uma resposta coesa e contextualizada[cite: 7].
3. **Resposta Automática (Send a text message):** O n8n utiliza o ID do chat de origem para enviar a resposta gerada pela IA de volta ao usuário no Telegram de forma automatizada.

---

## 📦 Como Importar e Executar este Projeto

Se você deseja clonar ou importar este fluxo em sua própria instância do n8n, siga os passos abaixo:

1. **Pré-requisitos:**
   * Node.js e n8n instalados localmente.
   * Conta ativa no [Telegram](https://telegram.org/) e um bot criado via `@BotFather`.
   * Chave de API gratuita do [Google AI Studio](https://aistudio.google.com/).

2. **Passo a passo:**
   * Clone este repositório ou baixe o arquivo `.json` do workflow contido nele.
   * Abra a sua instância local do n8n (`http://localhost:5678`)[cite: 1].
   * No canto superior direito, clique em **Add Workflow** ➔ **Import from File** e selecione o arquivo JSON do projeto.
   * Configure as suas credenciais:
     * **Telegram API:** Insira o Token gerado pelo BotFather.
     * **Google Gemini API:** Insira a sua chave de API obtida no Google AI Studio.
   * Inicie o túnel do ngrok para apontar para a porta do n8n:
     ```bash
     ngrok http 5678
     ```
   * Alterne o status do workflow no n8n de **Inactive** para **Active** (Verde).

---

## 💡 Demonstração Prática

O bot responde a saudações, dúvidas frequentes e interações de suporte de maneira fluida, servindo como uma excelente base para automações de atendimento ao cliente, captação de leads ou assistentes pessoais.

---

## 👤 Autor

Desenvolvido por **Mateus Iensen** ([mateus-programmer](https://github.com/mateus-programmer)).
