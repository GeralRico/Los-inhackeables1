# Instructivo — Cómo Crear un Caso de Uso / Flujo Funcional

# Objetivo

Este instructivo explica paso a paso cómo llenar correctamente la plantilla de casos de uso del proyecto.

El objetivo es que todos los integrantes documenten los flujos de manera uniforme, clara y profesional.

---

# PASO 1 — Definir el nombre del flujo

El nombre debe describir claramente la acción principal.

## Correcto
- Compra de Boleta
- Validación QR
- Login Usuario
- Publicar Evento

## Incorrecto
- Flujo 1
- Backend compra
- Proceso sistema

---

# PASO 2 — Asignar ID

Formato recomendado:

```text
CU-01
CU-02
CU-03
```

Ejemplo:
- CU-01 → Compra de Boleta
- CU-02 → Validación QR

---

# PASO 3 — Escribir el objetivo

Responder:

> ¿Qué quiere lograr el usuario o el sistema?

Debe ser:
- corto
- claro
- directo

## Correcto
“Permitir que un cliente compre una boleta para un evento.”

## Incorrecto
“El sistema realiza muchas operaciones relacionadas con la compra.”

---

# PASO 4 — Definir actores

## Actor principal
Quién inicia el flujo.

Ejemplos:
- Cliente
- Organizador
- Administrador
- Personal Logístico

---

## Actores secundarios
Servicios externos o sistemas involucrados.

Ejemplos:
- Pasarela de pagos
- Notification Service
- Ticket Service

---

# PASO 5 — Escribir la descripción general

Explicar brevemente:
- qué hace el flujo
- por qué es importante

Máximo 1 párrafo corto.

## Ejemplo

“Este flujo permite que un cliente seleccione un evento, realice el pago y reciba una boleta digital con código QR.”

---

# PASO 6 — Definir precondiciones

Responder:

> ¿Qué debe existir antes de iniciar?

Ejemplos:
- Usuario autenticado
- Evento publicado
- Stock disponible
- Pasarela activa

---

# PASO 7 — Construir el flujo principal

Esta es la parte más importante.

Aquí deben escribir el proceso paso a paso en orden cronológico.

---

# Reglas importantes

## Cada paso debe:
- tener UNA sola acción
- ser claro
- seguir orden temporal
- describir comportamiento del sistema

---

# Estructura correcta

| Paso | Acción |
|---|---|
| 1 | El cliente selecciona el evento |
| 2 | El sistema valida disponibilidad |
| 3 | Se crea una orden pendiente |

---

# Ejemplo completo

| Paso | Acción |
|---|---|
| 1 | El cliente consulta eventos disponibles |
| 2 | El cliente selecciona un evento |
| 3 | El cliente selecciona tipo de boleta |
| 4 | El sistema valida stock disponible |
| 5 | El sistema crea una orden pendiente |
| 6 | El sistema inicia proceso de pago |
| 7 | La pasarela procesa el pago |
| 8 | El sistema recibe confirmación |
| 9 | El sistema genera ticket QR |
| 10 | El sistema envía notificación |

---

# Qué NO hacer

## Incorrecto

| Paso | Acción |
|---|---|
| 1 | El usuario compra el ticket y el sistema hace todo |

Problemas:
- ambiguo
- mezcla muchas acciones
- no explica flujo

---

# PASO 8 — Crear flujos alternos

Aquí documentan:
- errores
- excepciones
- fallos
- casos especiales

---

# Cómo escribirlos

## Estructura

### Nombre escenario
### Qué ocurre
### Qué debe hacer el sistema

---

# Ejemplo

## A1 — Pago rechazado

### Escenario
La pasarela rechaza el pago.

### Resultado esperado
La orden queda en estado FAILED y no se genera ticket.

---

# Qué deben cubrir SIEMPRE

En VivaEventos son obligatorios:
- pago rechazado
- pago pendiente
- stock insuficiente
- webhook duplicado
- QR ya usado
- fallo notificaciones

---

# PASO 9 — Definir postcondiciones

Responder:

> ¿Cómo termina el sistema después del flujo?

Ejemplos:
- Ticket generado
- Orden pagada
- Stock actualizado
- QR validado

---

# PASO 10 — Agregar reglas de negocio

Aquí van restricciones importantes.

## Ejemplos
- No vender más boletas que el aforo.
- Un QR solo puede validarse una vez.
- Solo administradores pueden modificar eventos.
- Un webhook no puede procesarse dos veces.

---

# PASO 11 — Identificar servicios involucrados

Listar qué microservicios participan.

## Ejemplo

| Servicio | Responsabilidad |
|---|---|
| Order Service | Crear órdenes |
| Payment Service | Procesar pagos |
| Ticket Service | Generar QR |

---

# PASO 12 — Agregar endpoints relacionados

Listar endpoints utilizados en el flujo.

## Ejemplo

| Método | Endpoint | Uso |
|---|---|---|
| POST | /orders | Crear orden |
| POST | /payments | Procesar pago |
| POST | /webhooks/payment | Confirmar pago |

---

# PASO 13 — Relacionar requisitos no funcionales

Indicar qué requisitos importantes intervienen.

Ejemplos:
- Seguridad
- Escalabilidad
- Concurrencia
- Disponibilidad
- Trazabilidad

---

# PASO 14 — Agregar observaciones técnicas

Aquí se escriben detalles importantes de arquitectura o backend.

Ejemplos:
- El webhook debe ser idempotente.
- Notification Service no debe bloquear compras.
- La validación QR debe responder rápidamente.

---

# Checklist antes de terminar

Antes de guardar el documento verificar:

- [ ] Tiene nombre claro
- [ ] Tiene ID
- [ ] Tiene precondiciones
- [ ] Tiene flujo principal
- [ ] Tiene flujos alternos
- [ ] Tiene postcondiciones
- [ ] Tiene endpoints
- [ ] Tiene microservicios
- [ ] Tiene reglas negocio
- [ ] Tiene errores importantes
- [ ] Tiene diagrama relacionado

---

# Resultado esperado

Un desarrollador nuevo debe poder:
- entender el flujo
- implementar endpoints
- identificar servicios
- crear pruebas
- entender errores
- construir diagramas

SOLO leyendo el caso de uso.