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
Backlog Priorizado
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

### Módulo 3: Cronograma, Capacidade e Alocação Assistidos

#### **Projeto:** [Conecta Cargas - Scheduling Assistant](module-3)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Scheduling Prompt** - Estruturação de contexto para planejamento de cronograma
- **Análise What-If** - Simulação de cenários futuros para antecipar riscos

**Conceitos abordados:**
- **Mapeamento Preditivo de Dependências:** Classificação de dependências em três grupos - técnicas (funcionalidade depende da conclusão de outra), de recursos (mesmo profissional especializado) e externas (fornecedores, aquisições, aprovações regulatórias). A IA analisa o conteúdo das User Stories para identificar dependências não documentadas.
- **Overcommitment:** Planejamento que compromete 100% da capacidade da equipe, sem margem para imprevistos (defeitos, incidentes, reuniões, suporte, férias). A prática leva a atalhos, débito técnico e perda de qualidade.
- **Capacidade Nominal vs. Capacidade Real:** Uso de fator de utilização (ex: 65% da capacidade nominal disponível para novas funcionalidades) para reservar tempo para atividades inevitáveis do cotidiano (suporte, correções, revisões, refinamentos).
- **Análise What-If:** Simulação de cenários (ex: férias de desenvolvedor, atraso de fornecedor, antecipação de módulo) para recalcular datas, identificar impactos em cascata e evidenciar trade-offs antes da execução.
- **Enabler Tasks:** Tarefas habilitadoras identificadas automaticamente pela IA para iniciar processos de aquisição ou preparação de infraestrutura antes que se tornem bloqueios (ex: compra de sensores IoT).
- **Decomposição de Dependências:** Nem toda dependência bloqueia integralmente uma funcionalidade. A IA identifica oportunidades de entregar versões incrementais que geram valor imediato enquanto componentes restantes continuam em desenvolvimento.
- **Caminho Crítico:** Sequência de atividades cujo atraso impacta diretamente a data final de entrega. A IA recalcula automaticamente sempre que ocorrem alterações no projeto.

**Aplicação prática:**
No contexto da Conecta Cargas, a equipe possui capacidade nominal de 35 Story Points por sprint, com fator de utilização de 65% (aproximadamente 22 pontos efetivos). O cronograma considera dependências como a necessidade de sensores IoT (prazo de 60 dias), que bloqueiam funcionalidades como manutenção preditiva e monitoramento de temperatura. A IA distribui as funcionalidades ao longo de 6 sprints (12 semanas), antecipando os alertas de velocidade (sem dependência de hardware) e utilizando sprints intermediárias para preparar infraestrutura, contratos de API e simuladores para os sensores. A funcionalidade de manutenção preditiva é identificada como inviável no MVP, pois mesmo após a chegada do hardware, o algoritmo necessita de 30 dias de dados históricos para treinamento. O cronograma propõe como alternativa o uso de alertas de velocidade como indicador indireto de desgaste operacional.

**Arquitetura:**
```
Backlog Priorizado + Dependências + Contexto da Equipe
    ↓
Scheduling Prompt (LLM + Temperatura Baixa)
    ├─ Contexto: Capacidade da equipe (especializações, férias, feriados)
    ├─ Contexto: Fator de utilização (65% disponível para novas funcionalidades)
    ├─ Contexto: Dependências (técnicas, recursos, externas)
    ├─ Contexto: Restrições estratégicas (MVP em 12 semanas, demo na Sprint 3)
    ├─ Cálculo: Capacidade por sprint (22 pts normal / 18 pts com feriado)
    ├─ Análise: Mapeamento preditivo de dependências (grafo textual)
    └─ Geração: Cronograma adaptativo + Estratégias de contorno
    ↓
Cronograma Executável + Análise What-If (Pronto para Estimativas)
```
