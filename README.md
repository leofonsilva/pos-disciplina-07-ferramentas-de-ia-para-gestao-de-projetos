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

### Módulo 08: Governança, Compliance e Qualidade

#### **Projeto:** [Conecta Cargas - Governance as Code](module-08)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Compliance Prompt** - Geração inteligente de checklists de conformidade adaptados ao contexto do projeto
- **Danger.js** - Ferramenta para automação de verificações de conformidade em Pull Requests
- **Governança como Código (Governance as Code)** - Transformação de políticas organizacionais em regras executadas automaticamente no pipeline de integração contínua

**Conceitos abordados:**
- **Governança como Código:** Princípio de descrever regras de conformidade de maneira estruturada e executá-las automaticamente no pipeline sempre que ocorre uma alteração relevante no projeto. A conformidade deixa de ser uma atividade posterior à implementação e passa a fazer parte do processo de desenvolvimento.
- **Checklist de Conformidade Adaptativo:** O modelo recebe informações sobre o contexto específico da aplicação (domínio de negócio, requisitos regulatórios, arquitetura, maturidade da equipe, políticas internas) e produz checklists personalizados, divididos em três categorias:
  - **Bloqueadores de Deploy:** Condições que impedem a liberação da versão se não atendidas (ex: conformidade com LGPD, aprovações formais, comunicação explícita de limitações técnicas).
  - **Verificações Operacionais:** Boas práticas recomendadas (ex: plano de comunicação, monitoramento pós-deploy, plano de reversão, gestão de segredos).
  - **Registros Obrigatórios para Auditoria:** Documentação que preserva rastreabilidade (ex: base legal para tratamento de dados, registro de bugs conhecidos, identificadores de commit e versões).
- **Trilha de Auditoria:** Conexão entre requisito, decisão, implementação e implantação - cada alteração deve possuir uma origem claramente identificável, permitindo rastrear por que uma funcionalidade foi implementada, qual Pull Request a realizou e quem autorizou sua implantação.
- **Danger.js:** Executado durante a análise de Pull Requests, permite escrever regras em JavaScript para verificar automaticamente diversos aspectos de conformidade (obrigatoriedade de vínculo com Jira, aprovações obrigatórias para componentes críticos, cobertura de testes, tamanho de Pull Requests).
- **Separação entre Lógica e Configuração:** Princípio da engenharia de software aplicado à governança - o comportamento do mecanismo permanece estável, enquanto parâmetros específicos do projeto (arquivos críticos, limites) podem ser ajustados sem alterar o código das validações.
- **Contextualização de Riscos:** A IA produz verificações específicas para o cenário apresentado (ex: devido ao bug S4-10 que afeta 43 veículos, o modelo exige que o sistema informe explicitamente essa condição no painel para evitar falsos negativos).

**Aplicação prática:**
Durante o primeiro deploy em produção do módulo de alertas de velocidade da Conecta Cargas, o Compliance Prompt recebe informações sobre o contexto (monitoramento de GPS em tempo real, dados de localização de motoristas, componentes envolvidos, stakeholders responsáveis, histórico do bug S4-10). O modelo gera um checklist com bloqueadores como conformidade com LGPD (documentação da base legal para tratamento de dados), aprovações formais (operacional, técnica, jurídica), e uma verificação específica: como 43 veículos permanecem sem suporte, o sistema deve informar explicitamente essa condição. O checklist também inclui recomendações operacionais (plano de comunicação, monitoramento pós-deploy, plano de rollback) e registros para auditoria. Simultaneamente, o modelo gera um arquivo Danger.js com regras como exigência de identificador do Jira nos Pull Requests, aprovação dupla para alterações em componentes de GPS, alertas para redução de cobertura de testes e identificação de PRs excessivamente grandes.

**Arquitetura:**
```
Contexto do Deploy + Políticas Organizacionais + Histórico do Projeto
    ↓
Compliance Prompt (LLM)
    ├─ Bloqueadores de Deploy (LGPD, aprovações, comunicação de limitações)
    ├─ Verificações Operacionais (comunicação, monitoramento, rollback, segredos)
    └─ Registros para Auditoria (base legal, bugs conhecidos, versões)
    ↓
Checklist de Conformidade
    ↓
(Paralelo) Geração de Regras Danger.js
    ├─ Obrigatoriedade: ID do Jira nos Pull Requests
    ├─ Aprovação: 2 aprovações para componentes GPS
    ├─ Alerta: Redução de cobertura de testes
    └─ Alerta: Pull Requests excessivamente grandes
    ↓
Pipeline de CI/CD com Governança Automatizada
```

### Módulo 09: Automação em Jira/Asana/Trello/Notion/Slack

#### **Projeto:** [Conecta Cargas - Ecosystem Bot](module-09)

**Tecnologias utilizadas:**
- **LLM (Large Language Model)** - Motor com raciocínio estruturado
- **Natural Language to Workflow Parser** - Transformação de mensagens em linguagem natural em artefatos estruturados para ferramentas de gestão
- **Webhooks** - Mecanismo de integração entre ferramentas para eventos e notificações

**Conceitos abordados:**
- **Ferramentas Conectadas vs. Ferramentas Integradas:** Ferramentas conectadas compartilham eventos (webhooks tradicionais), enquanto ferramentas integradas compartilham contexto - a informação é interpretada antes da ação, identificando natureza, domínio do problema e decisões automáticas sobre artefatos, plataformas e parâmetros.
- **Natural Language to Workflow:** Princípio de permitir que o usuário se comunique em linguagem natural enquanto a IA transforma automaticamente essa comunicação em objetos estruturados compatíveis com as ferramentas de gestão (Jira, Slack, Notion). A mensagem deixa de ser apenas texto e passa a representar uma fonte estruturada de conhecimento.
- **Parser Semântico:** Extração de estrutura semântica (identificação de entidades, intenções), classificação de prioridade (alta/média/baixa), reconhecimento de componentes mencionados, identificação de equipe responsável, e decisão sobre ações necessárias (criar card, abrir incidente, notificar gestor).
- **Classificação de Mensagens:** O parser distingue entre bugs (prioridade alta, investigação), features (nova funcionalidade, planejamento), tasks (atividades operacionais) e perguntas (sem criação automática de cards até confirmação).
- **Action Required Flag:** Campo obrigatório para mensagens contendo alternativas de decisão (ex: adiar deploy ou remover funcionalidade). Impede que o bot crie automaticamente cards operacionais para problemas que dependem de decisão gerencial estratégica.
- **Recuperação de Contexto (RAG):** Para mensagens em threads (ex: respostas curtas como "pode fazer isso"), o bot recupera automaticamente as últimas mensagens da conversa para compreender o contexto completo antes do parsing.
- **Trilha de Auditoria:** Registro estruturado de cada card criado automaticamente (data, canal de origem, identificador da mensagem, versão do prompt, resultado completo do modelo), estabelecendo rastreabilidade sobre como determinada atividade surgiu.
- **Glossário de Jargões:** Manutenção de um glossário estruturado com termos internos da equipe (ex: P0, Sprint End, stand-up) incorporado automaticamente ao contexto do parser para melhor compreensão.
- **Sincronização Jira ↔ Slack:** Propagação de alterações de status do Jira para canais do Slack, com separação de canais de comunicação e canais de acompanhamento automatizado para evitar fadiga de alertas.

**Aplicação prática:**
Na Conecta Cargas, três cenários demonstram o Natural Language to Workflow Parser:
1. **Bug:** Mensagem "os alertas de velocidade pararam de chegar em Uberlândia, preciso investigar" - parser identifica bug, prioridade alta, componente de GPS, responsável vazio (pois a responsabilidade não foi explicitamente assumida), e gera descrição rica com pontos de investigação (rastreadores, MQTT, AWS Lambda, Firebase).
2. **Feature com Prazo:** Mensagem "Carlos pediu antecipação do módulo de manutenção preditiva para antes do final do mês devido à revisão anual" - parser identifica nova funcionalidade prioritária, solicitante Carlos, prazo final do mês, mas responsável vazio (expressão "alguém pode pegar isso?" não assume responsabilidade).
3. **Decisão Crítica:** Mensagem "deploy de sexta bloqueado porque módulo depende de hardware não entregue" com alternativas "adiar ou remover funcionalidade" - parser identifica criticidade máxima, mas ao analisar o resultado, percebe-se que o campo Action Required está vazio; o prompt é ajustado para preencher este campo automaticamente quando mensagens contêm alternativas de decisão, devolvendo a situação ao gestor para decisão manual.

**Arquitetura:**
```
Mensagem em Linguagem Natural (Slack/Teams)
    ↓
Natural Language to Workflow Parser (LLM + Contexto)
    ├─ Recuperação: Contexto da Thread (mensagens anteriores)
    ├─ Classificação: Bug vs. Feature vs. Task vs. Pergunta
    ├─ Extração: Prioridade, Componente, Responsável, Prazo
    ├─ Decisão: Action Required? (sim/não)
    ├─ Geração: Objeto Estruturado (JSON para Jira)
    └─ (Opcional) Glossário de Jargões para melhor compreensão
    ↓
(Curadoria: Confirmação antes da criação do card)
    ↓
Criação de Card no Jira + Notificação no Slack
    ↓
Sincronização Jira → Slack (alterações de status propagadas)
```
