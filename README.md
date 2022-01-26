# <center>[Json-server-capstone](https://json-server-capstone.herokuapp.com/)</center>

## Endpoints

- [/users](#1)
- [/animes](#2)
- [/mylist](#3)
- [/comments](#4)
- [/avatars](#5)

## <center id="1"> Cadastro </center>

`POST /register`
`POST /signup`
`POST /users`

Qualquer um desses 3 endpoints irá cadastrar um novo usuário.
Os campos obrigatórios são os de email email e password.

`POST /signup - FORMATO DA REQUISIÇÃO`

```json
{
  "name": "jhondoe",
  "email": "jhondoe@mail.com",
  "password": "123456"
}
```

`POST /signup - FORMATO DA RESPOSTA - 200 Created`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InJvYmVydEBnbWFpbC5jb20iLCJpYXQiOjE2NDIwMzgyMTcsImV4cCI6MTY0MjA0MTgxNywic3ViIjoiMSJ9.lJR--iEy4tPaSP31MPAnnOWoKK3aeaJTTkzLWnCkiYg",
  "user": {
    "email": "jhondoe@mail.com",
    "name": "jhondoe",
    "id": 1
  }
}
```

### Possiveis erros </br>

Caso esteja tentando adicionar um novo usuário com um email que já esteja cadastrado.

`POST /signup - FORMATO DA RESPOSTA - 400 Bad Request`

```json
{
  "name": "JhonDoe",
  "email": "robson@mail.com",
  "password": "123456"
}
```

`Retorno:`

```json
"Email already exists"
```

## <center > Login </center>

`POST /login`
`POST /signin`

Qualquer um desses 2 endpoints pode ser usado para realizar login.

`POST /signin - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "robson@mail.com",
  "password": "123456"
}
```

`POST /signin - FORMATO DA RESPOSTA - 200 OK`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InJvYmVydEBnbWFpbC5jb20iLCJpYXQiOjE2NDIwMzgwNDEsImV4cCI6MTY0MjA0MTY0MSwic3ViIjoiMSJ9.hEyFlcAYVivNsX4OB-bK7yBW-abLzoBfeeVCI4FD1Yg",
  "user": {
    "email": "robson@mail.com",
    "name": "Robson",
    "id": 1
  }
}
```

### Possíveis erros

Caso email ou senha digitados estejam incorretos.

`POST /signin - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "johndoe@mail.com",
  "password": "000404"
}
```

`POST /signin - FORMATO DA RESPOSTA - 400 Bad Request`

Caso email incorreto

```json
"Cannot find user"
```

Caso password incorreto

```json
"Incorrect password"
```

## <center > Atualizar dados do usuário </center>

E possível atualizar qualquer dado do usuário sendo necessário passar o número do id do usuário no caminho da requisição. Esta rota necessita de autenticação ,todas as rotas que necessitam de autenticação e necessário passar o accessToken no header da requisição.
</br>`Exemplo:`

{
"headers": {
"Authorization": `Bearer: ${accessToken}`
}
}

`PATCH /users/1 - FORMATO DA REQUISIÇÃO`

```json
{
  "name": "Robson",
  "email": "robson@mail.com",
  "password": "654321"
}
```

`PATCH /users/1 - FORMATO DA RESPOSTA - 200 OK`

```json
{
  "email": "robson@mail.com",
  "password": "$2a$10$3svpjhnOoDOPpc4fnPYNkuDRIJbGkCPXLxNmne0bqemFy.fErAZUu",
  "name": "Robson",
  "id": 1
}
```

### Possíveis erros

> Caso id não pertença ao usuário. </br>`401 Unauthorized`

```json
"Cannot read properties of undefined (reading 'id')"
```

> Caso id não tenha sido passado na requisição. </br> `403 Forbidden`

```json
"Private resource access: entity must have a reference to the owner id"
```

> Caso acessToken não tenha sido passado na requisição. </br> `401 Unauthorized`

```json
"Missing token"
```

## <center id="2"> Animes </center>

Lista todos os animes cadastrados, sendo 56 animes no momento. Todos os usuários tem acesso a está rota, porém somente usuários logados podem comentar e avaliar os animes.

`GET /animes - FORMATO DA RESPOSTA - 200 OK`</br>

```json
[
  {
    "id": 1,
    "title": "Naruto: Shippuuden",
    "category": ["Ação", "Angústia", "Comédia", "Artes marciais"],
    "rate": [],
    "banner_url": "https://media.kitsu.io/anime/cover_images/1555/original.jpg",
    "image-url": "https://media.kitsu.io/anime/poster_images/1555/large.jpg",
    "original": "Naruto: Shippuden",
    "status": "Concluído",
    "launch_date": "2007",
    "studio": "Pierrot, Studio Pierrot",
    "synopsis": "Já se passaram dois anos e meio desde que Naruto Uzumaki deixou Konohagakure, a Vila Oculta da Folha, para um treinamento intenso após os eventos que alimentaram seu desejo de ser mais forte. Agora a Akatsuki, a misteriosa organização de ninjas desonestos de elite, está se aproximando de seu grande plano que pode ameaçar a segurança de todo o mundo shinobi. Embora Naruto seja mais velho e eventos sinistros surjam no horizonte, ele mudou pouco em personalidade - ainda indisciplinado e infantil - embora agora esteja muito mais confiante e possua uma determinação ainda maior para proteger seus amigos e sua casa. Aconteça o que acontecer, Naruto seguirá lutando pelo que é importante para ele, mesmo às custas de seu próprio corpo, na continuação da saga sobre o menino que deseja se tornar Hokage. (Fonte: MAL Rewrite)."
  },
  {
    "id": 2,
    "title": "One Piece",
    "category": ["Ação", "Crime", "Comédia", "Pirata"],
    "rate": [],
    "banner_url": "https://media.kitsu.io/anime/12/cover_image/21ecb556255bd46b95aea4779d19789f.jpg",
    "image_url": "https://media.kitsu.io/anime/poster_images/12/large.jpg",
    "original": "One Piece",
    "status": "Em exibição",
    "launch_date": "1999",
    "studio": "Toei Animation",
    "synopsis": "Gol D. Roger era conhecido como o 'Rei dos Piratas', o ser mais forte e mais infame que navegou na Grand Line. A captura e morte de Roger pelo Governo Mundial trouxe uma mudança em todo o mundo. Suas últimas palavras antes de sua morte revelaram a existência do maior tesouro do mundo, One Piece. Foi essa revelação que trouxe a Grande Era dos Piratas, homens que sonhavam em encontrar One Piece - que promete uma quantidade ilimitada de riqueza e fama - e possivelmente o auge da glória e o título de Rei dos Piratas. Entra Monkey D. Luffy, um garoto de 17 anos que desafia sua definição padrão de pirata. Em vez da persona popular de um pirata perverso, endurecido e desdentado saqueando aldeias por diversão, a razão de Luffy ser um pirata é de pura admiração: o pensamento de uma aventura emocionante que o leva a pessoas intrigantes e, finalmente, ao tesouro prometido. Seguindo os passos de seu herói de infância, Luffy e sua tripulação viajam pela Grand Line, vivenciando aventuras loucas, desvendando mistérios sombrios e lutando contra inimigos fortes, tudo para alcançar a mais cobiçada de todas as fortunas – One Piece."
  }
]
```

## <center id="3"> Adicionando animes a lista </center>

Para adicionar um anime a lista e necessário passar o corpo do anime selecionado, adicionando a propriedade "urserId" com o id do usuário.

`POST /mylist - FORMATO DA RESPOSTA - 201 Created`</br>

```json
{
  "id": 1,
  "title": "Naruto: Shippuuden",
  "category": ["Ação", "Angústia", "Comédia", "Artes marciais"],
  "rate": [],
  "banner_url": "https://media.kitsu.io/anime/cover_images/1555/original.jpg",
  "image-url": "https://media.kitsu.io/anime/poster_images/1555/large.jpg",
  "original": "Naruto: Shippuden",
  "status": "Concluído",
  "launch_date": "2007",
  "studio": "Pierrot, Studio Pierrot",
  "synopsis": "Já se passaram dois anos e meio desde que Naruto Uzumaki deixou Konohagakure, a Vila Oculta da Folha, para um treinamento intenso após os eventos que alimentaram seu desejo de ser mais forte. Agora a Akatsuki, a misteriosa organização de ninjas desonestos de elite, está se aproximando de seu grande plano que pode ameaçar a segurança de todo o mundo shinobi. Embora Naruto seja mais velho e eventos sinistros surjam no horizonte, ele mudou pouco em personalidade - ainda indisciplinado e infantil - embora agora esteja muito mais confiante e possua uma determinação ainda maior para proteger seus amigos e sua casa. Aconteça o que acontecer, Naruto seguirá lutando pelo que é importante para ele, mesmo às custas de seu próprio corpo, na continuação da saga sobre o menino que deseja se tornar Hokage.",
  "userId": 1
}
```

## <center > Listando meus animes </center>

Para listar os seus animes adicionados e necessário passar o userId no corpo da requisição.
Ex: users/:userId/mylist

`GET users/1/mylist - FORMATO DA RESPOSTA - 200 OK`</br>

```json
{
  "id": 1,
  "title": "Naruto: Shippuuden",
  "category": ["Ação", "Angústia", "Comédia", "Artes marciais"],
  "rate": [],
  "banner_url": "https://media.kitsu.io/anime/cover_images/1555/original.jpg",
  "image-url": "https://media.kitsu.io/anime/poster_images/1555/large.jpg",
  "original": "Naruto: Shippuden",
  "status": "Concluído",
  "launch_date": "2007",
  "studio": "Pierrot, Studio Pierrot",
  "synopsis": "Já se passaram dois anos e meio desde que Naruto Uzumaki deixou Konohagakure, a Vila Oculta da Folha, para um treinamento intenso após os eventos que alimentaram seu desejo de ser mais forte. Agora a Akatsuki, a misteriosa organização de ninjas desonestos de elite, está se aproximando de seu grande plano que pode ameaçar a segurança de todo o mundo shinobi. Embora Naruto seja mais velho e eventos sinistros surjam no horizonte, ele mudou pouco em personalidade - ainda indisciplinado e infantil - embora agora esteja muito mais confiante e possua uma determinação ainda maior para proteger seus amigos e sua casa. Aconteça o que acontecer, Naruto seguirá lutando pelo que é importante para ele, mesmo às custas de seu próprio corpo, na continuação da saga sobre o menino que deseja se tornar Hokage.",
  "userId": 1
}
```

## <center > Removendo animes da lista </center>

Para remover animes da lista é necessário passar id do item selecionado no caminho da requisição.

`DELETE /mylist/1 - FORMATO DA RESPOSTA - 200 OK`</br>

```json
{}
```

## <center id="4"> Adicionando comentários </center>

Para poder adicionar um comentário e necessário o usuário estar logado. Contendo o 'userId' ,'animeId': contendo o id do anime selecionado.

`POST /comments - FORMATO DA RESPOSTA - 201 Created`</br>

```json
{
  "userId": 1,
  "animeId": 55,
  "comment": "Esse ainda não assisti"
}
```

## <center > Atualizar comentário </center>

Para atualizar um comentário e necessário passar o id do comentário no caminho da requisição

`PATCH/comments/1 - FORMATO DA REQUISIÇÃO - 200 OK`</br>

```json
{
  "comment": "Assisti ele ontem, muito bom!!"
}
```

## <center > Remover comentário </center>

Para remover um comentário e necessário passar o id do comentário selecionado no caminho da requisição.

`DELETE/comments/1 - FORMATO DA REQUISIÇÃO - 200 OK`</br>

```json
{
  "comment": "Assisti ele ontem, muito bom!!"
}
```

## <center > Listar comentários </center>

Para listar os comentários.
`GET/comments - FORMATO DA REQUISIÇÃO - 200 OK`</br>

```json
{
  "userId": 1,
  "animeId": 55,
  "comment": "Esse ainda não assisti"
}
```

## <center > Listar um comentário em especifíco </center>

Para listar um comentários de um anime em especifíco e necessário passar o id do anime no qual esteja procurando no caminho da requisição.

`GET/comments?animeId=55 - FORMATO DA REQUISIÇÃO - 200 OK`</br>

```json
{
  "userId": 1,
  "animeId": 55,
  "comment": "Esse ainda não assisti"
}
```

## <center id="5"> Avatars </center>

Para listar os avatares padrões de usuário.

`GET/avatars - FORMATO DA REQUISIÇÃO - 200 OK`</br>

```json
[
  "https://icon-library.com/images/anime-icon/anime-icon-9.jpg",
  "http://pm1.narvii.com/6861/44017694789ca7409a0a9a30a8c0be4a7e2bd9f8r1-800-713v2_00.jpg",
  "https://icon-library.com/images/cool-anime-icon/cool-anime-icon-9.jpg",
  "https://wallpapercave.com/uwp/uwp1426727.jpeg"
]
```
