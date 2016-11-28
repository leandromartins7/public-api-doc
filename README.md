# VEXPENSES RESTful API v2

## Autenticação

Para acessar os dados utilizando nossa API é necessário que você se faça a autenticação no sistema. Para isso adicione uma chave no header HTTP conforme o exemplo a abaixo:

```
Authorization: Bearer <TOKEN>
```

O ``<TOKEN>`` descrito no código deve ser substituido pelo Token de autorização que você consegue através da sua conta no VEXPENSES.


## Endpoints

O dominio para acesso dos endpoints da API é ``https://api.vexpenses.com/v2``.

### Fluxos de Aprovação

####``GET /fluxos-de-aprovacao`` - Para pegar todos os fluxos de aprovação

```javascript
{
  "request": "https://api.vexpenses.com/v2/fluxos-de-aprovacao" ,
  "method" : "GET",
  "success": true,
  "statusCode": 200,
  "message": "Fluxos de aprovação enviados com sucesso!",
  "data": [{
    "id": 2,
    "idExterno" : null,
    "idEmpresa": 216,
    "descricao": "Fluxo 1",
    "created_at": "2016-09-22 14:43:12",
    "updated_at": "2016-09-22 14:43:12",
    "deleted_at": null,
    "etapas": [{
      "operador": "E",
      "valorEntrada": 0,
      "grupos": [{
        "operador": "E",
        "aprovadores" : [1, 12, 13]
      }, {
        "operador": "OU",
        "aprovadores" : [2, 10]
      }]
    }, {
      "operador": "OU",
      "valorEntrada": 1000,
      "grupos": [{
        "operador": "OU",
        "aprovadores" : [3, 4]
      }]
    }]
  }, {
    "id": 3,
    "idExterno" : null,
    "idEmpresa": 216,
    "descricao": "Fluxo 2",
    "created_at": "2016-09-29 17:51:34",
    "updated_at": "2016-09-29 17:51:34",
    "deleted_at": null,
    "etapas": [{
      "operador": "E",
      "valorEntrada": 0,
      "grupos": [{
        "operador": "E",
        "aprovadores" : [1, 12, 13]
      }, {
        "operador": "OU",
        "aprovadores" : [2, 10]
      }]
    }, {
      "operador": "OU",
      "valorEntrada": 1000,
      "grupos": [{
        "operador": "OU",
        "aprovadores" : [3, 4]
      }]
    }]
  }]
}

```

#### ``GET /fluxos-de-aprovacao/:id_fluxo`` - Para pegar um fluxo de aprovação

```javascript
{
  "request": "https://api.vexpenses.com/v2/fluxos-de-aprovacao/2",
  "method" : "GET",
  "success": true,
  "statusCode": 200,
  "message": "",
  "data": {
    "id": 2,
    "idExterno" : null,
    "idEmpresa": 216,
    "descricao": "Fluxo 1",
    "created_at": "2016-09-22 14:43:12",
    "updated_at": "2016-09-22 14:43:12",
    "deleted_at": null,
    "etapas": [{
      "operador": "E",
      "valorEntrada": 0,
      "grupos": [{
        "operador": "E",
        "aprovadores" : [1, 12, 13]
      }, {
        "operador": "OU",
        "aprovadores" : [2, 10]
      }]
    }, {
      "operador": "OU",
      "valorEntrada": 1000,
      "grupos": [{
        "operador": "OU",
        "aprovadores" : [3, 4]
      }]
    }]
  }
}
```

#### ``POST /fluxos-de-aprovacao`` - Para criar um fluxo

**Request body:**

>OBS: A primeira etapa é sempre OBRIGATÓRIA, ou seja, tem valorEntrada = 0.

```javascript
{
  "descricao": "Fluxo 1",
  "idExterno": "bc346365-2a5a-40cf-a544-9cab34c8f0e7",
  "etapas": [{
    "operador": "E",
    "valorEntrada": 0,
    "grupos": [{
      "operador": "E",
      "aprovadores" : [1, 12, 13]
    }, {
      "operador": "OU",
      "aprovadores" : [2, 10]
    }]
  }, {
    "operador": "OU",
    "valorEntrada": 1000,
    "grupos": [{
      "operador": "OU",
      "aprovadores" : [3, 4]
    }]
  }]
}
```

**Response:**


```javascript
{
  "request": "https://api.vexpenses.com/v2/fluxos-de-aprovacao",
  "method": "POST",
  "success": true,
  "statusCode": 201
  "message": "",
  "data": {
    "id": 10,
    "idExterno": "bc346365-2a5a-40cf-a544-9cab34c8f0e7",
    "descricao": "Fluxo 1",
    "created_at": "2016-11-23 16:39:10",
    "updated_at": "2016-11-23 16:39:10",
    "etapas": [{
      "operador": "E",
      "valorEntrada": 0,
      "grupos": [{
        "operador": "E",
        "aprovadores": [1, 12, 13]
      }, {
        "operador": "OU",
        "aprovadores": [2, 10]
      }]
    }, {
      "operador": "OU",
      "valorEntrada": 1000,
      "grupos": [{
        "operador": "OU",
        "aprovadores": [3, 4]
      }]
    }]
  }
}
```

#### ``PUT /fluxos-de-aprovacao/:id_fluxo`` - Para atualizar um fluxo

Neste caso o envio de etapas é opcional.

Toda edição de etapas é uma substituição, portanto, se quiser alterar uma etapa envie todo o array de etapas.

**Request body:**

```javascript
{
  "descricao": "Comercial",
  "etapas": [{
    "operador": "E",
    "valorEntrada": 0,
    "grupos": [{
      "operador": "E",
      "aprovadores" : [1, 12, 13]
    }, {
      "operador": "OU",
      "aprovadores" : [2, 10]
    }]
  }, {
    "operador": "OU",
    "valorEntrada": 1000,
    "grupos": [{
      "operador": "OU",
      "aprovadores" : [3, 4]
    }]
  }]
}
```

**Response:**


```javascript
{
  "request": "https://api.vexpenses.com/v2/fluxos-de-aprovacao/10",
  "method": "PUT",
  "success": true,
  "statusCode": 200,
  "message": "",
  "data": {
    "id": 10,
    "idExterno": "bc346365-2a5a-40cf-a544-9cab34c8f0e7",
    "descricao": "Comercial",
    "created_at": "2016-11-23 16:39:10",
    "updated_at": "2016-11-23 17:00:00",
    "etapas": [{
      "operador": "E",
      "valorEntrada": 0,
      "grupos": [{
        "operador": "E",
        "aprovadores": [1, 12, 13]
      }, {
        "operador": "OU",
        "aprovadores": [2, 10]
      }]
    }, {
      "operador": "OU",
      "valorEntrada": 1000,
      "grupos": [{
        "operador": "OU",
        "aprovadores": [3, 4]
      }]
    }]
  }
}
```

#### ``DELETE /fluxos-de-aprovacao/:id_fluxo`` - Para deletar um fluxo

```javascript
{
  "request": "https://api.vexpenses.com/v2/fluxos-de-aprovacao/10",
  "method": "DELETE",
  "success": true,
  "statusCode": 200,
  "message": ""
}
```


#### ``PUT /relatorios/:id_relatorio/pagar`` - Para "pagar" um relatório

**Request body:**

```javascript
{
  "dataPagamento" : "2016-11-23",
  "valorPagamento" : 200.00
}
```

**Response:**

```javascript
{
  "request": "https://api.vexpenses.com/v2/relatorios/10/pagar",
  "method": "PUT",
  "success": true,
  "statusCode": 200,
  "message": "",
  "data": {
    "id": 10,
    "idUsuario": 92,
    "idDevice": null,
    "descricao": "NOVEMBRO",
    "status": "PAGO",
    "idEtapaResultado": null,
    "dataAprovacao": "2016-07-15 13:22:12",
    "dataPagamento": "2016-08-17 17:24:41",
    "idEmpresaPagante": 1,
    "justificativa": null,
    "dataPagamento" : "2016-11-23",
    "valorPagamento" : 200.00
    "ativo": true,
    "created_at": "2016-11-13 13:26:24",
    "updated_at": "2016-11-23 17:00:00"
  }
}
```

#### ``GET /membros-de-equipe`` - Para listar os membros de equipe


```javascript
{
  "request": "https://api.vexpenses.com/v2/membros-de-equipe",
    "method": "GET",
    "success": true,
    "statusCode": 200,
    "message": "",
    "data": [{
      "id": 289,
      "idExterno": "a1d26199-28ef-432f-b460-be6bedf99095",
      "idEmpresa": 686,
      "idCargo": null,
      "idAprovacaoFluxo": null,
      "idDespesaLimitePolitica": null,
      "tipoUsuario": "ADMINISTRADOR",
      "nome": "Bruno Oliveira",
      "email": "bruno@indb.com.br",
      "cpf": null,
      "fone1": null,
      "fone2": null,
      "dataNascimento": null,
      "banco": null,
      "agencia": null,
      "conta": null,
      "ativo": true,
      "created_at": "2016-11-10 09:25:17",
      "updated_at": "2016-11-10 09:58:40"
    }]
}
```

#### ``GET /membros-de-equipe/:id_membro`` - Para buscar um único membro de equipe

```javascript
{
  "request": "https://api.vexpenses.com/v2/membros-de-equipe/289",
  "method": "GET",
  "success": true,
  "statusCode": 200,
  "message": "",
  "data": {
    "id": 289,
    "idEmpresa": 686,
    "idExterno": "a1d26199-28ef-432f-b460-be6bedf99095",
    "idCargo": null,
    "idAprovacaoFluxo": null,
    "idDespesaLimitePolitica": null,
    "tipoUsuario": "ADMINISTRADOR",
    "nome": "Bruno Oliveira",
    "email": "bruno@indb.com.br",
    "cpf": null,
    "fone1": null,
    "fone2": null,
    "dataNascimento": null,
    "banco": null,
    "agencia": null,
    "conta": null,
    "ativo": true,
    "created_at": "2016-11-10 09:25:17",
    "updated_at": "2016-11-10 09:58:40"
  } 
}
```

#### ``POST /membros-de-equipe`` - Para criar um membro de equipe

**Request body:**

```javascript
{
  "idExterno": "78c205da-935d-4772-8b34-4f142bb22831",
  "tipoUsuario": "USUARIO",
  "nome": "John Doe",
  "email": "john.doe@indb.com.br",
  "cpf": "412.441.929-00",
  "fone1": "(16) 99173-1135",
  "fone2": "(16) 3722-1234",
  "dataNascimento": "1980-05-16",
  "password": "xxxxxxxxxxxxx"
}
```

**Response:**

```javascript
{
  "request": "https://api.vexpenses.com/v2/membros-de-equipe",
  "method": "POST",
  "success": true,
  "statusCode": 201,
  "message": "",
  "data": {
    "id": 300,
    "idEmpresa": 686,
    "idExterno": "78c205da-935d-4772-8b34-4f142bb22831",
    "idCargo": null,
    "idAprovacaoFluxo": null,
    "idDespesaLimitePolitica": null,
    "tipoUsuario": "USUARIO",
    "nome": "John Doe",
    "email": "john.doe@indb.com.br",
    "cpf": "412.441.929-00",
    "fone1": "(16) 99173-1135",
    "fone2": "(16) 3722-1234",
    "dataNascimento": "1980-05-16",
    "banco": null,
    "agencia": null,
    "conta": null,
    "ativo": true,
    "created_at": "2016-11-10 13:00:00",
    "updated_at": "2016-11-10 13:00:00"
  }
}
```

#### ``PUT /membros-de-equipe/:id_membro`` - Para atualizar um membro de equipe

**Request body:**

```javascript
{ 
  "tipoUsuario": "ADMINSTRADOR",
}
```

**Response:**

```javascript
{
  "request": "https://api.vexpenses.com/v2/membros-de-equipe/300",
  "method": "PUT",
  "success": true,
  "statusCode": 200,
  "message": "",
  "data": {
    "id": 300,
    "idEmpresa": 686,
    "idExterno": "78c205da-935d-4772-8b34-4f142bb22831",
    "idCargo": null,
    "idAprovacaoFluxo": null,
    "idDespesaLimitePolitica": null,
    "tipoUsuario": "ADMINISTRADOR",
    "nome": "John Doe",
    "email": "john.doe@indb.com.br",
    "cpf": "412.441.929-00",
    "fone1": "(16) 99173-1135",
    "fone2": "(16) 3722-1234",
    "dataNascimento": "1980-05-16",
    "banco": null,
    "agencia": null,
    "conta": null,
    "ativo": true,
    "created_at": "2016-11-10 13:00:00",
    "updated_at": "2016-11-10 13:00:00"
  }
}
```

#### ``PUT /membros-de-equipe/:id_membro`` - Para desativar um membro de equipe

**Request body:**

```javascript
{
  "ativo": false,
}
```

**Response:**

```javascript
{
  "request": "https://api.vexpenses.com/v2/membros-de-equipe/300",
  "method": "PUT",
  "success": true,
  "statusCode": 200,
  "message": "",
  "data": {
    "id": 300,
    "idEmpresa": 686,
    "idExterno": "78c205da-935d-4772-8b34-4f142bb22831",
    "idCargo": null,
    "idAprovacaoFluxo": null,
    "idDespesaLimitePolitica": null,
    "tipoUsuario": "ADMINISTRADOR",
    "nome": "John Doe",
    "email": "john.doe@indb.com.br",
    "cpf": "412.441.929-00",
    "fone1": "(16) 99173-1135",
    "fone2": "(16) 3722-1234",
    "dataNascimento": "1980-05-16",
    "banco": null,
    "agencia": null,
    "conta": null,
    "ativo": false,
    "created_at": "2016-11-10 13:00:00",
    "updated_at": "2016-11-10 13:00:00"
  }
}
```
