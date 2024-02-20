openapi: 3.0.3
info:
  title: Заказ ресурсов в облаке
  version: 0.0.1
servers:
  - url: http://localhost:8080/api/v1
    description: Dev server
paths:
  /clouds:
    get:
      summary: Метод по получению ресуросов облака
      tags:
        - Clouds
      operationId: getAllClouds
      responses:
        "200" : 
          description: Успешный ответ со списком ресурсов
          content:
            adplication/json:
              schema:
                $ref: "#/components/schemas/Clouds"
        "default" : 
          description: Всё остальное
          content: 
            adplication/json:
              schema:
                $ref: "#/components/schemas/Error"
    post:
      summary: Создания заказа на облако
      tags:
        - Clouds
      operationId:  CreateCloud
      requestBody:
        content:
          adplication/json:
            schema:
              $ref: "#/components/schemas/Cloud"
      responses:
        "200" : 
          description: Успешный ответ со списком ресурсов
          content:
            adplication/json:
              schema:
                $ref: "#/components/schemas/Clouds"
        "default" : 
          description: Всё остальное
          content: 
            adplication/json:
              schema:
                $ref: "#/components/schemas/Error"
  /clouds/{cloud_id}:
    delete:
      summary: Отмена заказа
      tags: 
        - Clouds
      operationId: cancelCloudById
      parameters:
        - name: cloud_id
          in: path
          required: true
          description: Id заказа облака 
          schema:
            type: integer
          example: 123
      responses:
        "200" : 
          description: Успешная отмена заказа
          content:
            adplication/json: {}
        "default" : 
          description: Всё остальное
          content: 
            adplication/json:
              schema:
                $ref: "#/components/schemas/Error" 
components:
  schemas:
    Cloud:
      type: object
      properties:
        cloud_id:
          type: integer
          example: 1123
        ram:
          type: integer
          example: 16
        cpu:
          type: integer
          example: 2
        ssd:
          type: integer
        os:
          type: string
          example: linux
    Clouds:
      type: array
      items:
        $ref: "#/components/schemas/Cloud"
    Error:
      type: object
      properties:
        code_error:
          type: integer
          example: 28
        code_message:
          type: string
          example: error
      
