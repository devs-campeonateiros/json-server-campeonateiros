<h1 align="center">
League of Campeonateiros - API
</h1>

<p align = "center">
Este é o backend da aplicação League of Campeonateiros - um banco de dados de usuários, times e eventos!! O objetivo desta aplicação é criar uma plataforma de qualidade em grupo, utilizando todos os conhecimentos obtidos nos três módulos do curso.
</p>

<p align="center">
  <a href="#endpoints">Endpoints</a>
</p>

A API tem um total de XX endpoints, sendo em volta principalmente do usuário(time ou organizador), podendo realizar o cadastro do seu perfil, times e eventos que esta organizando ou gostaria de participar.

O URL base da API é  https://database-campeonateiros.herokuapp.com/

## Rotas que não precisam de autenticação

<h2 align ='center'> Listando times cadastrados </h2>

Nessa aplicação, o usuário sem fazer login ou se cadastrar, consegue visualizar os outros times já cadastrados na plataforma, na API podemos acesssar a lista da seguinte forma: 

`GET /users - FORMATO DA RESPOSTA - STATUS 200`

```json
[
	{
		"email": "higor@kenzie.com",
		"password": "$2a$10$1yak2vwsO2XTyMshwCkpBONT5X3Qr1KsJGWmYd9k6NlwFx9TyVdZy",
		"name": "Higor",
		"city": "Palhoça",
		"players": [],
		"url_image": "",
		"id": 1
	},
	{
		"email": "danone@email.com",
		"password": "$2a$10$zzhZ/afEpBKu7ZXRAsWsc.6bloaUUKFGlG8dHLafsD6/GfHKL2UN.",
		"name": "Danone FC",
		"city": "Palhoça",
		"id": 2
	}
]
```

`GET /events - FORMATO DA RESPOSTA - STATUS 200`

```json
[
	{
		"category": "FUTEBOL",
		"userId": 2,
		"name": "Torneio da Galera",
		"localization": "Ginásio Nazareno - Palhoça/sc",
		"date-start": "30/08/2022",
		"date-end": "30/08/2022",
		"image": "",
		"information": [],
		"id": 1
	}
]
```

<h2 align ='center'> Criação de usuário </h2>
### Cadastro

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
	"email": "danone@email.com",
	"password": "123456",
	"name": "Danone FC",
	"city": "Palhoça"
}
```
Caso o cadastro seja feito de forma correta, a resposta será assim:

`POST /users - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRhbm9uZUBlbWFpbC5jb20iLCJpYXQiOjE2NjE5MDA2NjAsImV4cCI6MTY2MTkwNDI2MCwic3ViIjoiMiJ9.ZlkLFQiR3QFk4p-g0e4CNxh-fVfudgGZ0i8JVkFUPVs",
	"user": {
		"email": "danone@email.com",
		"name": "Danone FC",
		"city": "Palhoça",
		"id": 2
	}
}
```

1. O campo "city": deve receber a cidade de origem do time cadastrado.

<h2 align = "center"> Login </h2>

```json
{
	"email": "danone@email.com",
	"password": "123456"
}
```
Caso de tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRhbm9uZUBlbWFpbC5jb20iLCJpYXQiOjE2NjE5MDA5NTUsImV4cCI6MTY2MTkwNDU1NSwic3ViIjoiMiJ9.bPm1D8tTUIrIckvrh1sVDgfTEykCObqoW13WFFgYbvg",
	"user": {
		"email": "danone@email.com",
		"name": "Danone FC",
		"city": "Palhoça",
		"id": 2
	}
}
```

Com esta resposta, temos duas informações importantes, token e user, sendo que ambos podem ser guardados no localStorage para fazer a gestão do usuario no Frontend.

## Rotas que necessitam de autorização

Rotas que necessitam de autorização(token) deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Criar Evento (token) </h2>

`Post /events - FORMATO DA REQUISIÇÃO`

```json
{
  "category": "FUTEBOL",
  "userId": 2,
  "name": "Torneio da Galera",
  "localization": "Ginásio Nazareno - Palhoça/sc",
  "date-start": "30/08/2022",
  "date-end": "30/08/2022",
  "image": "",
  "information": []
}
```

`Post /events - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"category": "FUTEBOL",
	"userId": 2,
	"name": "Torneio da Galera",
	"localization": "Ginásio Nazareno - Palhoça/sc",
	"date-start": "30/08/2022",
	"date-end": "30/08/2022",
	"image": "",
	"information": [],
	"id": 2
}
```

1. o campo - "category" deve receber respectivamente os sequintes tipos de evento:
  - "Futebol"
  - "Voleibol"
  - "Basquete"
  
2. o campo "userId": é o ID do usuário que estiver criando o evento, pois somente ele consegue adicionar informações relacionados ao evento.





