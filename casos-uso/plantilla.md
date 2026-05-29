
# Plantilla — Caso de Uso / Flujo Funcional

# 1. Información General

## ID
CU-XX

## Nombre
Nombre corto y claro del flujo.

## Objetivo
Explicar qué busca lograr el usuario o el sistema.

## Actor principal
Usuario principal que ejecuta el flujo.

## Actores secundarios
Servicios o actores externos involucrados.

---

# 2. Descripción General

Explicación breve del flujo y su importancia dentro del sistema.

---

# 3. Precondiciones

Condiciones necesarias antes de iniciar el flujo.

Ejemplos:
- Usuario autenticado
- Evento existente
- Stock disponible
- Pasarela operativa

---

# 4. Flujo Principal

| Paso | Acción |
|---|---|
| 1 | |
| 2 | |
| 3 | |
| 4 | |
| 5 | |

---

# 5. Flujos Alternos

## A1 — Nombre del escenario alterno

### Escenario
Descripción del problema o situación alterna.

### Resultado esperado
Qué debe hacer el sistema.

---

## A2 — Nombre del escenario alterno

### Escenario
Descripción del problema o situación alterna.

### Resultado esperado
Qué debe hacer el sistema.

---

# 6. Postcondiciones

Estado esperado después de terminar el flujo.

Ejemplos:
- Orden creada
- Ticket generado
- Stock actualizado
- Notificación enviada

---

# 7. Reglas de Negocio

Restricciones o reglas importantes.

Ejemplos:
- No vender más boletas que el aforo.
- Un QR solo puede validarse una vez.
- Solo administradores pueden modificar eventos.

---

# 8. Servicios Involucrados

| Servicio | Responsabilidad |
|---|---|
| | |
| | |
| | |

---

# 9. Eventos Asíncronos (Opcional)

Ejemplos:
- ORDER_CREATED
- PAYMENT_APPROVED
- TICKET_GENERATED

---

# 10. Endpoints Relacionados

| Método | Endpoint | Descripción |
|---|---|---|
| | | |
| | | |
| | | |

---

# 11. Requisitos No Funcionales Relacionados

Ejemplos:
- Escalabilidad
- Disponibilidad
- Trazabilidad
- Seguridad
- Concurrencia

---

# 12. Observaciones Técnicas

Detalles importantes para backend, arquitectura o integración.

Ejemplos:
- El webhook debe ser idempotente.
- La validación QR debe responder en menos de 2 segundos.
- Notification Service no debe bloquear compras.

---

# 13. Diagrama Relacionado

Nombre del diagrama asociado.

Ejemplo:
- secuencia-compra-boleta.png
