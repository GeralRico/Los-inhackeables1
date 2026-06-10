## **Arquitectura de Software – VivaEventos** 

## **1. Introducción** 

VivaEventos es una plataforma de gestión de eventos y venta de boletería diseñada para permitir a organizadores publicar eventos, administrar aforos, vender entradas, procesar pagos, generar boletas digitales con código QR y controlar el acceso a los eventos. 

La solución fue construida utilizando una arquitectura basada en microservicios con el objetivo de garantizar escalabilidad, mantenibilidad, disponibilidad y desacoplamiento entre los diferentes componentes del sistema. 

La arquitectura propuesta permite soportar picos de demanda durante la apertura de ventas, integrarse con servicios externos como pasarelas de pago y sistemas de correo, y mantener la trazabilidad completa de las operaciones realizadas por los usuarios. 

## **2. Estilo Arquitectónico** 

El sistema adopta una arquitectura de microservicios basada en eventos. 

Cada microservicio posee una responsabilidad claramente definida, una base de datos propia y se comunica con otros servicios mediante APIs REST y eventos asíncronos utilizando Apache Kafka. 

Principios aplicados: 

- Single Responsibility Principle (SRP) 

- Database per Service 

- Event Driven Architecture 

- API Gateway Pattern 

- Service Discovery Pattern 

- Externalized Configuration 

- Loose Coupling 

## **3. Arquitectura General** 

```
                           ┌─────────────────┐
                           │    Frontend     │
                           └────────┬────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │     API Gateway     │
                         └─────────┬───────────┘
```

1 

**==> picture [336 x 493] intentionally omitted <==**

**----- Start of picture text -----**<br>
                                   │<br>            ┌──────────────────────┼──────────────────────┐<br>            │                      │                      │<br>            ▼                      ▼                      ▼<br>     ┌─────────────┐      ┌─────────────┐      ┌─────────────┐<br>     │ Auth Service│      │Event Service│      │Order Service│<br>     └──────┬──────┘      └──────┬──────┘      └──────┬──────┘<br>            │                    │                    │<br>            │                    │                    │<br>            ▼                    ▼                    ▼<br>     ┌─────────────┐      ┌─────────────┐      ┌─────────────┐<br>     │Payment Svc  │      │Ticket Svc   │      │Notification │<br>     └──────┬──────┘      └──────┬──────┘      │   Service   │<br>            │                    │             └─────────────┘<br>            │                    │<br>            ▼                    ▼<br>         Wompi               QR Codes<br>            ▲<br>            │<br>            ▼<br>     ┌─────────────────┐<br>     │ Kafka Messaging │<br>     └─────────────────┘<br>            ▲<br>            │<br>            ▼<br>     ┌─────────────────┐<br>     │ Eureka Server   │<br>     └─────────────────┘<br>**----- End of picture text -----**<br>


## **4. Componentes de la Arquitectura** 

## **4.1 API Gateway** 

Es el punto de entrada único para todas las solicitudes realizadas por los clientes. 

Responsabilidades: 

- Enrutamiento de solicitudes. 

- Validación de JWT. 

2 

- Control de acceso. 

- Comunicación con Auth Service. 

- Centralización de seguridad. 

Beneficios: 

- Oculta la complejidad interna. 

- Reduce el acoplamiento entre clientes y servicios. 

- Facilita la aplicación de políticas de seguridad. 

## **4.2 Discovery Server** 

Implementado mediante Netflix Eureka. 

Responsabilidades: 

- Registro automático de servicios. 

- Descubrimiento dinámico. 

- Resolución de ubicaciones. 

- Soporte para escalabilidad horizontal. 

Beneficios: 

- Eliminación de configuraciones estáticas. 

- Facilidad para desplegar nuevas instancias. 

- Mayor resiliencia. 

## **4.3 Auth Service** 

Responsable de la autenticación y autorización de usuarios. 

Funcionalidades: 

- Registro de usuarios. 

- Inicio de sesión. 

- Generación de JWT. 

- Validación de JWT. 

- Gestión de roles. 

Roles soportados: 

- ADMIN 

- ORGANIZER 

- CUSTOMER 

3 

## **4.4 Event Service** 

Responsable de la administración de eventos. 

Funcionalidades: 

- Crear eventos. 

- Consultar catálogo. 

- Filtrar eventos. 

- Actualizar precios. 

- Cancelar eventos. 

Estados: 

- ACTIVE 

- CANCELLED 

- SOLD_OUT 

## **4.5 Order Service** 

Responsable de gestionar las órdenes de compra. 

Funcionalidades: 

- Crear órdenes. 

- Consultar órdenes. 

- Gestionar devoluciones. 

- Generar estadísticas. 

- Calcular ventas. 

Beneficios: 

- Centraliza la lógica comercial. • Garantiza consistencia de compras. 

## **4.6 Payment Service** 

Responsable de procesar pagos y comunicarse con la pasarela Wompi. 

Funcionalidades: 

- Crear transacciones. 

- Gestionar webhooks. 

- Validar pagos. 

- Aplicar promociones. 

- Gestionar devoluciones. 

- Detectar compras abandonadas. 

4 

Estados: 

- PENDIENTE 

- APROBADO 

- FALLIDO 

- DECLINADO 

Integración externa: 

- Wompi Sandbox 

## **4.7 Ticket Service** 

Responsable de la generación y validación de boletas digitales. 

Funcionalidades: 

- Generar tickets. 

- Generar códigos QR. 

- Consultar tickets. 

- Validar ingreso. 

- Evitar doble uso. 

Beneficios: 

- Control de acceso eficiente. 

- Trazabilidad de ingresos. 

## **4.8 Notification Service** 

Responsable de enviar comunicaciones a los usuarios. 

Funcionalidades: 

- Confirmación de compra. 

- Envío de tickets. 

- Recordatorios. 

- Notificación de cancelaciones. 

- Gestión de reintentos. 

Beneficios: 

- Procesamiento asíncrono. 

- Tolerancia a fallos. 

- Trazabilidad. 

5 

## **5. Comunicación Entre Servicios** 

## **Comunicación Síncrona** 

Se realiza mediante REST. 

Utilizada para: 

- Consulta de usuarios. 

- Validación de tokens. 

- Consulta de eventos. 

- Operaciones administrativas. 

## **Comunicación Asíncrona** 

Se realiza mediante Apache Kafka. 

Beneficios: 

- Desacoplamiento. 

- Escalabilidad. 

- Tolerancia a fallos. 

- Procesamiento distribuido. 

Eventos identificados: 

- PagoConfirmadoEvent 

- TicketGeneradoEvent 

- EventoCanceladoEvent 

- EventoCreadoEvent 

- DevolucionSolicitadaEvent 

## **6. Flujo Principal de Compra** 

## **Paso 1** 

El cliente consulta eventos. 

Frontend → API Gateway → Event Service 

## **Paso 2** 

El cliente selecciona entradas. 

Frontend → API Gateway → Order Service 

6 

## **Paso 3** 

Se crea una orden. 

Order Service registra la compra. 

## **Paso 4** 

Se inicia el pago. 

Order Service → Payment Service 

## **Paso 5** 

Wompi procesa la transacción. 

Payment Service → Wompi 

## **Paso 6** 

Wompi envía webhook. 

Wompi → Payment Service 

## **Paso 7** 

El pago es aprobado. 

Payment Service publica evento Kafka. 

## **Paso 8** 

Ticket Service genera la boleta. 

Kafka → Ticket Service 

## **Paso 9** 

Notification Service envía correo. 

Kafka → Notification Service 

## **Paso 10** 

El cliente recibe su ticket digital. 

7 

## **7. Seguridad** 

La seguridad se implementa mediante JWT. 

Mecanismos aplicados: 

- Autenticación centralizada. 

- Tokens firmados. 

- Roles y permisos. 

- Filtros de autorización. 

- Protección de endpoints. 

Beneficios: 

- Seguridad distribuida. 

- Bajo acoplamiento. 

- Escalabilidad. 

## **8. Persistencia** 

Cada microservicio administra su propia base de datos. 

Principio aplicado: 

Database per Service. 

Beneficios: 

- Independencia. 

- Escalabilidad. 

- Despliegue autónomo. 

- Menor acoplamiento. 

## **9. Trazabilidad** 

La plataforma registra eventos relevantes del negocio para facilitar soporte y auditoría. 

Ejemplos: 

- Creación de eventos. 

- Creación de órdenes. 

- Confirmación de pagos. 

- Generación de tickets. 

- Envío de notificaciones. 

- Solicitudes de devolución. 

8 

Esto permite reconstruir completamente el flujo de una operación. 

## **10. Requisitos No Funcionales Cubiertos** 

## **Escalabilidad** 

La arquitectura permite agregar instancias de servicios de forma independiente. 

## **Disponibilidad** 

Los servicios críticos permanecen desacoplados. 

## **Tolerancia a Fallos** 

Una falla en Notification Service no afecta pagos ni compras. 

## **Seguridad** 

Se implementa autenticación basada en JWT y control de acceso por roles. 

## **Mantenibilidad** 

Cada servicio posee una responsabilidad única y bien definida. 

## **Trazabilidad** 

Todas las operaciones relevantes pueden ser auditadas. 

## **11. Justificación Arquitectónica** 

La arquitectura basada en microservicios fue seleccionada para cumplir los requisitos del negocio planteados por VivaEventos. 

La combinación de Spring Boot, Eureka, API Gateway, Kafka, PostgreSQL y Wompi permite construir una plataforma escalable, resiliente y preparada para soportar eventos de alta concurrencia, manteniendo independencia entre componentes y facilitando la evolución futura del sistema. 

9 

