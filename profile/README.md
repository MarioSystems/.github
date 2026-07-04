# MarioSystems

Sistemas de backend, aplicações focadas em segurança e arquiteturas de software escaláveis.

---

## Sobre

MarioSystems é uma organização pessoal de engenharia de software focada em:

* Desenvolvimento Backend
* Sistemas orientados à segurança
* Autenticação e autorização
* Arquiteturas escaláveis
* Análise de segurança auxiliada por IA
* Conceitos de DevOps e infraestrutura

O objetivo destes projetos é simular ambientes corporativos do mundo real enquanto aprimoro minhas habilidades de engenharia de software, arquitetura e infraestrutura.

---

# Projetos Principais

## 🔐 Auth Gateway

Gateway de autenticação e autorização de nível corporativo desenvolvido com NestJS.

### Funcionalidades

* Autenticação JWT e Refresh Tokens
* Controle de Acesso Baseado em Funções (RBAC) e Guards de rota seguros
* Arquitetura Hexagonal (Ports and Adapters)
* Fluxo de testes com TDD Estrito + BDD
* Validação de requisições e limitação de taxa (Rate Limiting)
* Arquitetura modular e ambiente conteinerizado com Docker

### Stack

* NestJS
* TypeScript
* PostgreSQL
* Prisma
* Redis
* Docker

---

## 🚀 Notification Platform

Plataforma escalável de notificações multi-canal projetada em torno de uma arquitetura orientada a eventos.

### Funcionalidades

* Notificações por Email, SMS e Push
* Arquitetura Orientada a Eventos (EDA)
* Entrega At-Least-Once e Idempotência
* Mecanismos de Retry com Exponential Backoff
* Design de Consistência Eventual
* Processamento de filas e serviços Worker
* Logs, monitoramento e comunicação baseada em eventos

### Stack

* NestJS
* RabbitMQ
* PostgreSQL
* Redis
* Docker

---

## 🛡️ AI Security Analyzer

Sistema auxiliado por IA para análise de eventos de segurança e detecção de atividades suspeitas.

### Funcionalidades

* Classificação de ameaças e pontuação de risco (Risk Scoring)
* Análise de comportamento de login e correlação de eventos
* Recomendações geradas por IA (integração com a API da OpenAI)
* Programação Defensiva (validação estrita de esquemas com Zod)
* Padrões de Circuit Breaker e Fallback para requisições de LLM
* Desenvolvimento Orientado à Observabilidade (ODD)
* Logs de auditoria e alertas de segurança

### Stack

* NestJS
* OpenAI API
* PostgreSQL
* Redis
* Docker

---

## 🏛️ IAM Security System

Plataforma de gerenciamento de identidade e acesso (IAM) focada em auditoria e segurança corporativa.

### Funcionalidades

* Controle de acesso e gerenciamento de permissões (Roles)
* Fluxo de testes com TDD Estrito + BDD
* Trilhas de auditoria (Audit Trails) e logs de atividade
* Monitoramento de requisições e validação de segurança via Middleware
* Gerenciamento de autenticação

### Stack

* Django
* Django REST Framework
* PostgreSQL
* Redis
* Docker

---

# 🛠️ Metodologias de Desenvolvimento & Arquitetura

Aplicação de metodologias e padrões de engenharia corporativos em todos os projetos para garantir confiabilidade, segurança e escalabilidade.

## 1. No Ecossistema Geral (O que usar em todos)

* **DDD (Domain-Driven Design) & Clean Architecture:** Forte separação de conceitos. A lógica de negócios principal (Domínio/Casos de Uso) é estritamente isolada de detalhes de infraestrutura e frameworks (como NestJS/Django, Prisma, PostgreSQL, RabbitMQ) utilizando o padrão Ports & Adapters (Arquitetura Hexagonal).
* **TDD (Test-Driven Development) Pragmático:** O desenvolvimento é guiado pela escrita de testes unitários primeiramente para as regras de negócios críticas e casos de uso (Domain/Use Cases), complementado por testes de integração tradicionais para rotas e controladores.

## 2. Abordagem Específica por Projeto

### 🔐 Auth Gateway & 🏛️ IAM Security System
* **Metodologia:** TDD Estrito + BDD (Behavior-Driven Development)
* **Objetivo:** Determinismo absoluto e tolerância zero a regressões de comportamento.
* **Na Prática:** Testes de cenários de acesso baseados em comportamento (ex: *“Dado que um usuário possui a role 'Admin', quando ele tenta acessar a rota restrita X, então o acesso deve ser permitido”*) utilizando a sintaxe descritiva do BDD, além de 100% de cobertura de testes em componentes críticos como validadores de tokens, guards e auxiliares de criptografia.

### 🚀 Notification Platform
* **Metodologia:** EDA (Event-Driven Architecture) & Padrões de Resiliência
* **Objetivo:** Concorrência, processamento assíncrono e alta tolerância a falhas.
* **Na Prática:** Design voltado à **Consistência Eventual** com filas de mensagens (RabbitMQ). Implementação de **Idempotência** (garantindo que uma notificação não seja duplicada) e **Retry com Exponential Backoff** para lidar com timeouts ou falhas temporárias das APIs de provedores externos.

### 🛡️ AI Security Analyzer
* **Metodologia:** Programação Defensiva & Observability-Driven Development (ODD)
* **Objetivo:** Confiabilidade na ingestão de logs e resiliência diante de instabilidades dos modelos de IA externos.
* **Na Prática:** Validação estrita de payloads de entrada usando Zod, padrões de **Circuit Breaker** para lidar com indisponibilidade ou lentidão da API da OpenAI (com estratégias de fallback), e foco massivo em logs estruturados e métricas (OpenTelemetry, Prometheus, Grafana) para monitoramento em produção.

## 📊 Resumo Estruturado

| Projeto | Padrão Arquitetural | Metodologia de Desenvolvimento | Foco Técnico Principal |
| :--- | :--- | :--- | :--- |
| **Auth Gateway / IAM** | Arquitetura Hexagonal / Clean | TDD + BDD | Segurança estrita, Immutability, RBAC/ABAC |
| **Notification Platform** | Event-Driven Architecture (EDA) | Padrões de Resiliência (Idempotência, Retry) | Filas assíncronas (RabbitMQ), concorrência, retentativas |
| **AI Security Analyzer** | Pipe and Filter / Em Camadas | Observability-Driven Development (ODD) | Ingestão de logs, rate-limiting, resiliência contra falhas de API |

> [!TIP]
> **Dica de Ouro para Entrevistas:**
> Ao apresentar esses projetos, evite apenas citar ferramentas (ex: *"Usei NestJS"*). Em vez disso, explique suas decisões arquiteturais:
> *"Usei NestJS aplicando **Arquitetura Hexagonal** para isolar a regra de negócio do framework, garantindo que o **Auth Gateway** possa trocar o Prisma por qualquer outro ORM sem tocar nas regras de autenticação, tudo coberto por testes via **TDD**."*

---

# ⚙️ Princípios de Engenharia

Os projetos dentro da MarioSystems são projetados com foco em:

* Clean Architecture
* Arquitetura Hexagonal
* Princípios SOLID
* Padrões de Backend Escaláveis
* Boas Práticas de Segurança
* Design Orientado a Eventos (EDA)
* Conteinerização (Docker)
* Observabilidade
* Manutenibilidade

---

# 📚 Foco de Aprendizado Atual

* Arquitetura de Software
* Engenharia de Backend
* Segurança da Informação
* Integração de Inteligência Artificial
* Práticas de DevOps
* Infraestrutura e Monitoramento
* Sistemas Distribuídos

---

# 🔗 Objetivos da Organização

A MarioSystems foi criada para:

* Construir sistemas de backend reais
* Praticar o desenvolvimento de software corporativo
* Explorar arquiteturas escaláveis
* Desenvolver aplicações focadas em segurança
* Aprimorar habilidades de DevOps e infraestrutura
* Criar um portfólio robusto de engenharia de software

---

# 📌 Status

🛠️ Em desenvolvimento ativo
