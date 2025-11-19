# API da Life Clinic Digital Platform

## Visão Geral
Este documento fornece uma visão geral dos endpoints da API expostos pelos microserviços de Agendamento e Serviço de Notificações na plataforma Life Clinic. Cada endpoint inclui o método HTTP, URL, parâmetros de solicitação e formato de resposta.

## Serviço de Agendamento

### URL Base
`http://appointment-api.lifeclinic.svc.cluster.local:8080`

### Endpoints

#### 1. Criar Agendamento
- **Método:** POST
- **URL:** `/agendamentos`
- **Corpo da Solicitação:**
  ```json
  {
    "data_hora": "string",
    "especialidade": "string",
    "descricao": "string"
  }
  ```
- **Resposta:**
  - **201 Criado**
    ```json
    {
      "id": "string",
      "data_hora": "string",
      "especialidade": "string",
      "descricao": "string",
      "status": "string",
      "created_at": "string"
    }
    ```
  - **400 Solicitação Inválida**
    ```json
    {
      "erro": "string"
    }
    ```

#### 2. Obter Agendamento por ID
- **Método:** GET
- **URL:** `/agendamentos/{id}`
- **Resposta:**
  - **200 OK**
    ```json
    {
      "id": "string",
      "data_hora": "string",
      "especialidade": "string",
      "descricao": "string",
      "status": "string",
      "created_at": "string"
    }
    ```
  - **404 Não Encontrado**
    ```json
    {
      "erro": "string"
    }
    ```

#### 3. Verificar Saúde
- **Método:** GET
- **URL:** `/health`
- **Resposta:**
  - **200 OK**
    ```json
    {
      "status": "UP"
    }
    ```

## Serviço de Notificações

### URL Base
`http://patient-notification-service.lifeclinic.svc.cluster.local:8081`

### Endpoints

#### 1. Enviar Notificação
- **Método:** POST
- **URL:** `/notify`
- **Corpo da Solicitação:**
  ```json
  {
    "usuario_id": "string",
    "mensagem": "string"
  }
  ```
- **Resposta:**
  - **200 OK**
    ```json
    {
      "status": "string",
      "mensagem_id": "string"
    }
    ```
  - **400 Solicitação Inválida**
    ```json
    {
      "erro": "string"
    }
    ```

#### 2. Obter Notificações por ID de Usuário
- **Método:** GET
- **URL:** `/notifications/{usuario_id}`
- **Resposta:**
  - **200 OK**
    ```json
    [
      {
        "mensagem_id": "string",
        "usuario_id": "string",
        "mensagem": "string",
        "timestamp": "string"
      }
    ]
    ```
  - **404 Não Encontrado**
    ```json
    {
      "erro": "string"
    }
    ```

#### 3. Verificar Saúde
- **Método:** GET
- **URL:** `/health`
- **Resposta:**
  - **200 OK**
    ```json
    {
      "status": "UP"
    }
    ```

## Notas
- Certifique-se de utilizar os endpoints reais dos serviços, por exemplo:
  - `http://appointment-api.lifeclinic.svc.cluster.local:8080`
  - `http://patient-notification-service.lifeclinic.svc.cluster.local:8081`
- Todos os endpoints devem ser protegidos com HTTPS para garantir a privacidade e integridade dos dados.