# Lambda DynamoDB CRUD

Este projeto demonstra como criar um CRUD simples usando Node.js, AWS Lambda e DynamoDB com o Serverless Framework.

## Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas:

- [Node.js](https://nodejs.org/) (versão 14 ou superior)
- [npm](https://www.npmjs.com/)
- [Serverless Framework](https://www.serverless.com/)
- [AWS CLI](https://aws.amazon.com/cli/)
- Uma conta AWS com permissões adequadas para criar recursos (Lambda, DynamoDB, IAM)

## Configuração Inicial

### 1. Configurar AWS CLI

Configure a AWS CLI com suas credenciais. Abra o terminal e execute:

```bash
aws configure
```

Insira suas credenciais AWS quando solicitado:

```bash
AWS Access Key ID
AWS Secret Access Key
Default region name (ex: us-east-1)
Default output format (ex: json)
```

### 2. Clonar o Repositório

Clone o repositório para sua máquina local:

```bash
git clone https://github.com/seu-usuario/lambda-dynamodb-crud.git
cd lambda-dynamodb-crud
```

### 3. Instalar Dependências

Instale as dependências do projeto:

```bash
npm install
```

## Estrutura do Projeto

- handler.js: Contém as funções Lambda para criar, ler, atualizar e deletar itens no DynamoDB.

- serverless.yml: Configuração do Serverless Framework para definir os recursos e permissões.

## Configuração do Serverless

No arquivo serverless.yml, certifique-se de que a região e o nome da tabela estão corretos:

```bash
provider:
  name: aws
  runtime: nodejs20.x
  region: us-east-1
  environment:
    TABLE_NAME: CrudTable

custom:
  tableName: CrudTable
```

## Permissões IAM

No mesmo arquivo, adicionamos permissões IAM para que as funções Lambda possam interagir com a tabela DynamoDB:

```bash
iamRoleStatements:
  - Effect: Allow
    Action:
      - dynamodb:PutItem
      - dynamodb:GetItem
      - dynamodb:UpdateItem
      - dynamodb:DeleteItem
    Resource:
      - arn:aws:dynamodb:${self:provider.region}:*:table/${self:custom.tableName}
```

## Deploy

Faça o deploy da aplicação usando o Serverless Framework:

```bash
npx serverless deploy
```

## Testando a API

Use ferramentas como curl ou Postman para testar as funções CRUD.

### Criar um Item

```bash
curl -X POST https://YOUR_API_ENDPOINT/create \
-H "Content-Type: application/json" \
-d '{"info": "sample data"}'
```

### Ler um Item

```bash
curl -X GET https://YOUR_API_ENDPOINT/read/ITEM_ID
```


### Atualizar um Item

```bash
curl -X PUT https://YOUR_API_ENDPOINT/update/ITEM_ID \
-H "Content-Type: application/json" \
-d '{"info": "updated data"}'
```

### Deletar um Item

```bash
curl -X DELETE https://YOUR_API_ENDPOINT/delete/ITEM_ID
```

### Observações

Certifique-se de que o usuário AWS que está configurando a CLI tem permissões para criar e gerenciar recursos Lambda, DynamoDB e IAM.
Em caso de problemas com permissões, revise as políticas IAM atribuídas ao seu usuário ou role.

### Contribuindo
Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

### Licença
Este projeto está licenciado sob a licença MIT.

Desenvolvido por Adriano Negrão


Este README cobre todos os passos necessários para configurar e executar o projeto na máquina de qualquer pessoa, incluindo a configuração das permissões AWS necessárias. Sinta-se à vontade para ajustar as URLs e informações de contato conforme necessário.