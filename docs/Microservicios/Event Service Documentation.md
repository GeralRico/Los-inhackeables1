## **Event Service** 

## **Descripción** 

El Event Service es el microservicio responsable de la gestión del ciclo de vida de los eventos dentro de la plataforma VivaEventos. 

Permite crear, consultar, filtrar, actualizar y cancelar eventos, garantizando que la información de los eventos esté disponible para los demás microservicios del ecosistema. 

## **Responsabilidades** 

- Crear eventos. 

- Consultar catálogo de eventos. 

- Filtrar eventos por categoría y rango de fechas. 

- Actualizar precios de eventos. 

- Cancelar eventos. 

- Publicar eventos para su visualización en la plataforma. 

- Notificar eventos relevantes al ecosistema mediante Kafka. 

## **Tecnologías Utilizadas** 

- Java 21 • Spring Boot 3.3.5 • Spring Data JPA • PostgreSQL • Flyway • Spring Security • Apache Kafka • Eureka Client 

- Docker 

## **Endpoints** 

## **Crear Evento** 

**POST** `/events` 

Permite registrar un nuevo evento en la plataforma. 

Respuesta exitosa: 

- HTTP 201 Created 

## **Consultar Catálogo** 

**GET** `/events/catalog` 

1 

Obtiene todos los eventos disponibles para los clientes. 

Respuesta exitosa: 

- HTTP 200 OK 

## **Filtrar Eventos** 

**GET** `/events` 

Permite consultar eventos aplicando filtros. 

Parámetros soportados: 

- category 

- dateFrom 

- dateTo 

Respuesta exitosa: 

- HTTP 200 OK 

## **Actualizar Precio** 

**PATCH** `/events/{id}/price` 

Permite modificar el precio asociado a un evento. 

Respuesta exitosa: 

- HTTP 200 OK 

## **Cancelar Evento** 

**DELETE** `/events/{id}` 

Realiza una cancelación lógica (soft delete) del evento. 

Opcionalmente recibe el motivo de cancelación. 

Respuesta exitosa: 

- HTTP 200 OK 

Posibles errores: 

- HTTP 404 Not Found 

2 

• HTTP 409 Conflict 

## **Reglas de Negocio** 

- Un evento cancelado no puede recibir nuevas compras. • Solo usuarios autorizados pueden crear o modificar eventos. 

- La cancelación de un evento debe conservar el registro histórico. • La cancelación debe generar notificaciones a los clientes afectados. 

- Los filtros deben permitir búsquedas por categoría y fechas. 

- 

## **Requisitos No Funcionales Relacionados** 

- Seguridad. 

- Escalabilidad. 

- Disponibilidad. 

- Trazabilidad. 

- Mantenibilidad. 

## **Integraciones** 

## **Discovery Server** 

El servicio se registra automáticamente en Eureka para ser descubierto por otros microservicios. 

## **Kafka** 

El servicio publica eventos de negocio para informar cambios relevantes al resto del sistema. 

Ejemplos: 

- EVENT_CREATED 

- EVENT_PRICE_UPDATED 

- EVENT_CANCELLED 

## **Base de Datos** 

Base de datos independiente PostgreSQL siguiendo el principio de autonomía de microservicios. 

La persistencia se gestiona mediante Spring Data JPA y las migraciones mediante Flyway. 

3 

