Aqui está o passo a passo em Markdown para configurar e executar o código:

---

# Passo a Passo para Executar o Servidor Node.js com Operações Matemáticas

Este guia ensina como configurar e executar um servidor Node.js que realiza operações matemáticas básicas (soma, subtração, multiplicação e divisão) através de rotas HTTP.

## Pré-requisitos

- **Node.js**: Verifique se o Node.js está instalado executando `node -v` no terminal. Caso não esteja instalado, [baixe aqui](https://nodejs.org/).

## Passos

### 1. Crie uma Pasta para o Projeto

No terminal, crie e navegue até uma nova pasta para organizar seu projeto.

```bash
mkdir meu-servidor
cd meu-servidor
```

### 2. Inicialize o Projeto com `package.json`

Inicialize o projeto e crie o arquivo `package.json`, que irá gerenciar as dependências.

```bash
npm init -y
```

### 3. Instale o Express

O Express é o framework usado para criar o servidor HTTP.

```bash
npm install express
```

### 4. Crie o Arquivo do Servidor

Crie um arquivo chamado `server.js` e adicione o código do servidor:

```javascript
var express = require('express');
var app = express();
var bodyParser = require('body-parser');
app.use(bodyParser.json());

app.get('/', function(req, res) {
  res.send('Oi, mundo :-)');
});

app.post('/soma', function (req, res) {
    var body = req.body;
    var resultado = soma(body.a, body.b);
    res.send(`O resultado da soma de ${body.a} e ${body.b} é ${resultado}`);
});

app.post('/subtracao', function (req, res) {
    var body = req.body;
    var resultado = subtracao(body.a, body.b);
    res.send(`O resultado da subtração de ${body.a} e ${body.b} é ${resultado}`);
});

app.post('/multiplicacao', function (req, res) {
    var body = req.body;
    var resultado = multiplicacao(body.a, body.b);
    res.send(`O resultado da multiplicação de ${body.a} e ${body.b} é ${resultado}`);
});

app.post('/divisao', function (req, res) {
    var body = req.body;
    if (body.b === 0) {
        res.send('Erro: Divisão por zero não é permitida.');
    } else {
        var resultado = divisao(body.a, body.b);
        res.send(`O resultado da divisão de ${body.a} e ${body.b} é ${resultado}`);
    }
});

function soma(a, b) {
    return a + b;
}

function subtracao(a, b) {
    return a - b;
}

function multiplicacao(a, b) {
    return a * b;
}

function divisao(a, b) {
    return a / b;
}

var port = 3001;

app.listen(port, function() {
  console.log(`App de Exemplo escutando na porta http://localhost:${port}/`);
});
```

### 5. Inicie o Servidor

Execute o seguinte comando para iniciar o servidor:

```bash
node server.js
```

Você verá a mensagem: 

```
App de Exemplo escutando na porta http://localhost:3001/
```

### 6. Teste as Operações com cURL ou Postman

Para testar o funcionamento das operações, você pode utilizar o **Postman** ou **cURL**. Abaixo estão exemplos de comandos cURL:

#### Testar a Rota de Soma

```bash
curl -X POST http://localhost:3001/soma -H "Content-Type: application/json" -d "{\"a\": 5, \"b\": 3}"
```

#### Testar a Rota de Subtração

```bash
curl -X POST http://localhost:3001/subtracao -H "Content-Type: application/json" -d "{\"a\": 5, \"b\": 3}"
```

#### Testar a Rota de Multiplicação

```bash
curl -X POST http://localhost:3001/multiplicacao -H "Content-Type: application/json" -d "{\"a\": 5, \"b\": 3}"
```

#### Testar a Rota de Divisão

```bash
curl -X POST http://localhost:3001/divisao -H "Content-Type: application/json" -d "{\"a\": 6, \"b\": 3}"
```

Pronto! O servidor está configurado e as operações podem ser testadas diretamente pelo terminal ou por um cliente HTTP, como o Postman.
