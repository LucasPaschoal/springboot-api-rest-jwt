#  AuthWichProducts

API REST desenvolvida em **Spring Boot**, com **autenticação JWT** e **gerenciamento de produtos e usuários**.  
O projeto demonstra uma arquitetura limpa em camadas, integração com **PostgreSQL**, segurança com **Spring Security** e uso de **JPA/Hibernate** para persistência de dados.

---

##  Tecnologias Utilizadas

- **Spring Boot 3.x**
- **Spring Security (JWT)**
- **Spring Data JPA / Hibernate**
- **PostgreSQL**
- **Maven**
- **Java 17**

---

##  Arquitetura do Projeto

com.example.authwichproducts/ <br>
├── controller/ # Controladores REST (endpoints da API) <br>
├── model/ # Entidades JPA (Usuario, Produto) <br>
├── repository/ # Interfaces JpaRepository <br>
├── service/ # Regras de negócio (Usuário, Produto) <br>
├── security/ # Configurações e filtros JWT <br>
├── exceptions/ # Tratamento global de erros <br>
└── AuthWichProductsApplication.java <br>

yaml
Copiar código

**Padrão:** Arquitetura em camadas → `Controller → Service → Repository → Model`

---

## ⚙️ Configuração do Banco de Dados

Arquivo `application.properties`:

```properties
server.port=8081

spring.datasource.url=jdbc:postgresql://localhost:5432/meubanco
spring.datasource.username=SEU-USUARIO
spring.datasource.password=SUA-SENHA
spring.datasource.driver-class-name=org.postgresql.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```
 Altere as credenciais de banco conforme o seu ambiente.

 Endpoints Principais
 Autenticação
POST /auth/register
Registra um novo usuário.
Body:

json
Copiar código
{
  "username": "usuario",
  "password": "senha"
}
POST /auth/login
Autentica o usuário e retorna o token JWT.
Body:

json
Copiar código
```
{
  "username": "usuario",
  "password": "senha"
}
```
Resposta:

json
Copiar código
```
{
  "token": "jwt_token_aqui"
}
```
## 🛒 Produtos (requer JWT)
GET /api/produtos
Lista todos os produtos.

GET /api/produtos/{id}
Retorna um produto específico pelo ID.

POST /api/produtos
Cria um novo produto.
Body:

json
Copiar código
```
{
  "nome": "Produto Teste",
  "preco": 99.99
}
```
DELETE /api/produtos/{id}
Remove um produto existente.

##  Todos os endpoints /api/** exigem o header:

makefile
Copiar código
Authorization: Bearer <seu_token_jwt>
##  Conceitos Aplicados
JWT Authentication → autenticação stateless via token

Spring Security → controle de acesso e filtros

Camadas desacopladas → responsabilidades bem definidas

JPA/Hibernate → ORM e persistência

Tratamento Global de Exceções → respostas JSON padronizadas

##  Como Executar
Pré-requisitos
Java 17+

PostgreSQL rodando

Maven instalado

Passos

bash
Copiar código
```
# Clonar repositório
git clone https://github.com/seu-usuario/authWichProducts.git
cd authWichProducts

# Criar banco de dados
psql -U postgres -c "CREATE DATABASE meubanco;"

# Rodar o projeto
mvn spring-boot:run
```
A aplicação será iniciada em:

http://localhost:8081
