---
name: publicacao-e-versionamento
description: Automatiza o commit, auditoria e versionamento (SemVer e Git Tags) exclusivo para o repositório assistente-jorge-skills, garantindo conformidade com o GUIA_DE_SKILLS e atualização do manifesto skills.json.
---

# Publicação e Versionamento — Catálogo de Skills (assistente-jorge-skills)

Esta skill gerencia a auditoria, commits de desenvolvimento e o lançamento oficial de novas versões (Releases) **exclusivamente para o repositório de skills** (`assistente-jorge-skills` / `skill_extensao`).

---

## 📂 Escopo e Repositório Alvo

- **Repositório:** `https://github.com/JaderBrito09/assistente-jorge-skills`
- **Diretório Local:** Workspace `skill_extensao`
- **Conteúdo Gerenciado:**
  - Catálogo de Habilidades (`skills/<nome-da-skill>/SKILL.md`, `references/`, `scripts/`, `resources/`, `examples/`).
  - Manifesto de Registro (`skills.json`).
  - Documentação e Guias (`docs/GUIA_DE_SKILLS.md`, `docs/ARQUITETURA_INTEGRACAO.md`, `README.md`).
  - Configurações internas do agente (`.gemini/skills/`).

---

## 🎯 Tipos de Ação

1. **🔨 Commit Diário de Desenvolvimento (Work in Progress)**:
   - Salva o progresso diário de criação ou edição de skills.
   - Verifica sintaxe básica de arquivos editados.
   - Realiza commit com padrão Conventional Commits e envia para `origin main`.

2. **🚀 Lançamento Oficial de Versão do Catálogo (Release)**:
   - Audita a conformidade das skills com as diretrizes do `GUIA_DE_SKILLS.md`.
   - Garante que todas as novas skills estejam devidamente registradas ou estruturadas.
   - Pergunta o incremento SemVer (`patch`, `minor` ou `major`).
   - Atualiza documentos de versão e gera a **Git Tag anotada** de release.
   - Realiza o push dos commits e das tags para o GitHub (`assistente-jorge-skills`).

---

## 🚀 Fluxo de Execução Interativo (Passo 0)

Se a ação desejada não for informada na chamada, pergunte ao usuário:

> **O que você deseja realizar no repositório `assistente-jorge-skills` neste momento?**
> 1. **🔨 Commit Diário de Desenvolvimento**: Salvar alterações e progresso mantendo a versão atual.
> 2. **🚀 Lançar Nova Versão do Catálogo de Skills (Release)**: Auditar conformidade com `GUIA_DE_SKILLS.md`, incrementar SemVer e gerar Git Tag.

---

### 🔨 Fluxo A: Commit Diário de Desenvolvimento

1. **Verificação de Arquivos e Segurança**:
   - Garantir que arquivos temporários ou credenciais sensíveis não estejam staged.
   - Verificar integridade do manifesto `skills.json`.

2. **Comitar e Enviar**:
   ```bash
   git add .
   git commit -m "<tipo>(<escopo>): <descrição das alterações>"
   git push origin main
   ```
   *Exemplo de mensagem:* `feat(skills): adiciona nova habilidade de gestaogov` ou `docs(guias): atualiza GUIA_DE_SKILLS.md`

---

### 🚀 Fluxo B: Lançamento Oficial de Versão (Release do Catálogo)

1. **Auditoria de Conformidade de Skills**:
   - Verificar se os arquivos `SKILL.md` possuem frontmatter YAML válido (`name` e `description`).
   - Garantir que nomes de skills estejam em `kebab-case`.
   - Verificar se não há dados sensíveis ou URLs hardcoded específicas.
   - Confirmar se o arquivo `skills.json` reflete a estrutura atual.

2. **Pergunta Interativa de Versão SemVer**:
   - Selecionar o incremento:
     - **Patch** (ex: `v1.0.1` -> correções em skills existentes).
     - **Minor** (ex: `v1.1.0` -> adição de novas skills ou guias).
     - **Major** (ex: `v2.0.0` -> refatoração arquitetural completa do catálogo).

3. **Comitar, Taggear e Publicar**:
   ```bash
   git add .
   git commit -m "chore(release): bump catalog version to vX.Y.Z"
   git tag -a vX.Y.Z -m "Release vX.Y.Z do catálogo de skills"
   git push origin main
   git push origin vX.Y.Z
   ```
