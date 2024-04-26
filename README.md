

---

# Documentação da API para Criação de Usuários

## Visão Geral
Esta documentação descreve como usar a API para criar novos usuários em nosso sistema.

## Requisitos
- Você precisa ter um token de acesso válido para autenticação na API.
- Os dados do usuário a serem criados devem ser fornecidos em formato JSON.

## Endpoint
O endpoint para criar um novo usuário é:

```
POST https://app-dev.mapify.com.br/api/user
```

## Parâmetros
Os seguintes parâmetros devem ser fornecidos no corpo da solicitação em formato JSON:
- **name**: O nome completo do novo usuário.
- **email**: O endereço de e-mail do novo usuário. Deve ser único.
- **password**: A senha do novo usuário.

## Autenticação
A autenticação na API é feita através do cabeçalho de autorização. Você deve incluir o token de acesso como um cabeçalho `Authorization: Bearer {seu_token}`.

## Respostas
A API retorna uma resposta em formato JSON. Aqui estão os possíveis tipos de resposta:

- **Sucesso**: Se o usuário for criado com sucesso, a API retornará um status 200 e a seguinte estrutura JSON:

```json
{
    "message": "Novo usuário criado com sucesso",
    "api_key": "sua_chave_de_api"
}
```

- **Erro**: Se ocorrer um erro durante a criação do usuário, a API retornará um status 400 ou 500 e uma estrutura JSON contendo detalhes sobre o erro. Por exemplo:

```json
{
    "errors": [
        {
            "title": "Erro: Já existe uma conta com este e-mail",
            "status": 400
        }
    ]
}
```

## Exemplos de Solicitação e Resposta
Aqui estão exemplos de como criar um novo usuário usando diferentes tecnologias:

### PHP
```php
<?php

$endpoint = 'https://app-dev.mapify.com.br/api/user';
$token = 'seu_token_aqui';

$data = array(
    'name' => 'Example',
    'email' => 'Example@gmail.com',
    'password' => 'Example123'
);

$options = array(
    'http' => array(
        'method'  => 'POST',
        'header'  => "Content-Type: application/json\r\n" .
                     "Authorization: Bearer $token",
        'content' => json_encode($data)
    )
);

$context  = stream_context_create($options);
$result = file_get_contents($endpoint, false, $context);
$response = json_decode($result, true);

print_r($response);

?>
```

### cURL
```bash
curl -X POST \
  https://app-dev.mapify.com.br/api/user \
  -H 'Authorization: Bearer seu_token' \
  -H 'Content-Type: application/json' \
  -d '{
	"name": "Nome do Novo Usuário",
	"email": "novo_usuario@example.com",
	"password": "senha123"
}'
```

---
