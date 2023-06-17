# 04 Power Platform Custom Connector for Azure OpemAI 

This inspired is Microsoft MVP CHRIS O'BRIEN blogpost [Power Platform Custom Connector for Azure OpenAI](https://www.sharepointnutsandbolts.com/2023/02/call-chatgpt-gpt-3-from-power-apps-power-automate.html)
In this example you will able to 
- Use Power PLatform custom connector for Azure OpenAI
- Modiifications of Swagger file
- Test the connector
- Usage of the connector within Power Automate

## Step 1

a) Go to Make.PowerApps.com
b) Select **Custom Connector**
c) Select **Create from blank**

![01 Custom Connector](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/451a63dc-b6d1-4b31-aec1-e6df9ad53ce0)


## Step 2

Name the custom connetor 

![02 Name the connector](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/a71774ee-9e3f-4900-b715-1b21f25f9ddd)

## Step 3

Turn on the custom connector 

![03 Turn of Swagger Editor](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/00718ee3-956b-43d6-ad9d-71cf5230dde4)

## Step 4

Update the **host** witin Swagger Editor 

![04 Swagger Host](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/529b866b-b997-4c0c-9b4a-a9e1846aec63)


## Step 5

Update the **default** parameter witin Swagger Editor

![05 Swagger Deployment ID](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f360c0d1-fe85-4999-92d9-de81c18fb508)

~~~
swagger: '2.0'
info:
  title: AzOpenAI
  description: Azure OpenAI - Completions API
  version: '1.0'
host: [YOUR ENDPOINT PREFIX HERE].openai.azure.com
basePath: /openai
schemes:
  - https
consumes: []
produces: []
paths:
  /deployments/{deployment-id}/completions:
    post:
      responses:
        default:
          description: default
          schema:
            type: object
            properties:
              id:
                type: string
                description: id
              object:
                type: string
                description: object
              created:
                type: integer
                format: int32
                description: created
              model:
                type: string
                description: model
              choices:
                type: array
                items:
                  type: object
                  properties:
                    text:
                      type: string
                      description: text
                    index:
                      type: integer
                      format: int32
                      description: index
                    logprobs:
                      type: string
                      description: logprobs
                    finish_reason:
                      type: string
                      description: finish_reason
                description: choices
              usage:
                type: object
                properties:
                  prompt_tokens:
                    type: integer
                    format: int32
                    description: prompt_tokens
                  completion_tokens:
                    type: integer
                    format: int32
                    description: completion_tokens
                  total_tokens:
                    type: integer
                    format: int32
                    description: total_tokens
                description: usage
      parameters:
        - name: deployment-id
          in: path
          required: true
          type: string
          default: [YOUR DEPLOYMENT ID HERE]
          x-ms-visibility: important
        - name: api-version
          in: query
          required: true
          type: string
          default: '2022-12-01'
          x-ms-visibility: important
        - name: Content-Type
          in: header
          required: true
          default: application/json
          type: string
        - name: body
          in: body
          required: false
          schema:
            type: object
            properties:
              prompt:
                type: string
                description: >-
                  The prompt(s) to generate completions for, encoded as a string
                  or array of strings.\nNote that <|endoftext|> is the document
                  separator that the model sees during training, so if a prompt
                  is not specified the model will generate as if from the
                  beginning of a new document. Maximum allowed size of string
                  list is 2048.
              max_tokens:
                type: integer
                description: >-
                  The token count of your prompt plus max_tokens cannot exceed
                  the model's context length. Most models have a context length
                  of 2048 tokens (except for the newest models, which support
                  4096). Has minimum of 0.
              temperature:
                type: number
                description: >-
                  What sampling temperature to use. Higher values means the
                  model will take more risks. Try 0.9 for more creative
                  applications, and 0 (argmax sampling) for ones with a
                  well-defined answer.\nWe generally recommend altering this or
                  top_p but not both.
      operationId: Completions
      summary: Completions
      description: Completions API
      x-ms-visibility: important
definitions: {}
parameters: {}
responses: {}
securityDefinitions:
  API Key:
    type: apiKey
    in: header
    name: api-key
security:
  - API Key: []
tags: []
~~~


In my example **host** is as follows 
![06 Az Overview Host](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/b425cad0-6290-4c5b-ba7e-6122bb6f15ef)

and **default** parameter is as follows
![07 Az default](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/465a40fa-721a-4105-9690-11b459387946)


