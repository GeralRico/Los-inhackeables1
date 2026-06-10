## **Caso de Uso CU-01 – Crear Evento** 

## **Información General** 

**ID:** CU-01 

**Nombre:** Crear Evento 

**Objetivo:** Permitir a un organizador registrar un nuevo evento en la plataforma VivaEventos. 

## **Actor Principal:** Organizador 

## **Actores Secundarios:** 

- Event Service 

- PostgreSQL 

- Eureka Discovery Server 

## **Descripción General** 

El organizador registra un evento indicando información básica como nombre, ubicación, fecha, capacidad y precio. 

Una vez creado, el evento queda disponible en estado ACTIVE y puede ser consultado desde el catálogo. 

## **Precondiciones** 

- El usuario debe estar autenticado. 

- Debe poseer permisos de organizador. 

- La fecha del evento debe ser futura. 

## **Flujo Principal** 

1. El organizador accede al formulario de creación. 

2. Ingresa la información del evento. 

3. El sistema valida los datos enviados. 

4. El sistema crea el evento. 

5. Se asigna el estado ACTIVE. 

6. Se inicializa el stock disponible igual a la capacidad. 

7. El sistema almacena el evento. 

8. Se retorna la información del evento creado. 

1 

## **Flujos Alternos** 

## **A1 – Fecha inválida** 

La fecha enviada corresponde a una fecha pasada. 

## **Resultado:** 

HTTP 400 Bad Request. 

## **A2 – Capacidad inválida** 

La capacidad es menor a 1. 

## **Resultado:** 

HTTP 400 Bad Request. 

## **A3 – Precio negativo** 

El precio es menor que cero. 

## **Resultado:** 

HTTP 400 Bad Request. 

## **Postcondiciones** 

- El evento queda registrado en la base de datos. 

- El estado inicial es ACTIVE. 

- availableTickets es igual a capacity. 

- 

## **Reglas de Negocio** 

RN-01: La fecha del evento debe ser futura. 

RN-02: La capacidad mínima permitida es 1. 

RN-03: El precio no puede ser negativo. 

RN-04: Todo evento debe tener un organizador asociado. 

RN-05: El stock inicial de boletas es igual al aforo definido. 

2 

RN-06: Todo evento nuevo inicia en estado ACTIVE. 

## **Endpoint Relacionado** 

POST /events 

## **Datos de Entrada** 

```
{
"name":"Concierto Rock en el Parque",
"description":"Festival de rock al aire libre",
"category":"CONCIERTO",
"venue":"Parque Simón Bolívar",
"eventDate":"2026-08-15T18:00:00",
"capacity":5000,
"price":85000,
"organizerId":"550e8400-e29b-41d4-a716-446655440000"
}
```

## **Datos de Salida** 

Objeto EventResponse con la información completa del evento creado. 

3 

