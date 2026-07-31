# ESPECIFICAÇÃO DE VALIDAÇÃO: TELA DE AUTENTICAÇÃO E CADASTRO DO USUÁRIO

## 1. Mapeamento da Interface (Fonte: manual_do_usuario.md - Seções 4.1 e 5)
- **Menu/Ambiente**: Acesso público e inicial ao Sistema Gestaopublicagov.br.
- **Ambientes e URLs**:
  - Produção: `https://smeg.economia.gov.br`
  - Treinamento: `https://modulos-hom.plataformamaisbrasil.gov.br`
- **Elementos da Tela de Acesso**:
  - Botão principal: "Entrar com gov.br".
  - Redirecionamento obrigatório para autenticação gov.br (CPF e Senha).
- **Elementos da Tela de Cadastro do Usuário**:
  - Formulário com campos de seleção.
  - Campo "Módulo": opção obrigatória `Gestaopublicagov.br`.
  - Botão de ação: "Cadastrar".
  - Tela de autorização de uso de dados pessoais (LGPD).

## 2. Regras de Negócio e Funcionais (Fonte: GUIA IMGG.md - Seção 2.2; modelo_de_governanca.md - Diretrizes de Acesso e Responsabilidade)
- O cadastro e acesso são individuais por CPF vinculado ao sistema gov.br, garantindo rastreabilidade e accountability.
- Perfis disponíveis no cadastro de usuário:
  - Presidente do Comitê de Aplicação (exige vinculação à organização).
  - Membro do Comitê de Aplicação.
  - Coordenador de Rede de Parcerias (Federal, Estadual ou Municipal).
- **Regra de Liberação de Acesso**: O cadastro efetuado fica pendente de ativação/aprovação no sistema. A ativação depende do Presidente do Comitê (para membros da mesma instituição) ou do Coordenador de Rede de Parcerias responsável pelo âmbito de atuação.

## 3. Embasamento Legal e Normativo (Fonte: Portaria SEGES/MGI nº 7.383/2023 - Art. 6º e 7º; modelo_de_governanca.md - Princípios de Integridade)
- Art. 6º: Obrigatoriedade de cadastro dos agentes públicos e representantes de órgãos/entidades recebedoras ou repassadoras de transferências da União.
- Art. 7º: O cadastramento dos membros é condição necessária para constituir o Comitê de Aplicação formalmente perante a Rede de Parcerias.
- **Modelo de Governança**: Atendimento aos princípios de transparência, integridade e responsabilização no acesso às ferramentas de gestão pública.
