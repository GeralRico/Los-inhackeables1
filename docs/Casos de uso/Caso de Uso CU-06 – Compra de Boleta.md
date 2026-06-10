## **Caso de Uso CU-06 – Compra de Boleta** 

## **Objetivo** 

Permitir que un cliente compre una o varias boletas para un evento. 

## **Actor Principal** 

Cliente 

## **Actores Secundarios** 

- API Gateway 

- Order Service 

- Payment Service 

- Ticket Service 

- Notification Service 

## **Flujo Principal** 

1. El cliente selecciona un evento. 

2. El cliente selecciona tipo de boleta. 

3. El cliente indica cantidad. 

4. El sistema crea una orden en estado PENDING. 

5. Se registra auditoría. 

6. Se publica ORDER_CREATED. 

7. Payment Service inicia el proceso de pago. 

8. La pasarela procesa la transacción. 

9. Se confirma el pago. 

10. La orden cambia a CONFIRMED. 

11. Se publica ORDER_CONFIRMED. 

12. Ticket Service genera la boleta digital. 

13. Notification Service envía la confirmación al cliente. 

## **Flujos Alternos** 

## **A1 – Pago pendiente** 

La pasarela no responde inmediatamente. 

Resultado: 

La orden permanece en PAYMENT_PROCESSING. 

1 

## **A2 – Pago rechazado** 

La pasarela rechaza la transacción. 

Resultado: 

La orden permanece sin confirmar. 

## **A3 – Doble clic en comprar** 

Se recibe la misma idempotencyKey. 

Resultado: 

No se crea una segunda orden. 

## **Postcondiciones** 

- Orden confirmada. 

- Ticket generado. 

- Notificación enviada. 

- Auditoría registrada. 

## **Eventos Kafka** 

ORDER_CREATED 

ORDER_CONFIRMED 

## **Requisitos No Funcionales** 

- Idempotencia. 

- Consistencia. 

- Escalabilidad. 

- Disponibilidad. 

- Trazabilidad. 

2 

