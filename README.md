## O que é o projeto?

Desenvolvimento de aplicação serverless com Java e Maven para redirecionamento de urls. 

Realizado a integração com AWS S3 para criação e gerenciamento de buckets, exposição de endpoints via API Gateway, uso deAWS Lambda para processamento serverless, e manipulação de dados em JSON com Jackson.

Projeto feito no Curso Gratuito de Java da Rocketseat, que aconteceu entre 18/11/2024 e 22/11/2024, com 5h de duração.


## Estrutura do Repositório

- **`CreateUrlLambda/`**: Contém a primeira função Lambda responsável por salvar as informações da requisição e gerar um código único.

Exemplo do `body` da requisição:
```bash
{
	"originalUrl": "um link qualquer, exemplo: https://www.google.com.br/",
	"expirationTime": "tempo para expiração em segundos, exemplo: 1732208836"
}
```
```bash
    "originalUrl" type String
    "expirationTime" type long
```

Exemplo da reposta da requição `POST`:
```bash
{
	"code": "1f5f981b"
}
```
- **`RedirectUrlShortener/`**: Contém a segunda função Lambda responsável por capturar o código gerado pela função Lambda `CreateUrlLambda` e fazer uma requisição em `GET /{urlCode}`.

Exemplo:
```bash
https://minhaapi.com/{urlcode}
```

A resposta da requisição é o redirecionamento direto do link registrado.


## Requisitos para o projeto

- **Java** 17
- **Maven** para gerenciar dependências e empacotamento
- Conta na **AWS** com permissões para Lambda, S3 e API Gateway.



## Configuração na AWS

Explique como configurar os serviços da AWS para que o projeto funcione corretamente:

1. **Configurar o AWS S3**:
   - Crie um bucket no S3.
   - Configure permissões para o bucket, permitindo acesso às funções Lambda.

2. **Configurar o AWS Lambda**:
   - Faça o deploy de cada função Lambda individualmente:
     - Acesse o painel do AWS Lambda.
     - Crie uma nova função.
     - Faça o upload do `.jar` gerado no diretório `target/` de cada projeto.

3. **Configurar o API Gateway**:
   - Crie uma API REST no API Gateway.
   - Adicione endpoints para cada função Lambda.
   - Configure as integrações (métodos GET e POST) com as funções Lambda.


## Como Rodar Localmente

1. Clone o repositório:
   ```bash
   git clone https://github.com/WesleyRodrigues55/redirect-url-shortener.git
   cd redirect-url-shortener
   ```

2. Navegue para um dos projetos
   ```bash
    cd CreateUrlLambda
   ```

3. Instale as dependências e empacote o projeto:
    ```bash
    mvn clean package
    ```