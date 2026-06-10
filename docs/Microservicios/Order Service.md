**OrderService** **Descripción**

ElOrderServiceesresponsabledegestionarelciclodevidadelasórdenesdecompradentrodela
plataformaVivaEventos.

Controlalacreacióndeórdenes,laconfirmacióndepagos,lascancelaciones,lasdevolucionesyla
generacióndeestadísticasdeventas.

**Responsabilidades**

> •Crearórdenesdecompra. •Calcularvalorestotales. •Aplicardescuentos.
> •Gestionarestadosdelaorden. •Registrarauditoría.
> •PublicareventosdenegociomedianteKafka. •Generarreportesdeventas.
>
> •Generarestadísticasdecomportamientodecompra.

**Tecnologías**

> •SpringBoot •PostgreSQL •Kafka •SpringDataJPA •EurekaClient •Docker

**EntidadPrincipal** **Order** Atributosrelevantes:

> •id •eventId
>
> •customerId •customerEmail •ticketType •quantity •unitPrice
> •discountPct
>
> 1
>
> •totalAmount •status •idempotencyKey •createdAt •updatedAt

**EstadosdelaOrden** **PENDING**

Laordenfuecreadayestápendientedeiniciarelprocesodepago.

**PAYMENT_PROCESSING** Lapasarelaestáprocesandoelpago.

**CONFIRMED** Elpagofueconfirmadoexitosamente.

**CANCELLED** Laordenfuecancelada.

**REFUND_REQUESTED** Elclientesolicitódevolución.

**Endpoints** **CrearOrden** POST/orders

Creaunanuevaordendecompra.

Respuesta:

HTTP201Created

**ConsultarOrden** GET/orders/{id}

Obtienelainformacióndeunaorden.

> 2

Respuesta:

HTTP200OK

**SolicitarDevolución** POST/orders/{id}/refund

Registraunasolicituddedevolución.

Respuesta:

HTTP200OK

**VentasporEvento** GET/orders/events/{eventId}/sales

Obtienemétricasgeneralesdeventas.

**EstadísticasporEvento** GET/orders/events/{eventId}/statistics

Obtienemétricasdetalladasdecomportamientodecompra.

**EventosPublicados** ORDER_CREATED

ORDER_CONFIRMED

ORDER_CANCELLED

REFUND_REQUESTED

**ReglasdeNegocio**

RN-01:Unaordenconfirmadanopuedevolveraconfirmarse.

RN-02:SololasórdenesCONFIRMEDpuedensolicitardevolución.

RN-03:LasórdenesCANCELLEDnopuedensermodificadas.

> 3

RN-04:Cadaordendebetenerunidentificadorúnico.

RN-05:Lasoperacionescríticasdebenquedarauditadas.

RN-06:Elsistemadebesoportaridempotenciaparaevitarcomprasduplicadas.

**Trazabilidad** Cadacambiodeestadogeneraunregistrodeauditoríacon:

> •Estadoanterior. •Estadonuevo. •Actorresponsable.
> •Descripcióndelaacción. •Fechayhora.

**IntegraciónconKafka**
Elserviciopublicaeventosparadesacoplarprocesosposteriorescomo:

> •Generacióndetickets. •Envíodenotificaciones.
> •Procesamientodedevoluciones. •Actualizacióndemétricas.

**RequisitosNoFuncionales**

> •Consistencia. •Escalabilidad. •Disponibilidad. •Trazabilidad.
> •Seguridad.
>
> 4
