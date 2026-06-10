## **Caso de Uso CU-10 – Notificar Compra Exitosa** 

## **Objetivo** 

Informar al cliente que su compra fue confirmada y que su boleta ha sido generada correctamente. 

## **Actor Principal** 

Cliente 

## **Actores Secundarios** 

- Ticket Service 

- Notification Service 

- Kafka 

## **Flujo Principal** 

1. Ticket Service genera una boleta. 

2. Se publica el evento TICKET_GENERATED. 

3. Notification Service consume el evento. 

4. Se construye el mensaje correspondiente. 

5. Se registra la notificación. 

6. Se envía el correo al cliente. 

- Se actualiza el estado de la notificación. 

7. 

## **Flujo Alterno** 

## **A1 – Error de envío** 

El proveedor de correo no responde. 

Resultado: 

La notificación queda pendiente para reintento. 

## **Postcondiciones** 

- Cliente informado. 

- Notificación registrada. 

- Evidencia almacenada para soporte. 

1 

## **Requisitos No Funcionales Relacionados** 

- Trazabilidad. 

- Disponibilidad. 

- Tolerancia a fallos. 

2 

