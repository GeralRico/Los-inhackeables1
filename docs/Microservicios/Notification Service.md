**NotificationService** **Descripción**

ElNotificationServiceesresponsabledegestionarelenvíodecomunicacionesalosusuariosdela
plataformaVivaEventos.

Sufunciónprincipalesinformareventosrelevantesdelnegociocomocomprasexitosas,generaciónde
boletas,cancelacionesdeeventos,devolucionesyrecordatorios.

LaarquitecturasebasaeneventosKafka,permitiendodesacoplarcompletamenteelenvíode
notificacionesdelosprocesosdecompraypago.

**Responsabilidades**

> •Enviarconfirmacionesdecompra. •Notificargeneracióndetickets.
> •Informarcancelacionesdeeventos. •Informardevoluciones.
> •Programarrecordatorios. •Gestionarreintentosautomáticos.
> •Mantenertrazabilidaddecomunicaciones.

**TecnologíasUtilizadas**

> •SpringBoot •ApacheKafka •QuartzScheduler •PostgreSQL •SpringDataJPA
> •Docker

**EventosKafkaConsumidos** **PagoConfirmadoEvent**
Seutilizaparainformarqueunacomprafueaprobada.

**TicketGeneradoEvent**
Seutilizaparaenviarinformaciónasociadaalaboletagenerada.

> 1

**EventoCreadoEvent**
Permitegenerarcomunicacionesrelacionadasconnuevoseventos.

**EventoCanceladoEvent** Permiteinformarcancelacionesalosasistentes.

**DevolucionSolicitadaEvent**
Permiteinformareliniciodelprocesodedevolución.

**ProgramacióndeTareas** **ReminderJob**

Responsabledegenerarrecordatoriosautomáticosantesdelevento.

**RetryEmailJob**
Responsabledereenviarnotificacionesquenopudieronentregarseexitosamente.

**ReglasdeNegocio**

RN-01:Elfallodeunanotificaciónnodebeafectarelprocesodecompra.

RN-02:Todaslasnotificacionesdebenquedarregistradas.

RN-03:Lasnotificacionesfallidasdebenpoderreintentarse.

RN-04:Losrecordatoriosdebenprogramarseautomáticamente.

RN-05:Lascancelacionesdebennotificarseatodoslosasistentesafectados.

**RequisitosNoFuncionales**

> •Disponibilidad. •Escalabilidad. •Trazabilidad. •Toleranciaafallos.
> •Procesamientoasíncrono.
>
> 2

**BeneficiosArquitectónicos**

ElusodeKafkapermitedesacoplarcompletamenteelenvíodecorreosdelosprocesoscríticosdel
negocio.

Deestaforma,unafallatemporaldelNotificationServicenoafectalacompra,elpagonilageneración
detickets.

> 3
