# Arquitetura da Life Clinic Digital Platform

## Visão Geral
Este documento descreve a arquitetura da Life Clinic Digital Platform, projetada para processar transações financeiras com segurança e em grande escala. A arquitetura aproveita tecnologias nativas da nuvem, incluindo serviços da AWS, Kubernetes e Crossplane para gerenciamento de infraestrutura.

## Componentes da Arquitetura

### 1. Camada de Infraestrutura
- **VPC**: Uma Virtual Private Cloud (VPC) é provisionada para isolar o aplicativo e seus recursos.
- **Sub-redes**: A VPC inclui sub-redes públicas e privadas para aumentar a segurança e gerenciar o tráfego de forma eficaz.
- **EKS**: O Amazon Elastic Kubernetes Service (EKS) é usado para orquestrar os microsserviços, proporcionando escalabilidade e gerenciamento de aplicativos em contêineres.
- **RDS PostgreSQL**: Uma instância do RDS PostgreSQL Multi-AZ é utilizada para alta disponibilidade e persistência de dados.
- **ElastiCache Redis**: O Redis é empregado para gerenciamento de cache e sessões, melhorando o desempenho dos dados acessados com frequência.
- **Application Load Balancer**: Um ALB é configurado para distribuir o tráfego de entrada entre os microsserviços.
- **Route 53**: O AWS Route 53 é usado para gerenciamento de DNS, garantindo acesso confiável aos serviços.
- **Secrets Manager**: O AWS Secrets Manager é integrado para gerenciamento seguro de informações sensíveis, como credenciais de banco de dados.

### 2. Camada de Aplicação
- **Serviço de API de Transação**: 
  - Implementado em [linguagem escolhida, por exemplo, Python com FastAPI].
  - Expõe endpoints para criação e recuperação de transações.
  - Utiliza PostgreSQL para armazenamento de dados e Redis para cache.
  
- **Serviço de Notificações**: 
  - Implementado em [linguagem escolhida, por exemplo, Node.js com Express].
  - Gerencia notificações relacionadas a transações e recupera notificações específicas do usuário.
  - Compartilha a mesma instância do PostgreSQL, mas opera em um esquema separado.

### 3. Comunicação
- **Descoberta de Serviços**: A descoberta de serviços nativa do Kubernetes é utilizada para comunicação entre microsserviços.
- **Controlador de Ingress**: Um recurso de Ingress é configurado com terminação SSL/TLS para proteger o tráfego para os serviços.
- **Webhooks**: A API de Transação envia webhooks para o Serviço de Notificações após a criação da transação.

### 4. Observabilidade e Monitoramento
- **Prometheus e Grafana**: Essas ferramentas são configuradas para coleta e visualização de métricas, permitindo o monitoramento em tempo real do desempenho do aplicativo.
- **Logging**: Uma pilha ELK ou Fluentd é implementada para agregação e análise de logs.
- **Métricas Personalizadas**: Métricas específicas do domínio financeiro, como taxas de transação e latências de notificação, são coletadas e monitoradas.

### 5. Segurança
- **Políticas de Rede**: As NetworkPolicies do Kubernetes são configuradas para restringir o tráfego entre os serviços, aumentando a segurança.
- **RBAC**: O Controle de Acesso Baseado em Funções (RBAC) é implementado para gerenciar permissões para diferentes componentes do aplicativo.
- **HTTPS**: Todas as comunicações são protegidas por HTTPS para proteger os dados em trânsito.

## Diagrama
Consulte o diagrama da arquitetura localizado em `drawio/architecture.xml` para uma representação visual da arquitetura do sistema.

## Conclusão
Esta arquitetura é projetada para atender aos requisitos de escalabilidade, segurança e desempenho de uma plataforma de saúde moderna. Ao aproveitar os serviços da AWS, Kubernetes e Crossplane, a solução é robusta e flexível, permitindo melhorias futuras e escalonamento conforme necessário.