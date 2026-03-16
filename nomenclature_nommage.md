
# Nomenclature de Nommage – Projet Java / Spring Boot / DDD / Hexagonal

## 1. Règles générales

### Style global
- **Classes Java** : PascalCase
- **Méthodes / variables** : camelCase
- **Constantes** : UPPER_SNAKE_CASE
- **Packages** : lowercase uniquement
- **Fichiers SQL / Liquibase** : snake_case
- **Endpoints REST** : kebab-case

---

## 2. Domain (DDD)

### Entities
```
<NomAggregate>
```
Exemples : `User`, `Order`, `Invoice`

### Value Objects
```
<Concept>Value
```
Exemples : `EmailAddress`, `Price`, `PhoneNumber`

### Domain Events
```
<Aggregate><Action>DomainEvent
```
Exemples : `UserRegisteredDomainEvent`, `OrderPaidDomainEvent`

### Domain Services
```
<Concept>DomainService
```
Exemples : `PricingDomainService`, `FraudDetectionDomainService`

### Policies
```
<Invariant>Policy
```
Exemples : `EmailFormatPolicy`, `UserAgePolicy`

### Exceptions métier
```
<Concept>Exception
```
Exemples : `UserNotFoundException`, `BusinessRuleViolationException`

### Ports IN (Use Cases)
```
<Verbe><Noun>UseCase
```
Exemples : `CreateUserUseCase`, `GetUserByIdUseCase`

### Ports OUT
```
<Concept>Port
```
Exemples : `UserRepositoryPort`, `PaymentGatewayPort`

---

## 3. Application Layer

### Command Use Cases
```
<Verbe><Noun>Command
<Verbe><Noun>CommandHandler
```
Ex : `CreateUserCommand`, `CreateUserCommandHandler`

### Query Use Cases
```
<Verbe><Noun>Query
<Verbe><Noun>QueryHandler
```
Ex : `GetUserByIdQuery`, `GetUserByIdQueryHandler`

### Application Events
```
<Concept><Action>ApplicationEvent
```
Ex : `UserCreatedApplicationEvent`

---

## 4. Infrastructure Layer

### Adapters IN (API REST)

#### Controllers
```
<Module>Controller
<Module><Version>Controller
```
Ex : `UserController`, `OrderV1Controller`

#### DTO API
Entrée :
```
<Verbe><Noun>Request
```
Sortie :
```
<Noun>Response
<Noun>Dto
```

#### API Mappers
```
<Module>ApiMapper
```
Ex : `UserApiMapper`

---

### Adapters OUT (DB, systèmes externes)

#### JPA Entities
```
<Nom>JpaEntity
```

#### Repositories Spring Data
```
<Aggregate>JpaRepository
```

#### JPA Adapter
```
<Aggregate>JpaAdapter
```

#### JPA Mapper
```
<Aggregate>JpaMapper
```

#### Clients externes
```
<Provider><Resource>Client
<Provider><Concept>Adapter
<Provider><Concept>Dto
```
Ex : `StripePaymentClient`, `OpenAiTextGenerationAdapter`

---

## 5. Config Layer
```
<Concept>Config
```
Ex : `SecurityConfig`, `WebMvcConfig`, `JacksonConfig`

---

## 6. Bootstrap
```
<Application>Bootstrap
<Concept>Initializer
```
Ex : `ApplicationBootstrap`, `CacheInitializer`

---

## 7. Testing
Unit tests :
```
<ClasseTestée>Test
```
Integration tests :
```
<ClasseTestée>IT
```

---

## 8. SQL / Liquibase

### Fichiers de migration
```
V<version>__<description>.sql
```

### Tables
snake_case singulier

### Colonnes
snake_case

---

## 9. REST API Routing
- kebab-case
- ressources au pluriel
- version en tête d’URL

Exemples :
```
GET /v1/users
POST /v1/users
GET /v1/users/{id}
GET /v1/orders/{id}/items
```
