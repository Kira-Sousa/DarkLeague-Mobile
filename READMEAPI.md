# REST API - DarkLeague

#### **Introdução**

A API do DarkLeague oferece acesso eficiente a informações sobre cartas colecionáveis (TCG), utilizadores, binders, mercado e notificações. Desenvolvida para integração com a aplicação móvel Android, a API fornece dados atualizados em tempo real, permitindo a gestão de coleções, compras e interações sociais.

Os dados são entregues em formato JSON, garantindo respostas consistentes e facilitando a integração.

---

## **Utilizadores (Users)**

### Listar Todos os Utilizadores

- **URL:**
  `/api/users`

- **METHOD:**
  `GET`

- **SUCCESS RESPONSE:**
```json
[
  {
    "id": 1,
    "username": "AshKetchum",
    "email": "ash@poke.com",
    "rankingNome": "Mestre",
    "rankingNum": 1500,
    "tipoFavorito": "Fogo",
    "tipoUser": "Jogador"
  }
]

```

* **ERROR RESPONSE:**

```json
{
  "status": 500,
  "message": "An unexpected error occurred.",
  "timestamp": "2024-12-22T10:00:00"
}

```

* **SAMPLE CALL:**

```kotlin
@GET("users")
suspend fun getUsers(): List<UserDTO>

```

### Obter Utilizador por ID

* **URL:**
`/api/users/{id}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`id: [integer]`


* **SUCCESS RESPONSE:**

```json
{
  "id": 1,
  "username": "AshKetchum",
  "email": "ash@poke.com",
  "rankingNome": "Mestre",
  "rankingNum": 1500,
  "tipoFavorito": "Fogo",
  "tipoUser": "Jogador"
}

```

* **ERROR RESPONSE:**

```json
{
  "status": 404,
  "message": "User not found with id: 1",
  "timestamp": "2024-12-22T10:00:00"
}

```

* **SAMPLE CALL:**

```kotlin
@GET("users/{id}")
suspend fun getUserById(@Path("id") id: Long): UserDTO

```

### Registar Utilizador

* **URL:**
`/api/users/register`
* **METHOD:**
`POST`
* **REQUEST BODY:**

```json
{
  "username": "Misty",
  "email": "misty@gym.com",
  "password": "Password123!",
  "tipoFavorito": "Água"
}

```

* **SUCCESS RESPONSE:**

```json
{
  "id": 2,
  "username": "Misty",
  "email": "misty@gym.com",
  "rankingNome": "Iniciante",
  "rankingNum": 0,
  "tipoFavorito": "Água",
  "tipoUser": "Jogador"
}

```

* **ERROR RESPONSE:**

```json
{
  "status": 409,
  "message": "Email already in use",
  "timestamp": "2024-12-22T10:00:00"
}

```

* **SAMPLE CALL:**

```kotlin
@POST("users/register")
suspend fun register(@Body user: User): UserDTO

```

### Login

* **URL:**
`/api/users/login`
* **METHOD:**
`POST`
* **REQUEST BODY:**

```json
{
  "email": "ash@poke.com",
  "password": "Password123!"
}

```

* **SUCCESS RESPONSE:**

```json
{
  "id": 1,
  "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ..."
}

```

* **ERROR RESPONSE:**

```json
{
  "status": 401,
  "message": "Invalid password",
  "timestamp": "2024-12-22T10:00:00"
}

```

* **SAMPLE CALL:**

```kotlin
@POST("users/login")
suspend fun login(@Body request: LoginRequestDTO): LoginResponseDTO

```

---

## **Cartas (Cards)**

### Listar Todas as Cartas

* **URL:**
`/api/cartas`
* **METHOD:**
`GET`
* **SUCCESS RESPONSE:**

```json
[
  {
    "id": 101,
    "nome": "Charizard",
    "conjunto": "Base Set",
    "raridade": "Rare Holo",
    "imagem": "charizard_base.jpg",
    "precoAtual": 250.50,
    "tipoNome": "Fogo"
  }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("cartas")
suspend fun getAllCartas(): List<CartaDTO>

```

### Obter Carta por ID

* **URL:**
`/api/cartas/{id}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`id: [integer]`


* **SUCCESS RESPONSE:**

```json
{
  "id": 101,
  "nome": "Charizard",
  "conjunto": "Base Set",
  "raridade": "Rare Holo",
  "imagem": "charizard_base.jpg",
  "precoAtual": 250.50,
  "tipoNome": "Fogo"
}

```

* **ERROR RESPONSE:**

```json
{
  "status": 404,
  "message": "Carta com id 101 não encontrada",
  "timestamp": "2024-12-22T10:00:00"
}

```

* **SAMPLE CALL:**

```kotlin
@GET("cartas/{id}")
suspend fun getCartaById(@Path("id") id: Int): CartaDTO

```

### Listar Cartas por Conjunto

* **URL:**
`/api/cartas/conjunto/{nomeConjunto}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`nomeConjunto: [string]`


* **SAMPLE CALL:**

```kotlin
@GET("cartas/conjunto/{nome}")
suspend fun getCartasByConjunto(@Path("nome") nome: String): List<CartaDTO>

```

---

## **Binders (Pastas)**

### Listar Binders do Utilizador

* **URL:**
`/api/binders/user/{userId}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`userId: [integer]`


* **SUCCESS RESPONSE:**

```json
[
  {
    "id": 5,
    "name": "Melhores Cartas",
    "userId": 1,
    "previewImages": [
       "charizard.jpg",
       "blastoise.jpg",
       "pikachu.jpg",
       "mewtwo.jpg"
    ]
  }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("binders/user/{userId}")
suspend fun getBindersByUserId(@Path("userId") userId: Long): List<BinderDTO>

```

### Criar Binder

* **URL:**
`/api/binders`
* **METHOD:**
`POST`
* **REQUEST BODY:**

```json
{
  "name": "Trocas",
  "userId": 1
}

```

* **SUCCESS RESPONSE:**

```json
{
  "id": 6,
  "name": "Trocas",
  "userId": 1,
  "previewImages": []
}

```

* **SAMPLE CALL:**

```kotlin
@POST("binders")
suspend fun createBinder(@Body binder: BinderDTO): BinderDTO

```

### Apagar Binder

* **URL:**
`/api/binders/{id}`
* **METHOD:**
`DELETE`
* **URL Parameters:**
* Required:
`id: [integer]`


* **SUCCESS RESPONSE:**
*(Empty Body with status 200 OK)*
* **ERROR RESPONSE:**

```json
{
  "status": 404,
  "message": "Binder not found",
  "timestamp": "2024-12-22T10:00:00"
}

```

* **SAMPLE CALL:**

```kotlin
@DELETE("binders/{id}")
suspend fun deleteBinder(@Path("id") id: Long): Response<Unit>

```

---

## **Conteúdo dos Binders (BC)**

### Ver Cartas de um Binder

* **URL:**
`/api/bc/binder/{binderId}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`binderId: [integer]`


* **SUCCESS RESPONSE:**

```json
[
  {
    "id": 50,
    "binderId": 5,
    "cartaDTO": {
        "id": 101,
        "nome": "Charizard",
        "conjunto": "Base Set",
        "raridade": "Rare Holo",
        "imagem": "charizard_base.jpg",
        "precoAtual": 250.50,
        "tipoNome": "Fogo"
    }
  }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("bc/binder/{binderId}")
suspend fun getCartasByBinder(@Path("binderId") binderId: Long): List<BCDTO>

```

### Adicionar Carta ao Binder

* **URL:**
`/api/bc`
* **METHOD:**
`POST`
* **REQUEST BODY:**

```json
{
  "binderId": 5,
  "cartaId": 101
}

```

* **SUCCESS RESPONSE:**

```json
{
  "id": 51,
  "binderId": 5,
  "cartaDTO": {
     "id": 101,
     "nome": "Charizard",
     ...
  }
}

```

* **SAMPLE CALL:**

```kotlin
@POST("bc")
suspend fun addCardToBinder(@Body request: BCRequest): BCDTO

```

---

## **Favoritos**

### Listar Favoritos do Utilizador

* **URL:**
`/api/favoritos/user/{userId}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`userId: [integer]`


* **SUCCESS RESPONSE:**

```json
[
  {
    "id": 10,
    "userId": 1,
    "cartaDTO": {
        "id": 101,
        "nome": "Charizard",
        "conjunto": "Base Set",
        "raridade": "Rare Holo",
        "imagem": "charizard_base.jpg",
        "precoAtual": 250.50,
        "tipoNome": "Fogo"
    }
  }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("favoritos/user/{userId}")
suspend fun getFavoritos(@Path("userId") userId: Long): List<FavoritoDTO>

```

### Adicionar Favorito

* **URL:**
`/api/favoritos`
* **METHOD:**
`POST`
* **REQUEST BODY:**

```json
{
  "userId": 1,
  "cartaId": 101
}

```

* **SUCCESS RESPONSE:**

```json
{
  "id": 11,
  "userId": 1,
  "cartaDTO": { ... }
}

```

* **SAMPLE CALL:**

```kotlin
@POST("favoritos")
suspend fun addFavorito(@Body req: FavoritoRequest): FavoritoDTO

```

### Remover Favorito

* **URL:**
`/api/favoritos/user/{userId}/carta/{cartaId}`
* **METHOD:**
`DELETE`
* **URL Parameters:**
* Required:
`userId: [integer]`, `cartaId: [integer]`


* **SUCCESS RESPONSE:**
*(Empty Body with status 200 OK)*
* **ERROR RESPONSE:**

```json
{
  "status": 404,
  "message": "Favorito not found",
  "timestamp": "2024-12-22T10:00:00"
}

```

* **SAMPLE CALL:**

```kotlin
@DELETE("favoritos/user/{userId}/carta/{cartaId}")
suspend fun removeFavorito(@Path("userId") uId: Long, @Path("cartaId") cId: Long): Response<Unit>

```

---

## **Notificações & Mercado**

### Listar Notificações

* **URL:**
`/api/notificacoes/user/{userId}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`userId: [integer]`


* **SUCCESS RESPONSE:**

```json
[
  {
    "id": 20,
    "mensagem": "Compraste a carta Charizard!",
    "status": "NOVA",
    "data": "2024-12-22T10:00:00",
    "tipoConvite": 99,
    "jogador1Nome": "AshKetchum",
    "jogador2Nome": "",
    "localNome": ""
  }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("notificacoes/user/{userId}")
suspend fun getNotificacoes(@Path("userId") userId: Long): List<NotificacaoDTO>

```

### Comprar Carta (Gerar Notificação)

* **URL:**
`/api/notificacoes/buy`
* **METHOD:**
`POST`
* **REQUEST BODY:**

```json
{
  "userId": 1,
  "cartaId": 101
}

```

* **SUCCESS RESPONSE:**

```json
{
  "id": 21,
  "mensagem": "Compraste a carta Pikachu!",
  "status": "NOVA",
  "data": "2024-12-22T10:05:00",
  "tipoConvite": 99,
  "jogador1Nome": "AshKetchum",
  "jogador2Nome": "",
  "localNome": ""
}

```

* **SAMPLE CALL:**

```kotlin
@POST("notificacoes/buy")
suspend fun comprarCarta(@Body req: CompraRequest): NotificacaoDTO

```

---

## **Tipos & Locais**

### Listar Tipos

* **URL:**
`/api/tipos`
* **METHOD:**
`GET`
* **SUCCESS RESPONSE:**

```json
[
  { "id": 1, "nome": "Fogo" },
  { "id": 2, "nome": "Água" }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("tipos")
suspend fun getAllTipos(): List<Tipo>

```

### Obter Tipo por ID

* **URL:**
`/api/tipos/{id}`
* **METHOD:**
`GET`
* **SUCCESS RESPONSE:**

```json
{ "id": 1, "nome": "Fogo" }

```

### Listar Locais

* **URL:**
`/api/locais`
* **METHOD:**
`GET`
* **SUCCESS RESPONSE:**

```json
[
  {
    "id": 1,
    "nome": "Arena Lisboa",
    "latitude": 38.7,
    "longitude": -9.1,
    "imagem": "arena.jpg"
  }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("locais")
suspend fun getAllLocais(): List<Local>

```

---

## **Histórico de Preços**

### Obter Histórico de uma Carta

* **URL:**
`/api/historico/carta/{cartaId}`
* **METHOD:**
`GET`
* **URL Parameters:**
* Required:
`cartaId: [integer]`


* **SUCCESS RESPONSE:**

```json
[
  { "data": "2024-01-01", "preco": 200.00 },
  { "data": "2024-02-01", "preco": 250.50 }
]

```

* **SAMPLE CALL:**

```kotlin
@GET("historico/carta/{cartaId}")
suspend fun getHistoricoByCarta(@Path("cartaId") id: Long): List<HistoricoPrecoDTO>

```

```

