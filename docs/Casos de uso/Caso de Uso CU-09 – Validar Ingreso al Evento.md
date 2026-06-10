## **Caso de Uso CU-09 – Validar Ingreso al Evento** 

## **Objetivo** 

Permitir al personal logístico verificar la autenticidad de una boleta y autorizar el ingreso al evento. 

## **Actor Principal** 

Personal de Logística 

## **Actores Secundarios** 

- Ticket Service 

- Base de Datos 

## **Flujo Principal** 

1. El operador escanea el código QR. 

2. Se obtiene el código único del ticket. 

3. Ticket Service consulta la información asociada. 

4. El sistema verifica que el ticket exista. 

5. El sistema verifica que no haya sido utilizado. 

6. El sistema registra la validación. 

7. El sistema autoriza el ingreso. 

## **Flujos Alternos** 

## **A1 – Ticket inexistente** 

Resultado: 

Ingreso rechazado. 

## **A2 – Ticket previamente utilizado** 

Resultado: 

Ingreso rechazado. 

## **A3 – Ticket inválido** 

Resultado: 

1 

Ingreso rechazado. 

## **Postcondiciones** 

- El ticket queda marcado como utilizado. 

- Se registra fecha y hora de validación. 

- Se evita el reingreso con el mismo código. 

## **Reglas de Negocio** 

RN-01: Un ticket solo puede validar una vez. 

RN-02: Todo intento de validación debe ser registrado. 

RN-03: El código QR debe corresponder a un ticket existente. 

## **Endpoint Relacionado** 

POST /tickets/{codigo}/validate 

## **Requisitos No Funcionales Relacionados** 

- Baja latencia. 

- Alta disponibilidad. 

- Integridad de datos. 

- Trazabilidad. 

2 

