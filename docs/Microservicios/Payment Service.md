**Payment Service**

**Descripción**

El Payment Service es responsable de gestionar el procesamiento de pagos dentro de la plataforma VivaEventos.

Este servicio se integra con Wompi Sandbox para la creación de transacciones, recepción de confirmaciones mediante webhooks, gestión de devoluciones y aplicación de códigos promocionales.

La arquitectura implementada permite manejar pagos pendientes, aprobados o rechazados sin afectar la disponibilidad de otros servicios.

**Responsabilidades**

- Procesar pagos.
- Integrarse con Wompi.
- Validar webhooks.
- Gestionar devoluciones.
- Aplicar códigos promocionales.
- Detectar compras abandonadas.
- Publicar eventos Kafka.
- Ejecutar conciliación de transacciones.

**Tecnologías Utilizadas**

- Spring Boot
- PostgreSQL
- Apache Kafka
- Spring Security
- Wompi Sandbox
- Eureka Client
- Docker

**Entidad Principal**

**Payment**

Representa una transacción económica asociada a una orden. Campos relevantes:

- id
- orderId
- wompiTransactionId
- reference
- amountInCents
- currency
- status
- paymentMethodType
- customerEmail
- createdAt
- updatedAt

**Estados de Pago**

**PENDIENTE**

La transacción fue creada y se encuentra esperando confirmación por parte de Wompi. **APROBADO**

La transacción fue confirmada exitosamente.

**FALLIDO**

La transacción presentó un error durante el procesamiento.

**DECLINADO**

La transacción fue rechazada por la pasarela o entidad financiera.

**Integración Externa**

**Wompi Sandbox**

Se utiliza para:

- Crear transacciones.
- Consultar estados.
- Recibir confirmaciones.
- Gestionar devoluciones.

**Eventos de Negocio**

**Publicados**

- PAGO_CONFIRMADO
- PAGO_FALLIDO
- DEVOLUCION_SOLICITADA
- COMPRA_ABANDONADA

**Consumidos**

- ORDEN_LISTA_PARA_PAGO![](Aspose.Words.f2a808d8-4e31-4258-ad5f-446bfedeb44c.006.png)

**Reglas de Negocio**

RN-01: Toda transacción debe tener una referencia única.

RN-02: Los pagos inician en estado PENDIENTE.

RN-03: Un pago aprobado no puede volver a estado pendiente.

RN-04: La confirmación oficial proviene únicamente de Wompi mediante webhook. RN-05: Las devoluciones deben quedar registradas y auditadas.

RN-06: Los códigos promocionales deben validarse antes de iniciar el pago.

**Requisitos No Funcionales**

- Disponibilidad.
- Escalabilidad.
- Trazabilidad.
- Integridad de datos.
- Seguridad.

**Beneficios Arquitectónicos**

El uso de Kafka permite desacoplar el procesamiento de pagos de la generación de tickets y del envío de notificaciones.

De esta manera, una falla temporal en Notification Service o Ticket Service no afecta la confirmación del pago.
