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

### Módulo 2: Priorização Inteligente de Backlog

#### **Projeto:** [Conecta Cargas - Backlog Scorer](module-2)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Backlog Scorer** - Aplicação de frameworks de priorização com suporte da IA

**Conceitos abordados:**
- **MoSCoW:** Framework de classificação em quatro categorias (Must Have, Should Have, Could Have, Won't Have) para filtrar o backlog antes da priorização detalhada.
- **RICE Score:** Método de priorização baseado em quatro dimensões - Reach (alcance), Impact (impacto), Confidence (confiança) e Effort (esforço). Funcionalidades com alto impacto, grande alcance, alta confiança e baixo esforço recebem pontuações mais altas.
- **WSJF (Weighted Shortest Job First):** Framework que prioriza com base no custo do atraso (Cost of Delay) dividido pelo esforço. Composto por três dimensões: valor de negócio, criticidade temporal e redução de riscos/criação de oportunidades.
- **HIPPO (Highest Paid Person's Opinion):** Conceito que descreve decisões baseadas em hierarquia em vez de dados, evitado pela adoção de frameworks objetivos.
- **Flags de Atenção:** Sinalizações geradas pelo Backlog Scorer para identificar riscos, dependências e inconsistências que precisam ser tratadas antes do desenvolvimento, como dependências de hardware, metas sem dados históricos suficientes ou falta de evidência de contribuição para objetivos estratégicos.
- **Curadoria do Ranking:** Verificação manual de Reach (com dados reais), dependências técnicas não capturadas, revisão de funcionalidades com alta confiança e análise de todas as flags geradas antes da aprovação.
- **Calibração:** Substituição de estimativas genéricas por evidências de dados reais (analytics, pesquisas com usuários, indicadores financeiros). Em projetos em cold start, utiliza-se benchmarks de domínio e referências públicas (Gartner, Forrester).

**Aplicação prática:**
A partir do backlog produzido no módulo anterior, o Backlog Scorer aplica os frameworks de priorização no contexto da Conecta Cargas. O processo começa com a filtragem MoSCoW, seguida pela aplicação simultânea de RICE e WSJF. O modelo recebe o contexto estratégico do projeto (OKRs, restrições operacionais, dependências externas) para produzir estimativas mais consistentes. Diferentes frameworks produzem rankings distintos para o mesmo backlog - enquanto o RICE identifica onde o investimento produz maior retorno, o WSJF responde quais iniciativas não podem esperar. O resultado inclui flags de atenção (ex: dependência de hardware para manutenção preditiva, falta de dados históricos para meta de precisão de 80%) e recomendações para aquisição antecipada de equipamentos antes da alocação em sprints.

**Arquitetura:**
```
Backlog Priorizado (Módulo 1)
    ↓
Backlog Scorer (LLM + Contexto Estratégico)
    ├─ Filtro: MoSCoW (Must/Should/Could/Won't)
    ├─ Cálculo: RICE Score (Reach, Impact, Confidence, Effort)
    ├─ Cálculo: WSJF (Cost of Delay / Effort)
    ├─ Geração: Flags de Atenção e Riscos
    └─ Saída: Ranking Priorizado + Recomendações
    ↓
Backlog Priorizado + Flags (Pronto para Cronograma)
```
