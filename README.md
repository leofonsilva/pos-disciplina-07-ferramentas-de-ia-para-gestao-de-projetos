# Pós Disciplina 07 - Ferramentas de IA para Gestão de Projetos

## Introdução
Pendente...

## Módulos

### Módulo 01: Planejamento e Escopo com IA (Requirements Copilot)

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

### Módulo 02: Priorização Inteligente de Backlog

#### **Projeto:** [Conecta Cargas - Backlog Scorer](module-02)

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

### Módulo 03: Cronograma, Capacidade e Alocação Assistidos

#### **Projeto:** [Conecta Cargas - Scheduling Assistant](module-03)

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

### Módulo 04: Estimativas e Previsões

#### **Projeto:** [Conecta Cargas - Probability Forecast](module-04)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Probability Forecast Prompt** - Geração de previsões probabilísticas a partir de estimativas individuais
- **Estimativa de Três Pontos** - Técnica baseada em cenários otimista, mais provável e pessimista
- **Distribuição PERT** - Cálculo de estimativa ponderada que atribui maior peso ao cenário mais provável
- **Simulação de Monte Carlo** - Técnica estatística que executa milhares de simulações para gerar distribuições de probabilidade

**Conceitos abordados:**
- **Planning Fallacy (Falácia do Planejamento):** Tendência cognitiva humana a subestimar tempo, custo e complexidade de atividades futuras. Mesmo equipes experientes continuam produzindo estimativas otimistas, independentemente da competência técnica.
- **Estimativa Pontual vs. Probabilística:** Substituição de datas fixas por intervalos de confiança (percentis P50, P85, P95) que comunicam explicitamente o risco associado ao cronograma.
- **Percentis de Confiança:**
  - **P50 (Mediana):** 50% das simulações terminam até esta data. Risco significativo de atraso.
  - **P85:** 85% das simulações terminam até esta data. Nível de confiança recomendado para comunicação com clientes.
  - **P95:** 95% das simulações terminam até esta data. Postura conservadora para projetos críticos.
- **Restrições Determinísticas vs. Variabilidade:** A simulação de Monte Carlo representa apenas a incerteza incorporada ao modelo. Riscos externos (ex: atraso de fornecedor) tratados como datas fixas precisam ser gerenciados separadamente.
- **SLO (Service Level Objective) Aplicado a Projetos:** Uso de percentis de probabilidade para comunicar confiança em entregas, similar ao uso de percentis de latência em engenharia de confiabilidade.
- **Adaptação de Linguagem por Audiência:** Comunicação de resultados estatísticos de maneiras diferentes para equipe técnica (variâncias, distribuições PERT), gestores de produto (níveis de confiança, fatores de influência) e executivos (decisões de negócio, investimentos necessários).

**Aplicação prática:**
No contexto da Conecta Cargas, cada User Story recebe três cenários de estimativa (ex: alerta de velocidade com 2 semanas otimista, 3 semanas mais provável, 5 semanas pessimista). A IA calcula automaticamente a distribuição PERT de cada história, incluindo variância e desvio padrão. A simulação de Monte Carlo (10.000 execuções) sobre o backlog do MVP revela que o P50 é de aproximadamente 12,5 semanas, enquanto o P85 é de 13,1 semanas e o P95 de 13,4 semanas. A pequena diferença entre os percentis não indica baixa incerteza, mas a presença de uma restrição dominante: o lead time do fornecedor de hardware (60 dias) tratado como data fixa, que domina a variabilidade do cronograma. Funcionalidades com maior incerteza técnica (ex: score de comportamento do motorista com integração a acelerômetros desconhecidos) são identificadas como candidatas a spikes técnicos antes da implementação.

**Arquitetura:**
```
Cronograma + Estimativas de Três Pontos + Restrições Externas
    ↓
Probability Forecast Prompt (LLM + Temperatura Baixa)
    ├─ Entrada: User Stories com cenários (Otimista, Mais Provável, Pessimista)
    ├─ Cálculo: Distribuição PERT por história (Média Ponderada, Variância, Desvio)
    ├─ Simulação: Monte Carlo (milhares de execuções do cronograma)
    ├─ Geração: Percentis de confiança (P50, P85, P95)
    └─ Adaptação: Relatórios para diferentes audiências
    ↓
Previsões Probabilísticas + Riscos Identificados (Pronto para Monitoramento)
```

### Módulo 05: Riscos e Mitigações com AIOps de Projeto

#### **Projeto:** [Conecta Cargas - Risk Monitor](module-05)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Risk Monitor** - Monitoramento contínuo de indicadores de fluxo para identificação de anomalias
- **AIOps (Artificial Intelligence for IT Operations)** - Princípios de monitoramento automatizado aplicados à gestão de projetos

**Conceitos abordados:**
- **AIOps Aplicado a Projetos:** Transporte da abordagem de monitoramento de infraestrutura (logs, métricas, eventos) para o gerenciamento de projetos, utilizando dados do Jira (backlog, estados de User Stories, transições, bugs, históricos de alterações) como fonte contínua de informações sobre a saúde do projeto.
- **Lead Time:** Tempo total entre a entrada de uma história no backlog e sua conclusão. Aumento consistente indica que o volume de trabalho em andamento cresce mais rápido que a capacidade de entrega.
- **Cycle Time:** Tempo efetivo de desenvolvimento (desde o início do trabalho até a conclusão). Comparação com Lead Time permite identificar se o gargalo está na implementação (Cycle Time alto) ou em etapas anteriores/esperas (Lead Time alto, Cycle Time estável).
- **Taxa de Bugs por Sprint:** Comparação entre defeitos abertos e resolvidos. Crescimento contínuo do saldo de bugs indica que a dívida de qualidade está aumentando, consumindo capacidade que deveria ser dedicada a novas funcionalidades.
- **Frequência de Alterações em User Stories:** Acompanhamento de mudanças em descrições, critérios de aceite ou escopo após o início da sprint. Alta frequência indica **scope creep** e requisitos insuficientemente refinados.
- **Work in Progress (WIP):** Excesso de trabalho em progresso aumenta filas internas e reduz previsibilidade.
- **Cockpit de Riscos:** Dashboard estruturado por componentes (fluxo/eficiência, qualidade do produto, dependências externas, escopo/previsibilidade) que consolida indicadores, tendências e contexto operacional para classificar a severidade dos riscos.
- **Plano de Mitigação:** Estratégias proporcionais à anomalia encontrada, como **Stop Starting, Start Finishing** (interromper entrada de novos itens e focar na conclusão dos já iniciados), redução de limites de WIP, fortalecimento da **Definition of Ready** para funcionalidades com dependências externas, e estabelecimento de critérios objetivos para medir o sucesso da mitigação.

**Aplicação prática:**
No contexto da Conecta Cargas, durante a quinta sprint, o Risk Monitor analisa dados históricos das quatro primeiras sprints. O Lead Time cresceu de 6 para 11 dias, enquanto o Cycle Time permaneceu estável, indicando gargalo em esperas (dependências externas), não em perda de produtividade. O saldo de bugs cresce continuamente (novos bugs surgem mais rápido que sua correção). Funcionalidades como score de comportamento do motorista permanecem bloqueadas por dependência de hardware. O cockpit classifica o risco como elevado e recomenda ações como reduzir WIP, fortalecer Definition of Ready (histórias só entram na sprint com dependências resolvidas) e iniciar planos de contingência para a apresentação executiva, que ocorrerá na mesma sprint prevista para a chegada do hardware, sem margem para testes e validação.

**Arquitetura:**
```
Dados Históricos do Jira (4 sprints)
    ↓
Risk Monitor (LLM + Indicadores de Fluxo)
    ├─ Métrica: Lead Time (6 → 11 dias) vs. Cycle Time (estável)
    ├─ Métrica: Taxa de Bugs (abertos > resolvidos)
    ├─ Métrica: Frequência de Alterações (scope creep)
    ├─ Métrica: Work in Progress (excesso)
    ├─ Análise: Padrões de degradação (tendências)
    ├─ Classificação: Cockpit de Riscos por componente
    └─ Geração: Plano de Mitigação (Stop Starting, Start Finishing, Definition of Ready)
    ↓
Riscos Identificados + Ações de Mitigação (Pronto para Governança)
```

### Módulo 06: Reuniões Turbinadas (Notas, AIs, Follow-ups)

#### **Projeto:** [Conecta Cargas - Meeting Digest](module-06)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Meeting Digest** - Automação de documentação de reuniões com síntese semântica
- **Síntese Semântica** - Compreensão do significado das falas, identificando compromissos, decisões, riscos e questões não resolvidas

**Conceitos abordados:**
- **Síntese Semântica:** Diferente da transcrição literal que registra palavras exatas, a síntese compreende o significado das falas, identificando intenções, compromissos, decisões e contextos implícitos na conversa.
- **Classificação Semântica:** Quatro categorias de informação extraídas automaticamente da reunião:
  - **Compromissos de Ação:** Atividades assumidas por participantes com responsável, urgência e prazo.
  - **Decisões:** Acordos estabelecidos que alteram formalmente o comportamento do projeto (ex: exclusão de funcionalidade, adoção de procedimento temporário).
  - **Riscos e Impedimentos:** Fatores que bloqueiam o andamento do projeto (hardware indisponível, problemas de acesso, dependências).
  - **Perguntas em Aberto:** Questões que permaneceram sem resposta, com indicação de quem deverá fornecer esclarecimentos.
- **Rastreabilidade de Decisões:** Registro do contexto que justificou cada escolha, preservando o histórico de mudanças de escopo e permitindo auditoria futura.
- **Payload Estruturado (JSON):** Artefato gerado automaticamente para integração com ferramentas como Jira, contendo campos como título, responsável, prioridade, prazo e descrição detalhada, pronto para consumo por APIs e webhooks.
- **Protocolo de Auditoria da Ata:** Cinco etapas de curadoria antes da distribuição - leitura da tabela de ações em voz alta, revisão de responsáveis indefinidos, validação de decisões críticas com participantes, atribuição de responsáveis para perguntas em aberto, e verificação de informações implícitas não capturadas.
- **Curadoria de Transcrição:** Revisão rápida da transcrição antes do processamento para corrigir nomes de pessoas, sistemas, componentes técnicos e termos específicos do domínio, evitando propagação de erros.

**Aplicação prática:**
Durante uma Sprint Review da Conecta Cargas, o Meeting Digest processa a transcrição da reunião. A IA identifica que o mesmo assunto (acelerômetros para cálculo do comportamento do motorista) evolui ao longo da conversa: inicialmente como problema técnico, depois como necessidade de cotação, culminando na decisão formal de iniciar a aquisição. O modelo consolida essa evolução em uma linha narrativa única, preservando o raciocínio coletivo. O resumo executivo destaca funcionalidades concluídas, itens bloqueados e mudanças de escopo (retorno do S05 por necessidade de apresentação executiva, criação do S06 solicitado pelo RH). A tabela de ações inclui responsáveis (Marcos estima S05, Ana Lima detalha requisitos) e a identificação de perguntas em aberto (prazo do fornecedor de hardware). O JSON gerado permite integração automática com Jira, mas apresenta lacunas como o prazo implícito de Ana Lima (não preenchido no campo estruturado) e uma decisão técnica (ajuste de timeout) não capturada, que exige curadoria manual.

**Arquitetura:**
```
Áudio da Reunião
    ↓
Transcrição (Voz para Texto)
    ↓
Meeting Digest (LLM + Síntese Semântica)
    ├─ Classificação: Compromissos de Ação (responsável, prazo, urgência)
    ├─ Classificação: Decisões (acordos com justificativa e contexto)
    ├─ Classificação: Riscos e Impedimentos (bloqueadores identificados)
    ├─ Classificação: Perguntas em Aberto (dúvidas não resolvidas)
    ├─ Geração: Resumo Executivo da Reunião
    └─ Geração: Payload JSON (pronto para Jira/APIs)
    ↓
Curadoria Manual (Protocolo de Auditoria)
    ↓
Artefatos Estruturados (Ata, Ações, Decisões, Payload)
```

### Módulo 07: Status Reports e Executive Summaries

#### **Projeto:** [Conecta Cargas - Status Report Adaptativo](module-07)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Status Report Prompt** - Geração automática de relatórios adaptados por audiência
- **Status Report Adaptativo** - Personalização de linguagem, profundidade e foco para diferentes públicos

**Conceitos abordados:**
- **Status Report Adaptativo:** Princípio de adaptar o mesmo conjunto de informações para diferentes audiências (técnica, gerencial, executiva), preservando consistência dos dados mas alterando linguagem, nível de detalhe e foco da análise.
- **Comunicação por Perfil de Audiência:**
  - **Time Técnico:** Indicadores operacionais (Velocity, Lead Time, Cycle Time, Story Points, débito técnico, bloqueios). Linguagem técnica, formato de listas estruturadas. Foco em orientar o trabalho da próxima sprint.
  - **Gestores de Projeto/Produto:** Percentual de conclusão, aderência ao cronograma, capacidade da equipe, riscos classificados por probabilidade e impacto, decisões pendentes. Linguagem gerencial com resumo executivo e tabelas de riscos.
  - **Executivos e Clientes:** Retorno sobre investimento, impacto operacional, previsibilidade da entrega, cumprimento de objetivos estratégicos, marcos do projeto. Linguagem de negócio, formato conciso (máximo 1 página). A premissa: quanto maior o nível hierárquico, menor o tempo disponível para leitura.
- **Divergências de Interpretação:** Diferentes classificações de status (ex: vermelho vs. amarelo) podem ser igualmente defensáveis a partir dos mesmos dados, dependendo do contexto estratégico. A curadoria deve compreender o significado que cada classificação comunica aos stakeholders.
- **Curadoria do Status Report:** Verificações antes da distribuição - validar números (arredondamentos incorretos), adequar linguagem ao público (evitar termos técnicos no executivo), limitar decisões a 2-3 itens críticos, ajustar tom excessivamente negativo, e garantir que todo risco tenha ação correspondente e responsável.
- **Gestão de Portfólio:** Aplicação do mesmo Status Report Prompt a cada projeto individualmente, consolidando os relatórios executivos em um Executive Summary de portfólio que identifica tendências comuns, iniciativas críticas e prioridades para a alta gestão.

**Aplicação prática:**
No fechamento da Sprint 4 da Conecta Cargas, os dados brutos são: velocidade de 22 Story Points, Lead Time de 10 dias, 11 defeitos registrados (6 resolvidos), bloqueio de hardware, queda na previsibilidade. O Status Report Adaptativo gera três versões:
- **Time Técnico:** Foco no aumento do Lead Time, saldo de defeitos e excesso de WIP. Recomenda limitar itens simultâneos por desenvolvedor e priorizar correção do defeito crítico que afeta veículos antigos.
- **Gestor do Projeto:** Classifica o projeto em status amarelo, comunica risco moderado de atraso no MVP e apresenta a principal decisão necessária: aprovar aquisição de hardware ou remover funcionalidade de score de comportamento do escopo.
- **Diretoria:** Informa que a funcionalidade principal está operacional, confirma a demonstração para as próximas semanas e comunica risco moderado no fornecimento de equipamentos, com ações em andamento para resolução.

**Arquitetura:**
```
Dados da Sprint + Indicadores de Fluxo + Decisões Registradas
    ↓
Status Report Prompt (LLM + Temperatura Baixa)
    ├─ Versão Técnica: Velocidade, Lead Time, Cycle Time, WIP, Defeitos, Ações para a Sprint
    ├─ Versão Gerencial: Status (Verde/Amarelo/Vermelho), Riscos, Decisões Pendentes, Aderência ao Cronograma
    └─ Versão Executiva: Valor Entregue, Riscos Estratégicos, Marcos, Decisões de Alto Nível
    ↓
Curadoria (Validação de Números, Linguagem, Tom e Decisões)
    ↓
Relatórios Adaptados + (Opcional) Executive Summary de Portfólio
```
