# Go and PostgreSQL API

Este projeto é uma API RESTful simples desenvolvida em Go utilizando o framework Fiber e o ORM Gorm para interagir com um banco de dados PostgreSQL. A aplicação permite gerenciar livros, com funcionalidades como criar, listar, buscar por ID e excluir livros.

## Funcionalidades

- Criar um novo livro
- Listar todos os livros
- Buscar um livro por ID
- Excluir um livro

## Requisitos

Certifique-se de ter os seguintes itens instalados:

- [Go](https://golang.org/) v1.20 ou superior
- [PostgreSQL](https://www.postgresql.org/) v12 ou superior
- [Git](https://git-scm.com/)

## Configuração do Projeto

1. Clone o repositório:

   ```bash
   git clone https://github.com/pablopastuchenko/goandpostgres.git
   cd goandpostgres
   ```

2. Instale as dependências:

   ```bash
   go mod tidy
   ```

3. Configure as variáveis de ambiente:
   Crie um arquivo `.env` na raiz do projeto com as seguintes variáveis:

   ```env
   DB_HOST=localhost
   DB_PORT=5432
   DB_USER=seu_usuario
   DB_PASS=sua_senha
   DB_NAME=nome_do_banco
   DB_SSLMODE=disable
   ```

4. Inicie o PostgreSQL e crie o banco de dados especificado na variável `DB_NAME`.

5. Execute as migrações para criar as tabelas:
   O projeto executa automaticamente as migrações na inicialização.

## Executando a Aplicação

1. Inicie o servidor:

   ```bash
   go run main.go
   ```

2. A API estará disponível em [http://localhost:8080](http://localhost:8080).

## Endpoints da API

### Criar Livro

- **POST** `/api/create_books`
- **Body**:
  ```json
  {
    "author": "Autor Exemplo",
    "title": "Título Exemplo",
    "publisher": "Editora Exemplo"
  }
  ```
- **Resposta de Sucesso** (HTTP 200):
  ```json
  {
    "message": "book has been added"
  }
  ```

### Listar Todos os Livros

- **GET** `/api/books`
- **Resposta de Sucesso** (HTTP 200):
  ```json
  {
    "message": "books fetched successfully",
    "data": [
      {
        "id": 1,
        "author": "Autor Exemplo",
        "title": "Título Exemplo",
        "publisher": "Editora Exemplo"
      }
    ]
  }
  ```

### Buscar Livro por ID

- **GET** `/api/get_books/:id`
- **Resposta de Sucesso** (HTTP 200):
  ```json
  {
    "message": "book id fetched successfully",
    "data": {
      "id": 1,
      "author": "Autor Exemplo",
      "title": "Título Exemplo",
      "publisher": "Editora Exemplo"
    }
  }
  ```

### Excluir Livro

- **DELETE** `/api/delete_book/:id`
- **Resposta de Sucesso** (HTTP 200):
  ```json
  {
    "message": "book delete successfully"
  }
  ```

## Estrutura do Projeto

### Inicialização com Docker

Você pode iniciar o projeto com os seguintes comandos:

```bash
docker-compose up -d
go run main.go
```

### Cadastro de Usuário (POST)

- **URL**: `http://localhost:8000/users/signup`
- **Body**:
  ```json
  {
    "first_name": "Akhil",
    "last_name": "Sharma",
    "email": "akhil@gmail.com",
    "password": "akhilsharma",
    "phone": "+4534545435"
  }
  ```
- **Resposta**: "Cadastro realizado com sucesso!!"

### Login de Usuário (POST)

- **URL**: `http://localhost:8000/users/login`
- **Body**:
  ```json
  {
    "email": "akhil@gmail.com",
    "password": "akhilsharma"
  }
  ```
- **Resposta** (exemplo):
  ```json
  {
    "_id": "**********",
    "first_name": "Akhil",
    "last_name": "Sharma",
    "password": "$2a$14$UIYjkTfnFnhg4qhIfhtYnuK9qsBQifPKgu/WPZAYBaaN17j0eTQZa",
    "email": "akhil@gmail.com",
    "phone": "+4534545435",
    "token": "eyJc0Bwcm90b25v...",
    "Refresh_Token": "eyJhbGciOiJIUzI1NiIsInR5...",
    "created_at": "2022-04-09T08:14:11Z",
    "updated_at": "2022-04-09T08:14:11Z",
    "user_id": "61614f539f29be942bd9df8e",
    "usercart": [],
    "address": [],
    "orders": []
  }
  ```

### Adicionar Produto (POST)

- **URL**: `http://localhost:8000/admin/addproduct`
- **Body**:
  ```json
  {
    "product_name": "Alienware x15",
    "price": 2500,
    "rating": 10,
    "image": "alienware.jpg"
  }
  ```
- **Resposta**: "Produto adicionado com sucesso, Admin!!"

### Ver Todos os Produtos (GET)

- **URL**: `http://localhost:8000/users/productview`
- **Resposta**:
  ```json
  [
    {
      "Product_ID": "6153ff8edef2c3c0a02ae39a",
      "product_name": "alienwarex15",
      "price": 1500,
      "rating": 10,
      "image": "alienware.jpg"
    },
    {
      "Product_ID": "616152679f29be942bd9df8f",
      "product_name": "ginger ale",
      "price": 900,
      "rating": 5,
      "image": "gin.jpg"
    }
  ]
  ```

### Busca de Produtos por Regex (GET)

- **URL**: `http://localhost:8000/users/search?name=al`
- **Resposta**:
  ```json
  [
    {
      "Product_ID": "616152fa9f29be942bd9df91",
      "product_name": "Alienware x15",
      "price": 1500,
      "rating": 10,
      "image": "1.jpg"
    }
  ]
  ```

### Carrinho de Compras

- **Adicionar ao Carrinho (GET)**: `http://localhost:8000/addtocart?id=product_id&userID=user_id`
- **Remover do Carrinho (GET)**: `http://localhost:8000/removefromcart?id=product_id&userID=user_id`
- **Listar Itens do Carrinho (GET)**: `http://localhost:8000/listcart?id=user_id`

### Endereço do Usuário (POST)

- **URL**: `http://localhost:8000/addadress?id=user_id`
- **Body**:
  ```json
  {
    "house_name": "white house",
    "street_name": "white street",
    "city_name": "washington",
    "pin_code": "332423432"
  }
  ```
- **Nota**: O array de endereços é limitado a dois valores: "home" e "work". Não é permitido mais de dois endereços.

