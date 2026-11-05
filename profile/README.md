# MarioSystems

**Ecossistema de engenharia de software focado em Backend, Segurança e Arquiteturas Escaláveis.**

A MarioSystems é uma organização pessoal de engenharia de software dedicada à construção de sistemas backend que simulam cenários e desafios encontrados em ambientes corporativos.

O ecossistema reúne quatro projetos especializados, desenvolvidos com responsabilidades próprias e preparados para evoluir de maneira independente, mantendo contratos de integração entre os serviços.

O objetivo é aprofundar conhecimentos em engenharia de software, arquitetura, segurança da informação, sistemas distribuídos, infraestrutura e DevOps, construindo soluções que possam ser demonstradas e testadas na prática.

---

## 🎯 Objetivos

- Desenvolver sistemas backend com arquitetura bem definida.
- Aprofundar conhecimentos em autenticação, autorização e segurança.
- Trabalhar com sistemas distribuídos e processamento assíncrono.
- Aplicar padrões de resiliência e confiabilidade.
- Desenvolver soluções de análise de segurança auxiliadas por IA.
- Praticar infraestrutura, conteinerização, CI/CD e observabilidade.
- Construir um portfólio técnico demonstrável, documentado e testável.

---

# 🏗️ Arquitetura do Ecossistema

A MarioSystems será composta por quatro sistemas independentes, cada um responsável por um domínio específico.

| Sistema | Responsabilidade principal |
|---|---|
| Auth Gateway | Autenticação, emissão e validação de tokens e proteção de acesso. |
| IAM Security System | Gestão de identidades, papéis, permissões e auditoria. |
| Notification Platform | Processamento e entrega assíncrona de notificações. |
| AI Security Analyzer | Análise de eventos, identificação de comportamentos suspeitos e avaliação de riscos. |

Os sistemas serão desenvolvidos inicialmente de forma independente. A integração acontecerá por meio de APIs e eventos com contratos bem definidos, evitando acoplamento desnecessário.

## Fluxo conceitual de integração

1. O IAM gerencia identidades, papéis e permissões.
2. O Auth Gateway realiza a autenticação e protege o acesso aos serviços.
3. Eventos relevantes de autenticação e segurança podem ser encaminhados para a Notification Platform e para o AI Security Analyzer.
4. A Notification Platform processa os eventos e realiza os envios de forma assíncrona.
5. O AI Security Analyzer correlaciona eventos, identifica possíveis ameaças e produz avaliações de risco.

*Esse é o fluxo arquitetural planejado. A integração entre os sistemas será implementada progressivamente.*

---

# 🔐 1. Auth Gateway

<sub>Stack: NestJS · TypeScript · PostgreSQL · Prisma · Redis · Docker</sub>

Serviço centralizado de autenticação e proteção de acesso, responsável por gerenciar o fluxo de autenticação e fornecer mecanismos seguros de validação de identidade.

### Responsabilidades

- Cadastro e gerenciamento de usuários.
- Autenticação com email e senha.
- Emissão e validação de JWT.
- Gerenciamento de Refresh Tokens.
- Revogação e renovação de sessões.
- Controle de acesso baseado em funções (RBAC).
- Proteção de rotas utilizando Guards.
- Validação de dados de entrada.
- Rate Limiting.
- Registro de eventos relevantes de autenticação.

### Arquitetura e engenharia

- Arquitetura Hexagonal (Ports and Adapters).
- Separação entre domínio, aplicação e infraestrutura.
- Princípios SOLID.
- TDD para regras críticas.
- BDD para especificação de comportamentos.
- Testes unitários, de integração e ponta a ponta.
- Conteinerização com Docker.

### Objetivo técnico

Construir um serviço de autenticação seguro, modular e reutilizável, capaz de atender diferentes aplicações por meio de contratos HTTP bem definidos.

### Status

- [x] Setup inicial do NestJS.
- [x] Configuração inicial do banco de dados.
- [x] Modelagem inicial de dados.
- [x] Estrutura inicial do módulo de usuários.
- [ ] Implementação dos fluxos de autenticação.
- [ ] JWT e Refresh Tokens.
- [ ] RBAC e Guards.
- [ ] Redis e gerenciamento de sessões.
- [ ] Testes automatizados.
- [ ] Rate Limiting e proteções adicionais.
- [ ] Documentação e integração com os demais serviços.

---

# 🏛️ 2. IAM Security System

<sub>Stack: Django · Django REST Framework · PostgreSQL · Redis · Docker</sub>

Sistema de gerenciamento de identidades e acessos (Identity and Access Management), responsável pela administração de usuários, papéis, permissões e registros de auditoria.

### Responsabilidades

- Gerenciamento de identidades.
- Cadastro e administração de usuários.
- Gerenciamento de papéis (Roles).
- Definição e associação de permissões.
- Controle de acesso baseado em papéis (RBAC).
- Histórico de alterações e atividades.
- Trilhas de auditoria (Audit Trails).
- Registro de operações administrativas.
- Middleware para validações e controles de segurança.

### Arquitetura e engenharia

- Separação entre domínio, serviços e infraestrutura.
- Princípios SOLID.
- Organização modular com Django REST Framework.
- TDD para regras de autorização e segurança.
- BDD para cenários de acesso.
- Testes unitários e de integração.
- Auditoria de operações sensíveis.

### Objetivo técnico

Construir uma plataforma de governança de identidade e acesso, permitindo administrar políticas de autorização e rastrear operações realizadas no ecossistema.

### Integração planejada

O IAM será responsável pela administração das identidades e políticas de acesso. O Auth Gateway será responsável pelos fluxos de autenticação e proteção dos recursos.

A comunicação entre eles deverá acontecer por contratos definidos, sem compartilhar diretamente suas estruturas internas ou bancos de dados.

### Status

- [ ] Estrutura inicial do projeto.
- [ ] Modelagem de identidades, papéis e permissões.
- [ ] Implementação de RBAC.
- [ ] Serviços de autorização.
- [ ] Trilhas de auditoria.
- [ ] Middleware de segurança.
- [ ] Testes automatizados.
- [ ] Integração com o Auth Gateway.

---

# 🚀 3. Notification Platform

<sub>Stack: NestJS · TypeScript · RabbitMQ · PostgreSQL · Redis · Docker</sub>

Plataforma de notificações multicanal desenvolvida com arquitetura orientada a eventos (Event-Driven Architecture), responsável pelo processamento assíncrono e entrega confiável de mensagens.

### Responsabilidades

- Gerenciamento de notificações.
- Envio de notificações por Email.
- Estrutura preparada para integração com SMS e Push.
- Recebimento e publicação de eventos.
- Processamento assíncrono com RabbitMQ.
- Gerenciamento de filas e Workers.
- Controle de tentativas de entrega.
- Tratamento de falhas e retentativas.
- Histórico e acompanhamento do status das notificações.

### Arquitetura e engenharia

- Event-Driven Architecture (EDA).
- Processamento assíncrono.
- Entrega com semântica At-Least-Once.
- Idempotência para evitar processamento duplicado.
- Retry com Exponential Backoff.
- Dead Letter Queue (DLQ).
- Consistência eventual.
- Logs estruturados e monitoramento.
- Testes de integração e concorrência.

### Objetivo técnico

Desenvolver uma plataforma capaz de processar grandes volumes de notificações de maneira assíncrona, resiliente e desacoplada dos serviços que produzem os eventos.

### Integração planejada

A plataforma poderá receber eventos do Auth Gateway, IAM e AI Security Analyzer, permitindo enviar notificações relacionadas a autenticações, alterações administrativas e alertas de segurança.

### Status

- [ ] Estrutura inicial do projeto.
- [ ] Modelagem de notificações e entregas.
- [ ] Configuração do RabbitMQ.
- [ ] Implementação de Producers e Consumers.
- [ ] Workers de processamento.
- [ ] Integração com provedor de Email.
- [ ] Idempotência e controle de duplicidade.
- [ ] Retry com Exponential Backoff.
- [ ] Dead Letter Queue.
- [ ] Testes de resiliência e concorrência.
- [ ] Documentação e integração com os demais serviços.

---

# 🛡️ 4. AI Security Analyzer

<sub>Stack: NestJS · TypeScript · OpenAI API · PostgreSQL · Redis · Docker</sub>

Sistema de análise de eventos de segurança auxiliado por inteligência artificial, desenvolvido para identificar comportamentos suspeitos, correlacionar ocorrências e produzir avaliações de risco.

### Responsabilidades

- Ingestão de eventos de segurança.
- Análise de eventos de autenticação.
- Identificação de comportamentos suspeitos.
- Correlação de eventos relacionados.
- Classificação de ameaças.
- Cálculo de pontuação de risco (Risk Scoring).
- Recomendações de segurança auxiliadas por IA.
- Registro de análises e alertas.
- Histórico de eventos e decisões.

### Arquitetura e engenharia

- Arquitetura modular.
- Pipeline de ingestão e processamento de eventos.
- Programação defensiva.
- Validação estrita de dados com Zod.
- Regras determinísticas de detecção.
- Integração com modelos de linguagem por meio da OpenAI API.
- Circuit Breaker e estratégias de Fallback.
- Logs estruturados e trilhas de auditoria.
- Observabilidade com OpenTelemetry, Prometheus e Grafana.

### Objetivo técnico

Construir um sistema capaz de transformar eventos de segurança em informações úteis para identificar riscos e apoiar decisões de proteção.

A IA será utilizada como mecanismo complementar de análise. A detecção básica e o cálculo de risco deverão funcionar por regras determinísticas, mesmo quando o serviço externo de IA estiver indisponível.

### Integração planejada

O sistema poderá consumir eventos de autenticação, autorização e auditoria produzidos pelos outros serviços, permitindo analisar padrões de comportamento e identificar possíveis ameaças.

### Status

- [ ] Estrutura inicial do projeto.
- [ ] Definição do contrato de eventos.
- [ ] Modelagem de eventos de segurança.
- [ ] Pipeline de ingestão.
- [ ] Motor determinístico de detecção.
- [ ] Implementação de Risk Scoring.
- [ ] Integração com a OpenAI API.
- [ ] Circuit Breaker e Fallback.
- [ ] Histórico de análises e alertas.
- [ ] Observabilidade e auditoria.
- [ ] Testes de segurança e resiliência.

---

# 🧰 5. Padrões de Engenharia

Os projetos seguirão princípios e práticas de engenharia adequados às necessidades de cada sistema.

### Arquitetura

- Domain-Driven Design (DDD), quando houver benefício na modelagem do domínio.
- Clean Architecture.
- Arquitetura Hexagonal.
- Ports and Adapters.
- Princípios SOLID.
- Separação de responsabilidades.
- Baixo acoplamento e alta coesão.

### Testes

- TDD aplicado às regras de negócio críticas.
- BDD para especificação de comportamentos.
- Testes unitários.
- Testes de integração.
- Testes end-to-end.
- Testes de segurança.
- Testes de resiliência e concorrência quando aplicáveis.

### Segurança

- Autenticação e autorização.
- Validação e sanitização de entradas.
- Princípio do menor privilégio.
- Proteção contra abuso de requisições.
- Gerenciamento seguro de credenciais e segredos.
- Auditoria de operações sensíveis.
- Tratamento seguro de erros.

### Infraestrutura e DevOps

- Docker e Docker Compose.
- Linux e administração de servidores.
- Nginx e gerenciamento de tráfego.
- CI/CD com GitHub Actions.
- Gerenciamento de variáveis e segredos.
- Logs estruturados.
- Observabilidade.
- Monitoramento com OpenTelemetry, Prometheus e Grafana.

---

# 🌐 6. Infraestrutura do Ecossistema

A infraestrutura será organizada para reduzir custos operacionais e simplificar a administração, sem comprometer a separação lógica dos serviços.

### Estratégia de implantação

- Frontend e console demonstrativo hospedados na Vercel.
- APIs e serviços backend hospedados em infraestrutura cloud.
- Docker para padronização dos ambientes.
- PostgreSQL como banco relacional principal.
- Redis para cache e gerenciamento de dados temporários.
- RabbitMQ para comunicação assíncrona.
- Nginx como proxy reverso.
- GitHub Actions para automação de testes e deploy.

### Compartilhamento de infraestrutura

Sempre que tecnicamente adequado, os serviços poderão compartilhar instâncias de infraestrutura, mantendo isolamento lógico, credenciais, bancos e responsabilidades separados.

O compartilhamento de infraestrutura não significa compartilhamento de domínio ou dependência direta entre os sistemas.

A implantação será progressiva, priorizando baixo custo e facilidade de manutenção.

---

# 🖥️ 7. MarioSystems Console

Será desenvolvido um console central para apresentar e demonstrar os recursos dos projetos.

O console funcionará como ponto de entrada para recrutadores e desenvolvedores interessados em conhecer o ecossistema.

### Módulos planejados

**Identity & Access**
- Cadastro e autenticação de usuários de demonstração.
- Demonstração de papéis e permissões.
- Testes de rotas protegidas.

**Notification Center**
- Disparo de notificações de teste.
- Acompanhamento do processamento.
- Visualização de tentativas e falhas.

**Security Lab**
- Simulação de eventos de autenticação.
- Demonstração de comportamentos suspeitos.
- Visualização de Risk Score.
- Comparação entre análise determinística e análise auxiliada por IA.

**IAM Explorer**
- Visualização de papéis e permissões.
- Demonstração de operações administrativas.
- Consulta de trilhas de auditoria.

**Developer Center**
- Documentação das APIs.
- Swagger/OpenAPI.
- Diagramas arquiteturais.
- Repositórios e tecnologias utilizadas.
- Status dos testes e pipelines.

O ambiente demonstrativo utilizará dados fictícios, permissões limitadas e operações controladas, sem exposição de credenciais ou recursos administrativos reais.

---

# 🗺️ 8. Ordem de Desenvolvimento

A construção do ecossistema seguirá uma sequência progressiva, evitando desenvolver todos os sistemas simultaneamente.

| Etapa | Projeto | Objetivo |
|---|---|---|
| 1 | Auth Gateway | Concluir autenticação, tokens, autorização e segurança. |
| 2 | IAM Security System | Desenvolver governança de identidade, permissões e auditoria. |
| 3 | Notification Platform | Implementar filas, Workers, entrega e resiliência. |
| 4 | AI Security Analyzer | Desenvolver ingestão de eventos, detecção e análise de riscos. |
| 5 | Integração | Estabelecer comunicação entre os quatro sistemas. |
| 6 | Infraestrutura | Consolidar containers, CI/CD, deploy e observabilidade. |
| 7 | MarioSystems Console | Criar a interface demonstrativa centralizada. |
| 8 | Publicação | Disponibilizar documentação, demonstrações e ambiente de testes. |

Cada etapa deverá ter implementação funcional, testes, documentação e critérios de conclusão antes de avançar para a seguinte.

---

# 📊 9. Diretrizes de Qualidade

A qualidade dos projetos será avaliada não apenas pela quantidade de funcionalidades, mas principalmente pela qualidade das decisões de engenharia.

Critérios importantes:

- Código organizado e sustentável.
- Responsabilidades bem delimitadas.
- Testes automatizados confiáveis.
- Segurança desde a concepção.
- Tratamento adequado de falhas.
- Documentação técnica clara.
- Infraestrutura reproduzível.
- Observabilidade dos serviços.
- Integrações com contratos bem definidos.
- Demonstrações funcionais e verificáveis.

As funcionalidades descritas representam objetivos de desenvolvimento, não necessariamente recursos já implementados.

---

# 📚 10. Foco de Aprendizado

A MarioSystems também será utilizada como ambiente de estudo prático nas seguintes áreas:

- Engenharia de Backend.
- Arquitetura de Software.
- Sistemas Distribuídos.
- Segurança da Informação.
- Identidade e Controle de Acesso.
- Mensageria e Processamento Assíncrono.
- Inteligência Artificial aplicada à segurança.
- Banco de Dados e Modelagem.
- DevOps e Infraestrutura.
- Observabilidade e Monitoramento.
- Testes e Qualidade de Software.

A proposta é estudar cada conceito no contexto de um problema real de engenharia, implementando, testando e documentando as decisões tomadas.

---

# 📌 Status Geral

**Em desenvolvimento ativo.**

Atualmente, o Auth Gateway encontra-se na fase inicial de construção, com setup do NestJS, configuração inicial do banco de dados, modelagem e estrutura do módulo de usuários.

Os demais projetos estão em fase de planejamento arquitetural e definição de suas responsabilidades.

A MarioSystems evoluirá progressivamente, priorizando consistência técnica, integração entre sistemas e demonstrações funcionais.

---

**MarioSystems — Engineering Backend. Building Secure and Scalable Systems.**
