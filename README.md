# 🕷️ Multi-Threaded Web Automation & Cloud Integration
## 📖 Visão Geral

Este projeto é uma solução robusta de **RPA (Robotic Process Automation)** desenvolvida em Python. O objetivo principal é automatizar o preenchimento de cadastros complexos em portais web, simulando o comportamento humano de forma massiva e paralela.

O diferencial técnico deste projeto reside na sua capacidade de **evasão de detecção** e **escalabilidade**. Ele utiliza uma arquitetura de *multithreading* para gerenciar múltiplas instâncias de navegadores simultaneamente, cada uma operando sob um contexto de rede (Proxy) e *Fingerprint* (User-Agent) distintos.

Além disso, o sistema foi projetado para operar integrado a uma arquitetura em nuvem (**Azure**), onde uma API centraliza a validação de acesso e integridade dos dados antes da execução local.

## 🏗️ Arquitetura e Fluxo

A solução segue um fluxo linear com validação em nuvem e execução paralela local:

```mermaid
graph TD
    A[Usuário / Input Config] -->|Credenciais| B{Validação Azure API}
    B -- Negado --> X[Encerrar]
    B -- Aprovado --> C[Main Controller]
    C -->|Lê Excel| D[Carregar Proxies & Dados]
    C -->|Loop| E[Gerenciador de Threads]
    
    subgraph "Execução Paralela (Workers)"
    E --> F[Thread 1]
    E --> G[Thread 2]
    E --> H[Thread N...]
    end
    
    F -->|Injeta Extensão Proxy| I[Chrome Instance A]
    G -->|Injeta Extensão Proxy| J[Chrome Instance B]
    
    I -->|Ações Automatizadas| K[Site Alvo]
    J -->|Ações Automatizadas| K
