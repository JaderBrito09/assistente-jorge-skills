# 🧠 Engenharia de Prompts e Arquitetura de Agentes

Este documento cobre os conceitos teóricos de **Engenharia de Prompts**, **Arquitetura de Agentes Reutilizáveis** e a especificação de **Action Cards Interativos (JSON)** para o ecossistema de habilidades do **Assistente do Jorge**.

---

## 🏗️ Padrões de Engenharia de Agentes Modulares

O projeto adota uma arquitetura inspirada em padrões modernos de ecossistemas de agentes (como Anthropic Skills, Fabric de Daniel Miessler e OpenAI GPTs):

1. **Modularidade (Single Responsibility Principle)**: Cada habilidade contida em `skills/{slug}/` lida com um domínio ou tarefa bem especificada (ex: Auditoria de Compliance, Análise de Código, Consulta Geral).
2. **Separação entre Lógica e Conhecimento**:
   * `SKILL.md`: Contém a instrução de orquestração e comportamento (Lógica).
   * `references/`: Contém regras de negócio, tabelas e normas imutáveis (Conhecimento).
   * `templates/`: Contém moldes de relatórios e estruturas de formulários (Apresentação/Interação).

---

## 🎛️ Especificação de Action Cards Interativos (`interactive_prompt`)

As habilidades do Assistente do Jorge podem pausar a análise e exibir janelas clicáveis (Action Cards) no Sidepanel da extensão, permitindo ao usuário tomar decisões ou fornecer dados antes que a IA continue.

### Esquema JSON do Action Card:

O `System Prompt` da Skill deve instruir a IA a emitir o bloco de código a seguir quando uma ação interativa for requerida:

```json
{
  "type": "interactive_prompt",
  "title": "Pergunta ou Título da Tomada de Decisão",
  "options": [
    {
      "label": "Rótulo visível no Botão 1",
      "value": "Texto enviado como resposta do usuário ao clicar",
      "badge": "Destaque Visual (Opcional, ex: Recomendado)"
    },
    {
      "label": "Rótulo visível no Botão 2",
      "value": "Texto de resposta alternativa"
    }
  ]
}
```

---

## 📚 Fontes e Referências Oficiais de Pesquisa

* **Fabric Project (Daniel Miessler)**:  
  [https://github.com/danielmiessler/fabric](https://github.com/danielmiessler/fabric)  
  *Referência de arquitetura modular de prompts baseados em tarefas ("patterns") focados em utilidade e legibilidade.*

* **Learn Prompting - Prompt Engineering Guide**:  
  [https://learnprompting.org/](https://learnprompting.org/)  
  *Curso aberto cobrindo técnicas de zero-shot, few-shot, chain-of-thought, agentes e prompts estruturados em JSON.*

* **OpenAI Cookbook - Structured Outputs & JSON Mode**:  
  [https://github.com/openai/openai-cookbook](https://github.com/openai/openai-cookbook)  
  *Guias e padrões de como induzir LLMs a gerarem esquemas JSON confiáveis sem erros de sintaxe.*

* **W3C / ARIA & UI Components Best Practices**:  
  *Recomendações de design de interação amigável para Action Cards no Sidepanel de extensões.*
