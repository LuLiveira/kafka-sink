# Criação de Lambda com AWS CloudFormation

Este comando utiliza o AWS CloudFormation para criar uma stack que inclui uma função Lambda, conforme definido no arquivo `cloudformation.yml`.

```bash
aws cloudformation create-stack \
  --stack-name example-lambda-stack \
  --capabilities CAPABILITY_NAMED_IAM \
  --template-body file://cloudformation.yml \
  --endpoint-url http://localhost:4566
```
## Parametros
- `--stack-name`: Define o nome da stack criada.
- `--capabilities CAPABILITY_NAMED_IAM`: Necessário para permitir a criação de recursos IAM com permissões específicas.
- `--template-body`: Especifica o caminho do arquivo CloudFormation em formato YAML ou JSON.
- `--endpoint-url`: (Opcional) Aponta para um endpoint customizado (neste caso, `http://localhost:4566`, que pode ser utilizado para testes locais com ferramentas como o LocalStack).


### Saida
```json
{
    "StackId": "arn:aws:cloudformation:us-east-1:000000000000:stack/example-lambda-stack/d61cbd21"
}
```

# Listar lambdas criadas

Comando que lista todas as funções Lambda disponíveis na AWS.

```bash
aws lambda list-functions --endpoint-url=http://localhost:4566
```

## Parametros
`--endpoint-url`: Especifica o endpoint para o qual o comando será direcionado. É útil para definir um endpoint customizado, como `http://localhost:4566`, quando se utiliza ferramentas de teste locais, como o LocalStack. Esse parâmetro permite simular o ambiente AWS sem acessar diretamente a nuvem real.

### Saida

```json
{
    "Functions": [
        {
            "FunctionName": "lambda-connector-sink",
            "FunctionArn": "arn:aws:lambda:us-east-1:000000000000:function:lambda-connector-sink",
            "Runtime": "python3.11",
            "Role": "arn:aws:iam::000000000000:role/lambda-connector-sink-role",
            "Handler": "index.lambda_function",
            "CodeSize": 1635,
            "Description": "",
            "Timeout": 3,
            "MemorySize": 128,
            "LastModified": "2024-11-02T17:50:22.308171+0000",
            "CodeSha256": "cI8btvjlJXM3E41tfXUAP32/DML0v8YZAjyjqRqEaJU=",
            "Version": "$LATEST",
            "TracingConfig": {
                "Mode": "PassThrough"
            },
            "RevisionId": "670bd541-95f3-436e-b3fb-9358feda09dd",
            "PackageType": "Zip",
            "Architectures": [
                "x86_64"
            ],
            "EphemeralStorage": {
                "Size": 512
            },
            "SnapStart": {
                "ApplyOn": "None",
                "OptimizationStatus": "Off"
            }
        }
    ]
}
```

# Invocar uma Lambda Function

Comando que invoca uma função Lambda na AWS. Permite enviar dados de entrada (payload) para a função e obter uma resposta.

```bash
aws lambda invoke --function-name example-function \
--cli-binary-format raw-in-base64-out \
--payload '{"value": "my example"}' --output text result \
--endpoint-url http://localhost:4566
```
## Parametros

- `--function-name`: Especifica o nome da função Lambda a ser invocada, neste caso, `"example-function"`.

- `--cli-binary-format raw-in-base64-out`: Indica o formato do payload. O `raw-in-base64-out` é usado para enviar o payload como JSON bruto e receber a resposta em base64.

- `--payload`: Define o conteúdo JSON que será passado como entrada para a função Lambda. No exemplo, é `{"value": "my example"}`.

- `--output text`: Define o formato de saída do comando. Neste caso, `text` salva a resposta em formato de texto no arquivo especificado.

- `result.txt`: Nome do arquivo onde a saída da execução será salva.

- `--endpoint-url`: (Opcional) Define um endpoint customizado, como `http://localhost:4566`, para testes locais com ferramentas como o LocalStack.

- `--debug`: Executar o comando em modo verbose
### Saida

```json
$LATEST 200
```
