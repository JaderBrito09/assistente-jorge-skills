---
name: arquiteto-de-skills
description: Guiar a elaboração, análise, validação e publicação de habilidades (skills) para o Assistente do Jorge na pasta skills/ e no manifesto skills.json. Trigger quando o usuário pedir para criar uma nova skill, analisar/refinar uma skill existente, validar conformidade com GUIA_DE_SKILLS.md ou atualizar o catálogo skills.json.
---

# 🛠️ Arquiteto de Skills — Assistente do Jorge

Esta habilidade orienta a **concepção, análise, otimização e publicação** de habilidades modulares para o ecossistema do **Assistente do Jorge**.

Ela garante que toda nova skill seja criada respeitando rigorosamente os padrões de arquitetura do Sidepanel, o parser de markdown, a injeção de tags XML e o manifesto [`skills.json`](file:///Users/jader/Meu%20Drive/skill_extensao/skills.json).

---

## 📌 Documentos de Referência Obrigatórios

Ao atuar nesta habilidade, você deve consultar e respeitar as diretrizes presentes na pasta `docs/`:
1. [`GUIA_DE_SKILLS.md`](file:///Users/jader/Meu%20Drive/skill_extensao/docs/GUIA_DE_SKILLS.md): Contrato técnico de especificação de novas habilidades.
2. [`ARQUITETURA_INTEGRACAO.md`](file:///Users/jader/Meu%20Drive/skill_extensao/docs/ARQUITETURA_INTEGRACAO.md): Fluxo de comunicação client-gateway-LLM e parser de marcação.
3. [`META_PROMPTING_E_TAGS_XML.md`](file:///Users/jader/Meu%20Drive/skill_extensao/docs/META_PROMPTING_E_TAGS_XML.md): Boas práticas de escopo semântico e tags XML.
4. [`DIRETRIZES_PROMPTING_GEMINI.md`](file:///Users/jader/Meu%20Drive/skill_extensao/docs/DIRETRIZES_PROMPTING_GEMINI.md): Otimização de prompts para a família Google Gemini.
5. [`ENGENHARIA_PROMPTS_E_ARQUITETURA_AGENTES.md`](file:///Users/jader/Meu%20Drive/skill_extensao/docs/ENGENHARIA_PROMPTS_E_ARQUITETURA_AGENTES.md): Action Cards JSON e padrões de agentes.

---

## 🏗️ Estrutura Obrigatória de uma Habilidade (Skill)

Cada habilidade reside em uma pasta própria dentro de `skills/`:

```text
skills/{slug_da_skill}/
├── SKILL.md              📜 Instruções Principais (Obrigatório)
├── references/           📚 Bases de conhecimento em .md (Opcional)
└── templates/            📑 Moldes de relatórios (.md) ou Action Cards (.json) (Opcional)
```

### 📜 Estrutura do `SKILL.md` (3 Seções Obrigatórias)

O arquivo `SKILL.md` deve conter exatamente estas seções:

```markdown
# Skill: <Nome Amigável da Skill>
**Categoria**: <Geral | Compliance | Governança | Jurídico | etc.>
**Descrição**: <Breve resumo da utilidade da skill>

## Orientação Inicial ao Usuário
<Texto amigável exibido no chat do Sidepanel assim que a skill é selecionada pelo usuário>

## System Prompt
<Instrução de sistema enviada em segundo plano para o Gemini 2.5 Flash>
```

---

## ⚠️ Regras Rígidas para o `System Prompt`

1. **Uso Obrigaório de Tags XML**: O System Prompt deve instruir o Gemini a ler o contexto a partir dos delimitadores XML montados pelo Sidepanel:
   - `<regras_e_referencias>`: Textos da pasta `references/`.
   - `<templates_disponiveis>`: Modelos da pasta `templates/`.
   - `<conteudo_pagina>`: Texto extraído da aba ativa no Chrome.
   - `<documentos_anexados>`: Arquivos carregados pelo usuário.
   - `<mensagem_usuario>`: Comando ou escolha do usuário.

2. **Janelas Interativas / Action Cards (`interactive_prompt`)**:
   Quando a skill exigir decisões ou confirmações do usuário, oriente o modelo a retornar um bloco JSON com o seguinte formato:
   ```json
   {
     "type": "interactive_prompt",
     "title": "Pergunta ao usuário",
     "options": [
       { "label": "Opção 1", "value": "Texto de resposta 1", "badge": "Recomendado" },
       { "label": "Opção 2", "value": "Texto de resposta 2" }
     ]
   }
   ```

3. **Inexistência de Alucinações (Fallbacks Explicitados)**:
   Se uma regra da referência não puder ser validada por falta de dados na página ou anexos, exija que o modelo informe categoricamente: *"Dado ausente para validação segundo a regra X"*.

---

## 🔄 Fluxos de Trabalho da Skill Arquiteta

Ao ser acionada, esta skill pode operar em 3 modos:

### Modo 1: Concepção e Criação de Nova Skill
1. **Entrevista / Coleta de Requisitos**: Pergunta ao usuário sobre a categoria, objetivo, regras de negócio e interações da nova skill.
2. **Geração de Arquivos**:
   - Cria a pasta `skills/{slug}/`.
   - Gera o arquivo `SKILL.md` formatado.
   - Gera arquivos em `references/` e `templates/` se necessário.
3. **Registro no Manifesto**: Adiciona a entrada da nova skill no arquivo [`skills.json`](file:///Users/jader/Meu%20Drive/skill_extensao/skills.json).

### Modo 2: Auditoria e Validação de Skill Existente
1. Lê o `SKILL.md` e a pasta da skill informada.
2. Checa se as 3 seções obrigatórias existem.
3. Verifica a aderência às tags XML e o formato do `interactive_prompt`.
4. Propõe as melhorias ou refatorações necessárias.

### Modo 3: Atualização e Manutenção do Manifesto (`skills.json`)
1. Garante que o `skills.json` contenha o esquema válido:
```json
{
  "id": "SKILL-EXEMPLO-001",
  "slug": "exemplo",
  "name": "Nome da Skill",
  "category": "Categoria",
  "file": "skills/exemplo/SKILL.md",
  "references": ["skills/exemplo/references/ref.md"],
  "templates": ["skills/exemplo/templates/tpl.json"]
}
```
