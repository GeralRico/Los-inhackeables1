**Ticket Service**

**Descripción**

El Ticket Service es responsable de la generación, consulta y validación de boletas digitales dentro de la plataforma VivaEventos.

Las boletas se generan automáticamente cuando un pago es confirmado y contienen un código QR único utilizado para controlar el acceso al evento.

**Responsabilidades**

- Generar boletas digitales.
- Generar códigos QR.
- Consultar boletas.
- Validar ingreso al evento.
- Evitar el uso duplicado de boletas.
- Publicar eventos Kafka relacionados con tickets.
  **Tecnologías Utilizadas**

- Spring Boot
- PostgreSQL
- Apache Kafka
- ZXing (QR Code Generator)
- Eureka Client
- Docker

**Entidad Principal**

**Ticket**

Campos relevantes:

- id
- orderId
- eventId
- customerId
- ticketType
- uniqueCode
- qrImageUrl
- status
- validatedAt
- generatedAt

\*\*Generación de Tickets

La generación de tickets ocurre de forma automática cuando el servicio recibe un evento de pago confirmado.

Evento consumido:

PAGO_CONFIRMADO

Resultado:

- Creación del ticket.
- Generación de código QR.
- Persistencia en base de datos.
- Publicación del evento ticket.generated.

**Validación de Ingreso**

La validación se realiza utilizando el código único almacenado en el QR. Endpoint:

POST /tickets/{codigo}/validate

Validaciones realizadas:

- Existencia del ticket.
- Estado válido.
- Ticket no utilizado previamente.

**Eventos Kafka**

**Consumidos**

- PAGO_CONFIRMADO

**Publicados**

- TICKET_GENERATED
  **Reglas de Negocio**

RN-01: Cada ticket debe tener un código único.

RN-02: Una boleta solo puede utilizarse una vez.

RN-03: Todo ticket debe estar asociado a una orden válida. RN-04: El QR debe identificar unívocamente la boleta. RN-05: La validación debe registrar fecha y hora de ingreso. RN-06: Un ticket validado no puede volver a validarse.
**Requisitos No Funcionales**

- Disponibilidad.
- Escalabilidad.
- Rapidez de validación.
- Trazabilidad.
- Seguridad.

**Beneficios Arquitectónicos**

La generación de tickets está desacoplada del procesamiento de pagos mediante Apache Kafka.

Esto permite que la confirmación del pago no dependa directamente de la disponibilidad del Ticket Service.
3
