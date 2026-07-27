# Pós Disciplina 07 - Ferramentas de IA para Gestão de Projetos

## Introdução
Pendente...

## Módulos

### Módulo 1: Planejamento e Escopo com IA (Requirements Copilot)

#### **Projeto:** [Conecta Cargas - Requirements Copilot](module-01)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **System Prompt** - Contrato de comportamento para o modelo atuar como analista sênior de requisitos
- **PERT/Three-Point Estimation** - Para identificação de lacunas e incertezas durante a elicitação
- **Gherkin** - Formato para critérios de aceite (`Dado/Quando/Então`)

**Conceitos abordados:**
- **Requirements Copilot:** Uso de IA para automatizar a parte mecânica da engenharia de requisitos, transformando conversas em linguagem natural em artefatos estruturados (User Stories, épicos, features).
- **Curadoria de Requisitos:** A IA produz um rascunho estruturado que deve ser revisado pelo analista, com ênfase na rastreabilidade até a transcrição original para evitar alucinações.
- **Protocolo de Ambiguidade:** A IA identifica lacunas de informação em vez de inventar respostas, registrando perguntas em aberto para serem validadas com stakeholders.
- **Formato User Story:** Estrutura `"Como [ator específico]..."` em vez de "usuário" genérico.
- **Princípios INVEST:** A IA valida automaticamente se a história é Independente, Negociável, Valiosa, Estimável, Pequena e Testável.
- **Análise de Domínio de Confiança:** A IA gera um mapa de cobertura das conversas, indicando quais áreas do negócio possuem alta ou baixa confiança em informações.

**Aplicação prática:**
A partir da transcrição de uma reunião de *discovery* da empresa de logística Conecta Cargas, a IA estrutura o backlog inicial com User Stories e critérios de aceite. O processo vai além de uma simples transcrição, mapeando as incertezas (ambiguidades) e classificando o nível de confiança dos domínios de negócio discutidos, preparando as próximas entrevistas com o cliente para preencher lacunas de informação.

**Arquitetura:**
```
Transcrição de Reunião (Discovery)
    ↓
Requirements Copilot (LLM + System Prompt)
    ├─ Ação: Gerar Mapa de Domínios (Confiança Alta/Média/Baixa)
    ├─ Ação: Identificar Ambiguidades e Perguntas em Aberto
    ├─ Ação: Estruturar Épicos, Features e User Stories (formato INVEST)
    └─ Ação: Validar Critérios de Aceite (Gherkin)
    ↓
Backlog Estruturado + Lista de Pendências (Pronto para Jira/Refinamento)
```