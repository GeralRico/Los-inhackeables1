
# VivaEventos Backend

## Integrantes

| Nombre Completo | Código Estudiantil |
|---|---|
| Nombre Apellido | 2020XXXX |
| Nombre Apellido | 2020XXXX |
| Nombre Apellido | 2020XXXX |

---

# Descripción del Proyecto

VivaEventos es una plataforma de gestión de eventos y venta de boletería digital basada en una arquitectura de microservicios.

El sistema permite:

- Publicar eventos
- Gestionar aforos y stock de boletas
- Comprar tickets
- Procesar pagos mediante pasarela sandbox
- Generar tickets digitales con código QR
- Validar ingreso a eventos
- Gestionar notificaciones y trazabilidad

---

# Arquitectura General

El sistema está construido utilizando microservicios desacoplados.

## Microservicios

| Servicio | Responsabilidad |
|---|---|
| Auth Service | Autenticación y autorización |
| Event Service | Gestión de eventos |
| Order Service | Gestión de órdenes |
| Payment Service | Procesamiento de pagos |
| Ticket Service | Generación y validación QR |
| Notification Service | Envío de notificaciones |

---

# Tecnologías Utilizadas

## Backend
- Java 21
- Spring Boot
- Spring Security
- Spring Data JPA

## Base de Datos
- PostgreSQL

## Comunicación
- REST APIs
- RabbitMQ

## Seguridad
- JWT Authentication

## Infraestructura
- Docker
- Docker Compose

## Documentación API
- Swagger / OpenAPI

## Testing API
- Postman

## Pasarela de Pagos Sandbox
- Wompi Sandbox
- Stripe Test Mode
- MercadoPago Sandbox

---

# Requisitos Previos

Antes de ejecutar el proyecto se debe tener instalado:

- Docker
- Docker Compose
- Git
- Java 21 (opcional para desarrollo local)
- Maven (opcional para desarrollo local)

---

# Cómo Levantar el Proyecto

## 1. Clonar el repositorio

```bash
git clone https://github.com/usuario/vivaeventos-backend.git
```

---

## 2. Entrar al proyecto

```bash
cd vivaeventos-backend
```

---

## 3. Configurar variables de entorno

Crear un archivo:

```bash
.env
```

Basado en:

```bash
.env.example
```

---

## 4. Levantar contenedores

```bash
docker-compose up --build
```

---

# Puertos Utilizados

| Servicio | Puerto |
|---|---|
| API Gateway | 8080 |
| Auth Service | 8081 |
| Event Service | 8082 |
| Order Service | 8083 |
| Payment Service | 8084 |
| Ticket Service | 8085 |
| Notification Service | 8086 |
| PostgreSQL | 5432 |
| RabbitMQ | 5672 |
| Swagger UI | 8080/swagger-ui |

---

# Variables de Entorno

## Ejemplo `.env`

```env
# Database
DB_URL=jdbc:postgresql://postgres:5432/vivaeventos
DB_USER=postgres
DB_PASSWORD=password

# JWT
JWT_SECRET=your_secret_key

# RabbitMQ
RABBITMQ_HOST=rabbitmq
RABBITMQ_PORT=5672

# Payment Gateway
PAYMENT_API_KEY=your_payment_key
PAYMENT_PUBLIC_KEY=your_public_key

# Email
MAIL_USERNAME=test@mail.com
MAIL_PASSWORD=password
```

> Nunca subir secretos reales al repositorio.

---

# Cómo Probar el Sistema

El sistema puede probarse utilizando Swagger o Postman.

---

# Flujo de Compra Completo

## 1. Login usuario

### Endpoint

```http
POST /auth/login
```

---

## 2. Crear evento

### Endpoint

```http
POST /events
```

### Ejemplo Body

```json
{
  "name": "Concierto Rock",
  "location": "Bogotá",
  "capacity": 1000
}
```

---

## 3. Crear stock de boletas

### Endpoint

```http
POST /events/{id}/tickets
```

### Ejemplo Body

```json
{
  "type": "VIP",
  "price": 200000,
  "quantity": 100
}
```

---

## 4. Comprar ticket

### Endpoint

```http
POST /orders
```

### Ejemplo Body

```json
{
  "eventId": 1,
  "ticketType": "VIP",
  "quantity": 2
}
```

---

## 5. Simular pago sandbox

### Endpoint

```http
POST /payments
```

El sistema redireccionará a la pasarela sandbox.

---

## 6. Confirmar callback/webhook

### Endpoint

```http
POST /webhooks/payment
```

La pasarela enviará la confirmación del pago.

---

## 7. Ver ticket generado

### Endpoint

```http
GET /tickets/{id}
```

El ticket incluirá:
- Código QR único
- Información del evento
- Estado del ticket

---

# Validación QR

## Endpoint

```http
POST /tickets/validate
```

### Ejemplo Body

```json
{
  "ticketId": 15
}
```

### Resultado Esperado

- Primer uso → válido
- Segundo uso → rechazado

---

# Endpoints Principales

## Auth Service

| Método | Endpoint | Descripción |
|---|---|---|
| POST | /auth/login | Login usuario |
| POST | /auth/register | Registro usuario |

---

## Event Service

| Método | Endpoint | Descripción |
|---|---|---|
| GET | /events | Listar eventos |
| GET | /events/{id} | Obtener evento |
| POST | /events | Crear evento |
| PATCH | /events/{id} | Actualizar evento |

---

## Order Service

| Método | Endpoint | Descripción |
|---|---|---|
| POST | /orders | Crear orden |
| GET | /orders/{id} | Consultar orden |

---

## Payment Service

| Método | Endpoint | Descripción |
|---|---|---|
| POST | /payments | Procesar pago |
| POST | /webhooks/payment | Callback pasarela |

---

## Ticket Service

| Método | Endpoint | Descripción |
|---|---|---|
| GET | /tickets/{id} | Obtener ticket |
| POST | /tickets/validate | Validar QR |

---

# Swagger / OpenAPI

La documentación interactiva de la API estará disponible en:

```text
http://localhost:8080/swagger-ui/index.html
```

Desde Swagger se pueden:
- visualizar endpoints
- probar requests
- validar respuestas
- autenticarse con JWT

---

# Colección Postman

La colección Postman del proyecto se encuentra en:

```text
/postman/VivaEventos.postman_collection.json
```

---

# Estructura del Proyecto

```text
/docs
/services
/docker
/postman
README.md
docker-compose.yml
```

---

# Documentación Adicional

La documentación técnica y funcional se encuentra en:

```text
/docs
```

Incluye:
- casos de uso
- diagramas
- arquitectura
- pruebas
- decisiones arquitectónicas

---

# Estado del Proyecto

Proyecto académico desarrollado para la asignatura Desarrollo de Software III.
