# Deploy da Life Clinic Digital Platform

Este documento fornece instruções passo a passo para implantar a Plataforma Digital da Life Clinic, incluindo a infraestrutura necessária e os componentes do aplicativo.

## Pré-requisitos

Antes de começar, verifique se você tem o seguinte:

- Conta na AWS com permissões apropriadas para criar recursos.
- `kubectl` instalado e configurado para acessar seu cluster Kubernetes.
- `Crossplane` instalado em seu cluster Kubernetes.
- `Docker` instalado para criar imagens de contêiner.
- `Helm` instalado para gerenciar aplicativos Kubernetes.

## Etapa 1: Configurar o Crossplane

1. **Instalar o Crossplane**: Siga o guia de instalação oficial do Crossplane para configurar o Crossplane em seu cluster Kubernetes.
   
2. **Configurar o Provedor AWS**:
   - Navegue até o diretório `crossplane/providers`.
   - Aplique a configuração do provedor AWS:
     ```
     kubectl apply -f providers/aws-provider.yaml
     ```

3. **Configurar Funções IAM**: Certifique-se de que as funções IAM definidas em sua configuração de provedor tenham as permissões necessárias para gerenciar recursos da AWS.

## Etapa 2: Provisionar Infraestrutura

1. **Criar Definições de Recursos Compostos (XRDs)**:
   - Navegue até o diretório `crossplane/xrds`.
   - Aplique os XRDs:
     kubectl apply -f xrds/life-clinic-platform-xrd.yaml

2. **Criar Composições**:
   - Navegue até o diretório `crossplane/compositions`.
   - Aplique as composições:
     kubectl apply -f compositions/life-clinic-platform-composition.yaml

3. **Provisionar Instâncias**:
   - Navegue até o diretório `crossplane/instances`.
   - Aplique a configuração da instância:
     kubectl apply -f instances/life-clinic-platform-instance.yaml

## Etapa 3: Implantar Aplicativos Kubernetes

1. **Configurar Namespaces**:
   - Navegue até o diretório `k8s/namespaces`.
   - Aplique as configurações de namespace:
     kubectl apply -f namespaces/life-clinic-namespace.yaml

2. **Implantar API de Transações**:
   - Navegue até o diretório `k8s/apps/transaction-api`.
   - Aplique as configurações de implantação e serviço:

     kubectl apply -f deployment.yaml
     kubectl apply -f service.yaml
     kubectl apply -f ingress.yaml

3. **Implantar Serviço de Notificações**:
   - Navegue até o diretório `k8s/apps/notification-service`.
   - Aplique as configurações de implantação e serviço:

     kubectl apply -f deployment.yaml
     kubectl apply -f service.yaml

## Etapa 4: Configurar Monitoramento

1. **Implantar Ferramentas de Monitoramento**:
   - Navegue até o diretório `k8s/monitoring`.
   - Aplique as configurações de monitoramento para Prometheus e Grafana:

     kubectl apply -f prometheus.yaml
     kubectl apply -f grafana.yaml


## Etapa 5: Verificar Implantação

1. **Verificar o Status dos Pods**:
   - Use o seguinte comando para verificar o status dos seus pods:
     kubectl get pods -n life-clinic

2. **Acessar Serviços**:
   - Use a URL do Ingress para acessar a API de Transações e o Serviço de Notificações.

## Etapa 6: Limpar Recursos

Para limpar os recursos criados durante a implantação, execute o script de limpeza:

./scripts/cleanup.sh

## Conclusão

Você implantou com sucesso a Plataforma Digital da Life Clinic. Para mais detalhes sobre solução de problemas e documentação da API, consulte os respectivos documentos no diretório `docs`.