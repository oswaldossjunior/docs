Documentação da API – Push Notification Controller
==================================================

Descrição
---------

A API permite a integração com o Firebase para envio de notificações push. Os endpoints exigem autenticação e oferecem funcionalidades como obtenção de tokens, envio de notificações para dispositivos específicos, múltiplos dispositivos, tópicos e execução manual de agendamentos.

### Base URL:

    https://<sua-url-base>/api/push-notification
    

Endpoints Disponíveis
---------------------

* * *

### 1. **Obter Token de Autenticação do Firebase**

**GET** `/firebase-token`

#### Descrição:

Obtém um token de autenticação OAuth 2.0 do Firebase.

#### Respostas:

*   `200 OK`: Retorna o token de autenticação.
*   `500 Internal Server Error`: Erro inesperado.

#### Exemplo de Uso:

    curl -X GET "https://<sua-url-base>/api/push-notification/firebase-token" -H "Authorization: Bearer <seu-token>"
    

* * *

### 2. **Obter Device Token para CPF**

**GET** `/device-token-para-cpf?cpf=<cpf>`

#### Descrição:

Obtém o token de dispositivo associado a um CPF específico.

#### Parâmetros:

*   `cpf` (string, obrigatório): CPF do usuário.

#### Respostas:

*   `200 OK`: Retorna o token do dispositivo.
*   `400 Bad Request`: Requisição inválida.
*   `500 Internal Server Error`: Erro inesperado.

#### Exemplo de Uso:

    curl -X GET "https://<sua-url-base>/api/push-notification/device-token-para-cpf?cpf=12345678900" -H "Authorization: Bearer <seu-token>"
    

* * *

### 3. **Enviar Notificação para um Dispositivo**

**POST** `/send-to-device`

#### Descrição:

Envia uma notificação push para um dispositivo específico usando o device token.

#### Corpo da Requisição (JSON):

    {
      "deviceToken": "exemplo_token",
      "titulo": "Título da Notificação",
      "mensagem": "Mensagem da Notificação"
    }
    

#### Respostas:

*   `200 OK`: Notificação enviada com sucesso.
*   `400 Bad Request`: Requisição inválida.
*   `500 Internal Server Error`: Erro inesperado.

#### Exemplo de Uso:

    curl -X POST "https://<sua-url-base>/api/push-notification/send-to-device" \
    -H "Authorization: Bearer <seu-token>" \
    -H "Content-Type: application/json" \
    -d '{"deviceToken":"exemplo_token","titulo":"Olá!","mensagem":"Esta é uma notificação."}'
    

* * *

### 4. **Enviar Notificação para Múltiplos Dispositivos**

**POST** `/send-to-multiple-devices`

#### Descrição:

Envia uma notificação push para múltiplos dispositivos.

#### Corpo da Requisição (JSON):

    {
      "deviceTokens": ["token1", "token2"],
      "titulo": "Título",
      "mensagem": "Mensagem para múltiplos dispositivos"
    }
    

#### Respostas:

*   `200 OK`: Notificação enviada com sucesso.
*   `400 Bad Request`: Lista de tokens não pode ser vazia.
*   `500 Internal Server Error`: Erro inesperado.

* * *

### 5. **Enviar Notificação para um Tópico**

**POST** `/send-to-topic`

#### Descrição:

Envia uma notificação push para um tópico específico.

#### Corpo da Requisição (JSON):

    {
      "topic": "nome_do_topico",
      "titulo": "Título do Tópico",
      "mensagem": "Mensagem para o tópico"
    }
    

#### Respostas:

*   `200 OK`: Notificação enviada com sucesso.
*   `400 Bad Request`: O nome do tópico é obrigatório.
*   `500 Internal Server Error`: Erro inesperado.

* * *

### 6. **Executar Agendamento de Push Notification**

**POST** `/run-push-notification-schedule`

#### Descrição:

Executa manualmente o agendamento de envio de notificações push.

#### Respostas:

*   `200 OK`: Notificação enviada com sucesso.
*   `400 Bad Request`: Requisição inválida.
*   `500 Internal Server Error`: Erro inesperado.

#### Exemplo de Uso:

    curl -X POST "https://<sua-url-base>/api/push-notification/run-push-notification-schedule" -H "Authorization: Bearer <seu-token>"
    

* * *

Considerações Finais:
---------------------

*   Todos os endpoints requerem o header `Authorization` com um token Bearer válido.
*   Utilize a autenticação OAuth 2.0 para obter o token necessário.
*   Certifique-se de que os parâmetros obrigatórios estejam preenchidos corretamente.