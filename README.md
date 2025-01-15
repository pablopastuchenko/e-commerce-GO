# Você pode iniciar o projeto com os seguintes comandos
docker-compose up -d
go run main.go
Função de Cadastro de Usuário (requisição POST)

URL: http://localhost:8000/users/signup

json
Copiar código
{
  "first_name": "Akhil",
  "last_name": "Sharma",
  "email": "akhil@gmail.com",
  "password": "akhilsharma",
  "phone": "+4534545435"
}
Resposta: "Cadastro realizado com sucesso!!"

Função de Login de Usuário (requisição POST)

URL: http://localhost:8000/users/login

json
Copiar código
{
  "email": "akhil@gmail.com",
  "password": "akhilsharma"
}
Resposta (exemplo):

json
Copiar código
{
  "_id": "***********************",
  "first_name": "Akhil",
  "last_name": "Sharma",
  "password": "$2a$14$UIYjkTfnFnhg4qhIfhtYnuK9qsBQifPKgu/WPZAYBaaN17j0eTQZa",
  "email": "akhil@gmail.com",
  "phone": "+4534545435",
  "token": "eyJc0Bwcm90b25vbWFpbC5jb20iLCJGaXJzdF9OYW1lIjoiam9zZXBoIiwiTGFzdF9OYW1lIjoiaGVybWlzIiwiVWlkIjoiNjE2MTRmNTM5ZjI5YmU5NDJiZDlkZjhlIiwiZXhwIjoxNjMzODUzNjUxfQ.NbcpVtPLJJqRF44OLwoanynoejsjdJb5_v2qB41SmB8",
  "Refresh_Token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJFbWFpbCI6IiIsIkZpcnLCJVaWQiOiIiLCJleHAiOjE2MzQzNzIwNTF9.ocpU8-0gCJsejmCeeEiL8DXhFcZsW7Z3OCN34HgIf2c",
  "created_at": "2022-04-09T08:14:11Z",
  "updtaed_at": "2022-04-09T08:14:11Z",
  "user_id": "61614f539f29be942bd9df8e",
  "usercart": [],
  "address": [],
  "orders": []
}
Função de Adicionar Produto (requisição POST)

URL: http://localhost:8000/admin/addproduct

json
Copiar código
{
  "product_name": "Alienware x15",
  "price": 2500,
  "rating": 10,
  "image": "alienware.jpg"
}
Resposta: "Produto adicionado com sucesso, Admin!!"

Ver Todos os Produtos no Banco de Dados (requisição GET)

URL: http://localhost:8000/users/productview

Resposta:

json
Copiar código
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
  },
  {
    "Product_ID": "616152ee9f29be942bd9df90",
    "product_name": "iphone 13",
    "price": 1700,
    "rating": 4,
    "image": "ipho.jpg"
  },
  {
    "Product_ID": "616152fa9f29be942bd9df91",
    "product_name": "whiskey",
    "price": 100,
    "rating": 7,
    "image": "whis.jpg"
  },
  {
    "Product_ID": "616153039f29be942bd9df92",
    "product_name": "acer predator",
    "price": 3000,
    "rating": 10,
    "image": "acer.jpg"
  }
]
Função de Busca de Produtos por Regex (requisição GET)

Define a palavra de pesquisa para ordenação. URL: http://localhost:8000/users/search?name=al

Resposta:

json
Copiar código
[
  {
    "Product_ID": "616152fa9f29be942bd9df91",
    "product_name": "Alienware x15",
    "price": 1500,
    "rating": 10,
    "image": "1.jpg"
  },
  {
    "Product_ID": "616153039f29be942bd9df92",
    "product_name": "ginger Ale",
    "price": 300,
    "rating": 10,
    "image": "1.jpg"
  }
]
Adicionando Produtos ao Carrinho (requisição GET)

URL: http://localhost:8000/addtocart?id=xxxproduct_idxxx&userID=xxxxxxuser_idxxxxxx

Consulta correspondente no MongoDB.

Removendo Produto do Carrinho (requisição GET)

URL: http://localhost:8000/addtocart?id=xxxxxxx&userID=xxxxxxxxxxxx

Listando Itens no Carrinho do Usuário (requisição GET) e preço total

URL: http://localhost:8000/listcart?id=xxxxxxuser_idxxxxxxxxxx

Adicionando Endereço (requisição POST)

URL: http://localhost:8000/addadress?id=user_id********

O array de endereços é limitado a dois valores: "home" e "work". Não é permitido mais de dois endereços.

json
Copiar código
{
  "house_name": "white house",
  "street_name": "white street",
  "city_name": "washington",
  "pin_code": "332423432"
}
Editando o Endereço de Casa (requisição PUT)

URL: http://localhost:8000/edithomeaddress?id=xxxxxxxxxxuser_idxxxxxxxxxxxxxxx

Editando o Endereço de Trabalho (requisição PUT)

URL: http://localhost:8000/editworkaddress?id=xxxxxxxxxxuser_idxxxxxxxxxxxxxxx

Deletando Endereços (requisição GET)

URL: http://localhost:8000/deleteaddresses?id=xxxxxxxxxuser_idxxxxxxxxxxxxx

Deleta ambos os endereços.

Função de Finalização de Compra e Colocação de Pedido (requisição GET)

Após a finalização da compra, os itens devem ser removidos do carrinho.

URL: http://localhost:8000?id=xxuser_idxxx

Compra Instantânea de Produtos (requisição GET)

URL: http://localhost:8000?userid=xxuser_idxxx&pid=xxxxproduct_idxxxx

