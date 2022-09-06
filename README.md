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
      "email": "danone@email.com",
      "password": "$2a$10$1yak2vwsO2XTyMshwCkpBONT5X3Qr1KsJGWmYd9k6NlwFx9TyVdZy",
      "name": "Danone FC",
      "city": "Palhoça",
      "players": ["Cristiano", "Ronaldo", "Messi", "Neymar"],
      "url_image": "https://i.pinimg.com/564x/a2/df/be/a2dfbe8df09c969ec925b8cf1fa6ab47.jpg",
      "id": 1
    },
    {
      "email": "kenzieclub@kenzie.com",
      "password": "$2a$10$1yak2vwsO2XTyMshwCkpBONT5X3Qr1KsJGWmYd9k6NlwFx9TyVdZy",
      "name": "Danone FC",
      "city": "Palhoça",
      "players": ["Tsunode", "Wesley", "4lysson", "Vilson"],
      "url_image": "https://veja.abril.com.br/wp-content/uploads/2019/12/1.jpg",
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
		"localization": "Ginásio Nazareno - Palhoça/SC",
		"date-start": "30/08/2022",
		"date-end": "30/08/2022",
		"image": "",
		"subscription": "R$ 300,00",
		"awards": "Troféu e medalha para os campeões",
		"quantity": 8,
		"address": "Camp Now KenzieClub",
		"teams": [
			{
				"city": "Palhoça",
				"url_image": "https://thumbs.dreamstime.com/z/ilustra%C3%A7%C3%A3o-do-vetor-da-silhueta-bola-voleibol-isolada-no-branco-119929868.jpg",
				"UserId": 2
			},
			{
				"name": "Kenzie FC",
				"city": "Palhoça",
				"url_image": "https://veja.abril.com.br/wp-content/uploads/2019/12/1.jpg",
				"UserId": 3
			},
			{
				"name": "Danone FC",
				"city": "Palhoça",
				"url_image": "https://i.pinimg.com/564x/a2/df/be/a2dfbe8df09c969ec925b8cf1fa6ab47.jpg",
				"UserId": 1
			}
		],
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
	"city": "Palhoça/SC"
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
		"city": "Palhoça/SC",
		"id": 2
	}
}
```

1. O campo "city": deve receber a cidade/estado de origem do time cadastrado.

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
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRhbm9uZUBlbWFpbC5jb20iLCJpYXQiOjE2NjE5MDY0NTEsImV4cCI6MTY2MTkxMDA1MSwic3ViIjoiMSJ9.xH2G55cvVVoIf6oKF10bgG-vmuUyBfBfNeYQebxtnT0",
	"user": {
		"email": "danone@email.com",
		"name": "Danone FC",
		"city": "Palhoça/SC",
		"players": [
			"Cristiano",
			"Ronaldo",
			"Messi",
			"Neymar"
		],
		"url_image": "https://i.pinimg.com/564x/a2/df/be/a2dfbe8df09c969ec925b8cf1fa6ab47.jpg",
		"id": 1
	}
}
```

Com esta resposta, temos duas informações importantes, token e id, sendo que ambos podem ser guardados no localStorage para fazer a gestão do usuario no Frontend.

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
  "dateStart": "30/08/2022",
  "dateEnd": "30/08/2022",
}
```

`Post /events - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"category": "FUTEBOL",
	"userId": 2,
	"name": "Torneio da Galera",
	"localization": "Ginásio Nazareno - Palhoça/sc",
	"dateStart": "30/08/2022",
	"dateEnd": "30/08/2022",
	"id": 2
}
```

1. O campo - "category" deve receber respectivamente os sequintes tipos de evento:
  - "Futebol"
  - "Voleibol"
  - "Basquete"
  
2. o campo "userId": é o ID do usuário que estiver criando o evento, pois somente ele consegue adicionar informações relacionados ao evento.

<h2 align ='center'> Atualizando o Evento (token) </h2>

`Patch /events/id (id do evento a ser editado) - FORMATO DA REQUISIÇÃO`

```json
    {
    		"image": "url da imagem",
		"subscription": "R$ 300,00",
		"awards": "Troféu e medalha para os campeões",
		"quantity": 8,
		"address": "Esquina do bar Madalena"
		"teams": []
		}
```

1. O campo - "teams" serão os times inscritos no evento. Sendo que será um array de objetos com as seguintes inf. de cada time inscrito :
	- "city": cidade/estado do time inscrito;
	- "url_image": logo do time inscrito;
	- "userId: id do time inscrito.

`Patch /events - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"category": "Futebol",
	"userId": 3,
	"name": "Copa doss cria",
	"localization": "Morro do alemão",
	"dateStart": "03/09/2022",
	"dateEnd": "03/09/2022",
	"image": "",
	"subscription": "R$ 300,00",
	"awards": "Troféu e medalha para os campeões",
	"quantity": 8,
	"address": "Camp Now KenzieClub",
	"teams": [
		{
			"city": "Palhoça",
			"url_image": "https://thumbs.dreamstime.com/z/ilustra%C3%A7%C3%A3o-do-vetor-da-silhueta-bola-voleibol-isolada-no-branco-119929868.jpg",
			"UserId": 2
		},
		{
			"name": "Kenzie FC",
			"city": "Palhoça",
			"url_image": "https://veja.abril.com.br/wp-content/uploads/2019/12/1.jpg",
			"UserId": 3
		},
		{
			"name": "Danone FC",
			"city": "Palhoça",
			"url_image": "https://i.pinimg.com/564x/a2/df/be/a2dfbe8df09c969ec925b8cf1fa6ab47.jpg",
			"UserId": 1
		}
	"id": 2,
}
```

<h2 align ='center'> Deletando o Evento (token) </h2>

`Delete /events/id (id do evento a ser editado) - Não é necessário passar corpo na requisição!`

<h2 align ='center'> Atualizando o usuário (token) </h2>

`Patch /users/id (id do Usuário a ser editado) - FORMATO DA REQUISIÇÃO`

```json
{
	"players": [
		"Zezin",
		"Anão",
		"Canhotin",
		"Vissoto"
	],
	"url_image": "https://thumbs.dreamstime.com/z/ilustra%C3%A7%C3%A3o-do-vetor-da-silhueta-bola-voleibol-isolada-no-branco-119929868.jpg"
}
```

`Patch /users/id (id do Usuário a ser editado) - FORMATO DA RESPOSTA - STATUS 200`

```json

{
	"email": "canela@mail.com",
	"password": "$2a$10$l7lutElDxqAexWlpmo.OjeiI26h2fILW8rrGlW0B18YY3Xa3BjBVa",
	"name": "Só canela FC",
	"city": "São Paulo",
	"id": 3,
	"players": [
		"Zezin",
		"Anão",
		"Canhotin",
		"Vissoto"
	],
	"url_image": ""
}
```


<h2 align ='center'> Deletando o Usuário (token) </h2>

`Delete /users/id (id do Usuário a ser editado) - Não é necessário passar corpo na requisição!`

<h1>Escrito e criado por - team campeonateiros!! </h1>
