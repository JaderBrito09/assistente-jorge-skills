# 🚀 Diretrizes de Prompting para Gemini (Google)

Este documento compila as especificações técnicas, boas práticas e recomendações oficiais para elaboração de **System Instructions** e engenharia de prompts voltadas à família de modelos **Google Gemini** (Gemini 2.5 Flash / 1.5 Pro / Flash), utiliadas pelo motor do **Assistente do Jorge**.

---

## 📌 Particularidades do Motor Gemini

O Gemini se destaca pela imensa janela de contexto (de até 1 a 2 milhões de tokens), capacidade nativa multimodal e suporte a **Instruções de Sistema (`systemInstruction`)** separadas do corpo principal das mensagens.

### Diretrizes Chave para o Gemini:
1. **Separação Rígida de Papel**: O `systemInstruction` define quem o modelo é, quais diretrizes ele NUNCA pode quebrar e qual o formato de saída esperado (ex: Markdown + JSON). O corpo da mensagem traz os dados mutáveis (tags XML com contexto e mensagem do usuário).
2. **Clareza de Tarefa Única ou Encadeada**: Prompts de sistema no Gemini funcionam melhor quando organizados com seções bem demarcadas (ex: `PAPEL`, `DIRETRIZES`, `FORMATO DE SAÍDA`, `EXEMPLOS`).
3. **Controle de Respostas JSON / Saídas Estruturadas**: O Gemini responde excepcionalmente bem a instruções que exigem blocos de código JSON explicitamente tipados (como no caso dos nossas Janelas Interativas / Action Cards).

---

## 📚 Fontes e Referências Oficiais de Pesquisa

* **Google AI Studio - System Instructions Guide**:  
  [https://ai.google.dev/gemini-api/docs/system-instructions](https://ai.google.dev/gemini-api/docs/system-instructions)  
  *Guia oficial sobre como configurar a instrução de sistema global para governar o comportamento do Gemini.*

* **Google Gemini Prompting Strategies**:  
  [https://ai.google.dev/gemini-api/docs/prompting-strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)  
  *Estratégias recomendadas pela equipe do Google para otimizar precisão, raciocínio lógico e formatação de saídas.*

* **Gemini Developer Documentation**:  
  [https://ai.google.dev/docs](https://ai.google.dev/docs)  
  *Documentação geral das APIs, parâmetros de temperatura, top_p e limites de tokens.*

---

## ⚡ Boas Práticas de Otimização no Assistente do Jorge

* **Evitar Redundância Verbosa**: Embora o Gemini suporte contextos massivos, instruções de sistema limpas e sumarizadas evitam dispersão e reduzem o tempo total de geração (latência de resposta na extensão).
* **Definição Clara de Fallbacks**: Quando os dados da página ou documentos anexados não forem suficientes para validar uma regra, instrua expressamente o modelo a declarar a ausência de dados em vez de alucinar informações.
* **Uso de Formato Markdown Consistente**: O renderizador do Sidepanel aceita tabelas, blocos de código e alertas em Markdown. O `System Prompt` da Skill deve exigir essas estruturas visualmente ricas.
