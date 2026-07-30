# 📑 Meta-Prompting e Uso de Tags XML

Este documento reúne diretrizes, guias teóricos e práticas fundamentais sobre **Meta-Prompting** e o **uso estruturado de Tags XML** em System Prompts, com foco na arquitetura de habilidades do **Assistente do Jorge**.

---

## 💡 O que é Meta-Prompting?

**Meta-Prompting** é a técnica de projetar um prompt de sistema cujo propósito principal é atuar como um *compilador, gerador ou auditor de outros prompts*. Em vez de executar uma tarefa de usuário final diretamente, o Meta-Prompt instrui o modelo de linguagem (LLM) a:
1. Entrevistar o usuário ou analisar os requisitos do domínio.
2. Formular o **System Prompt** ideal, definindo papel, limites de escopo e diretrizes comportamentais.
3. Estruturar arquivos auxiliares (bases de referência em `.md` e templates/action cards em `.json`).

---

## 🏷️ Por que utilizar Tags XML em Prompts?

Tags XML (como `<regras_e_referencias>`, `<conteudo_pagina>`, `<documentos_anexados>`, `<mensagem_usuario>`) são altamente recomendadas por provedores de ponta (como Anthropic e Google) para delimitar o escopo das informações enviadas ao modelo.

### Principais Benefícios:
* **Clareza de Limite de Escopo (Context Scoping)**: O LLM diferencia com precisão matemática o que é instrução de controle, o que é regra de referência e o que é o dado bruto trazido da página web ou documento anexado.
* **Prevenção contra Prompt Injection**: Ao encapsular dados externos ou input do usuário em tags como `<conteudo_pagina>` e `<mensagem_usuario>`, o modelo é instruído a tratar esse conteúdo como *dado a ser analisado* e não como *instruções de comando do sistema*.
* **Citação e Auditoria**: Permite instruir a IA a citar a origem exata da informação (ex: *"Segundo a regra X encontrada na tag `<regras_e_referencias>`..."*).

---

## 📚 Fontes e Referências de Pesquisa

* **Anthropic Prompt Engineering - Use XML Tags**:  
  [https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags)  
  *Explica como delimitar partes complexas do prompt com tags para evitar confusões e melhorar a acurácia de respostas.*

* **Anthropic Metaprompt System Guide**:  
  [https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/metaprompt](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/metaprompt)  
  *Apresenta o modelo teórico e o template de Meta-Prompt usado para gerar System Prompts robustos baseados em tarefas.*

* **Anthropic Helper Tools - Metaprompt Generator**:  
  [https://github.com/anthropics/anthropic-cookbook/tree/main/misc/metaprompt.ipynb](https://github.com/anthropics/anthropic-cookbook/tree/main/misc/metaprompt.ipynb)  
  *Notebook com a implementação prática da Anthropic para geração de prompts via meta-instrução.*

---

## 🎯 Padrão de Injeção de Tags XML no Assistente do Jorge

No SidePanel da extensão Chrome, o payload enviado ao Gemini consolida o contexto sob as seguintes tags padrão:

```xml
<regras_e_referencias>
[Conteúdo dos arquivos Markdown baixados da pasta references/]
</regras_e_referencias>

<templates_disponiveis>
[Modelos de relatórios (.md) ou estruturas JSON de formulários baixados de templates/]
</templates_disponiveis>

<conteudo_pagina url="https://exemplo.com">
[Texto limpo extraído do DOM da página web ativa]
</conteudo_pagina>

<documentos_anexados>
[Texto ou conteúdo extraído dos arquivos carregados pelo usuário]
</documentos_anexados>

<mensagem_usuario>
[Pergunta atual ou resposta selecionada pelo usuário]
</mensagem_usuario>
```

### Exemplo de Instrução no `System Prompt`:
```text
Sua análise DEVE se fundamentar estritamente nos dados contidos nas tags XML:
1. Valide o conteúdo da tag <conteudo_pagina> contra as regras da tag <regras_e_referencias>.
2. Se houver discrepância, utilize a estrutura do modelo na tag <templates_disponiveis> para reportar os erros.
3. Responda diretamente ao comando do usuário presente na tag <mensagem_usuario>.
```
