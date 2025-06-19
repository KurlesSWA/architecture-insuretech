# Задание 5

## swagger-схема

```yaml
swagger: '2.0'
info:
  description: API сервиса управления клиентскими данными
  version: 1.0.0
  title: Клиентский Сервис
host: api.client-service.com
basePath: /v1
schemes:
  - https
paths:
  /clients/{id}:
    get:
      tags:
        - Клиент
      summary: Получить информацию о клиенте по ID
      description: Возвращает информацию о клиенте.
      produces:
        - application/json
      parameters:
        - name: id
          in: path
          description: ID клиента
          required: true
          type: string
      responses:
        '200':
          description: Успешный ответ
          schema:
            $ref: '#/definitions/Client'
  /clients/{id}/documents:
    get:
      tags:
        - Документы
      summary: Список документов клиента
      description: Возвращает список документов клиента по ID.
      produces:
        - application/json
      parameters:
        - name: id
          in: path
          description: ID клиента для поиска его документов
          required: true
          type: string
      responses:
        '200':
          description: Успешный ответ
          schema:
            type: array
            items:
              $ref: '#/definitions/Document'
  /clients/{id}/relatives:
    get:
      tags:
        - Родственники
      summary: Информация о родственниках клиента
      description: Возвращает информацию о родственниках клиента по ID.
      produces:
        - application/json
      parameters:
        - name: id
          in: path
          description: ID клиента
          required: true
          type: string
      responses:
        '200':
          description: Успешный ответ
          schema:
            type: array
            items:
              $ref: '#/definitions/Relative'
definitions:
  Client:
    type: object
    properties:
      id:
        type: string
      name:
        type: string
      age:
        type: integer
  Document:
    type: object
    properties:
      id:
        type: string
      type:
        type: string
      number:
        type: string
      issueDate:
        type: string
      expiryDate:
        type: string
  Relative:
    type: object
    properties:
      id:
        type: string
      relationType:
        type: string
      name:
        type: string
      age:
        type: integer
```

[Ссылка](swagger.yaml) на swagger-схему

## GraphQL схема

```graphql
type Query {
  # Получить информацию о клиенте по ID
  client(id: ID!): Client

  # Получить список документов клиента
  clientDocuments(id: ID!): [Document]

  # Получить информацию о родственниках клиента
  clientRelatives(id: ID!): [Relative]
}

type Client {
  id: ID!
  name: String!
  age: Int!
}

type Document {
  id: ID!
  type: String!
  number: String!
  issueDate: String! 
  expiryDate: String!
}

type Relative {
  id: ID!
  relationType: String!
  name: String!
  age: Int!
}
```

[Ссылка](graphql.graphql) на GraphQL-схему
