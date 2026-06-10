## **Caso de Uso CU-07 – Procesar Pago** 

## **Objetivo** 

Permitir que un cliente realice el pago de una orden utilizando la pasarela Wompi. 

## **Actor Principal** 

Cliente 

## **Actores Secundarios** 

- Order Service • Payment Service • Wompi • Kafka 

- Ticket Service 

## **Flujo Principal** 

1. El cliente confirma la compra. 

2. Order Service genera la orden. 

3. Se publica el evento ORDEN_LISTA_PARA_PAGO. 

4. Payment Service recibe el evento. 

5. Se crea una transacción en Wompi. 

6. El pago queda en estado PENDIENTE. 

7. Wompi procesa la transacción. 

8. Wompi envía un webhook. 9. Payment Service valida la firma. 

10. El pago cambia a APROBADO. 

11. Se publica el evento PAGO_CONFIRMADO. 

12. Ticket Service genera la boleta. 13. Notification Service envía la confirmación. 

## **Flujos Alternos** 

## **A1 – Pago rechazado** 

Wompi rechaza la transacción. 

Resultado: 

Estado DECLINADO. 

1 

## **A2 – Error de procesamiento** 

Se produce un error durante la operación. 

Resultado: 

Estado FALLIDO. 

## **A3 – Confirmación tardía** 

La pasarela demora en responder. 

Resultado: 

El pago permanece en estado PENDIENTE hasta recibir el webhook. 

## **Postcondiciones** 

- Pago registrado. 

- Estado actualizado. 

- Evento Kafka generado. 

- Ticket emitido si el pago fue aprobado. 

## **Requisitos No Funcionales Relacionados** 

- Trazabilidad. 

- Consistencia. 

- Disponibilidad. 

- Escalabilidad. 

2 

