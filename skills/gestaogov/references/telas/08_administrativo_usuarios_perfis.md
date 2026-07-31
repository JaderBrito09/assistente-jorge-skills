# ESPECIFICAÇÃO DE VALIDAÇÃO: MENU ADMINISTRATIVO (USUÁRIOS E PERFIS)

## 1. Mapeamento da Interface (Fonte: manual_do_usuario.md - Seções 6.3, 6.3.1 e 6.3.2, Figuras 37 a 41)
- **Menu/Ambiente**: `Menu Administrativo`.
- **Acesso por Perfis**: Visível apenas pelos perfis Presidente do Comitê de Aplicação e Coordenadores da Rede de Parcerias (Federal, Estadual e Municipal).
- **Submenu Usuários**:
  - Campo de busca/consulta de usuários cadastrados.
  - Colunas da tabela: `CPF`, `Nome`, `Perfil` e `Ação`.
  - Expansor `+`: Exibe dados detalhados do cadastro do usuário.
  - Ações na coluna `Ação`: Ícones para Ativação / Inativação do cadastro. Usuários inativos recebem sinalização visual destacada.
- **Submenu Perfis do Sistema**:
  - Visível exclusivamente para o perfil Presidente do Comitê de Aplicação.
  - Colunas da tabela: `Nome`, `Módulo`, `Global` (sim/não) e `Ação`.
  - Expansor `+`: Relaciona a lista detalhada de permissões do perfil dentro do sistema.

## 2. Regras de Negócio e Funcionais (Fonte: GUIA IMGG.md - Seção 2.2; modelo_de_governanca.md - Segregação de Funções e Alçadas)
- **Alçadas e Visibilidade da Gestão de Usuários**:
  - **Presidente do Comitê de Aplicação**: Visualiza, ativa e inativa apenas os usuários pertencentes à sua própria instituição/órgão.
  - **Coordenador da Rede de Parcerias (Federal/Estadual/Municipal)**: Visualiza e gerencia os usuários pertencentes aos órgãos dentro de seu respectivo âmbito de atuação regional/federativo.
- A desativação de um usuário revoga imediatamente seu acesso aos formulários de aplicação e monitoramento da instituição.

## 3. Embasamento Legal e Normativo (Fonte: Portaria SEGES/MGI nº 7.383/2023 - Art. 6º e 7º; modelo_de_governanca.md - Controles Internos e Acessos)
- Art. 6º: A governança de acessos e a manutenção do cadastro atualizado dos usuários é responsabilidade compartilhada entre a Secretaria-Executiva da Rede de Parcerias e os dirigentes/presidentes de comitê institucionais.
- **Modelo de Governança**: Aplicação do princípio de segregação de funções e gestão de permissões por alçada de atuação.
