# 🏥 Life Clinic Digital Platform

Este repositório contém a infraestrutura e o código de aplicação para a Life Clinic, uma clínica digital voltada ao acolhimento de casais com dificuldade para engravidar. A solução integra ginecologistas e especialistas em reprodução assistida, promovendo acessibilidade, jornada integrada e inteligência artificial para recomendações clínicas — tudo provisionado em cloud ☁️ (AWS 🟧) com Kubernetes ☸️ e Crossplane 🛩️.

## 📁 Estrutura do Projeto

- **crossplane/** 🛩️: Configurações para provisionamento de recursos AWS via Crossplane
  - **providers/** 🟧: Configuração do provider AWS
  - **compositions/** 🏗️: Composições para stack de infraestrutura (VPC, EKS, RDS, ElastiCache, etc.)
  - **xrds/** 🧩: CompositeResourceDefinitions para a plataforma Life Clinic
  - **instances/** 🧪: Instâncias das composições

- **k8s/** ☸️: Manifests Kubernetes para deploy dos serviços
  - **namespaces/** 🏷️: Namespaces para isolar componentes
    - `lifeclinic-platform`, `appointment-api`, `patient-notification-service`, `medical-records-api`, `ai-recommendation-service`, `monitoring`, `security`
  - **apps/** 🧬: Microserviços da plataforma
    - **appointment-api/** 📅: API de agendamento de consultas
    - **patient-notification-service/** 🔔: Serviço de notificações para pacientes
    - **medical-records-api/** 🗂️: API de prontuário digital
    - **ai-recommendation-service/** 🤖: Serviço de IA para recomendações clínicas
  - **monitoring/** 📊: Prometheus, Grafana
  - **security/** 🛡️: NetworkPolicies, RBAC

- **docker/** 🐳: Dockerfiles dos microserviços
  - **appointment-api/** 📅
  - **patient-notification-service/** 🔔
  - **medical-records-api/** 🗂️
  - **ai-recommendation-service/** 🤖

- **docs/** 📚: Documentação
  - **ARCHITECTURE.md** 🏗️: Arquitetura e diagramas
  - **DEPLOYMENT.md** 🚀: Deploy da infra e apps
  - **API.md** 🔌: Documentação dos endpoints
  - **TROUBLESHOOTING.md** 🩺: Troubleshooting

- **scripts/** ⚡: Scripts de automação
  - **deploy.sh** 🚀
  - **test.sh** 🧪
  - **cleanup.sh** 🧹

- **drawio/** 🖼️: Diagramas de arquitetura (draw.io)

## 🛠️ Instruções de Setup

1. **Pré-requisitos**:
   - Docker 🐳, kubectl ☸️, Crossplane CLI 🛩️, AWS CLI 🟧

2. **Clone o Repositório**:
   ```bash
   git clone https://github.com/rlsouza-cyber/life-clinic-digital-platform.git
   cd life-clinic-digital-platform
   ```

3. **Configure as credenciais AWS** 🟧.

4. **Provisionamento da Infraestrutura**:
   ```bash
   ./scripts/deploy.sh
   ```

5. **Deploy dos Microserviços**:
   - Aplique os manifests em `k8s/apps/` ☸️.

6. **Acesso aos Serviços**:
   - Use o endpoint do Load Balancer 🌐 para acessar as APIs de agendamento, prontuário, notificações e recomendações.

## 🏗️ Decisões Arquiteturais

- **Microserviços** 🧬: Escalabilidade, resiliência e manutenção facilitada
- **Crossplane** 🛩️: Provisionamento declarativo e seguro na AWS
- **Kubernetes** ☸️: Orquestração de containers e automação de deploy
- **IA** 🤖: Serviço dedicado para recomendações clínicas inteligentes
- **Segurança** 🛡️: RBAC, NetworkPolicies e IAM com privilégio mínimo
- **Observabilidade** 📊: Monitoramento com Prometheus e Grafana

## 🎯 Escopo da POC

- Diagrama de contexto e infraestrutura (drawio/architecture.xml) 🖼️
- MVP com IA (ai-recommendation-service) 🤖
- Infraestrutura cloud (AWS via Crossplane) ☁️🟧🛩️
- Demonstração dos endpoints principais (agendamento, prontuário, notificações, recomendação) 🔌

## 🎉 Conclusão

Esta POC demonstra a viabilidade técnica, escalabilidade e alinhamento estratégico de uma clínica digital inteligente, pronta para evoluir e atender demandas reais do setor de saúde reprodutiva. Para detalhes, consulte a documentação em `docs/` 📚.
