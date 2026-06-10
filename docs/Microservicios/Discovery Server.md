## **Discovery Server** 

## **Descripción** 

El Discovery Server es el componente encargado del descubrimiento de servicios dentro de la arquitectura de microservicios de VivaEventos. 

Está basado en Netflix Eureka y permite que los microservicios se registren automáticamente al iniciar y descubran dinámicamente la ubicación de otros servicios sin necesidad de configuraciones estáticas. 

## **Objetivo** 

Proporcionar un mecanismo centralizado de registro y descubrimiento de servicios para facilitar la comunicación entre microservicios y mejorar la escalabilidad de la plataforma. 

## **Tecnología Utilizada** 

- Spring Boot • Spring Cloud Netflix Eureka 

## **Responsabilidades** 

El Discovery Server es responsable de: 

- Registrar microservicios. 

- Mantener un catálogo actualizado de servicios disponibles. 

- Permitir el descubrimiento dinámico de servicios. 

- Facilitar la comunicación entre componentes distribuidos. 

- Reducir dependencias de configuración estática. 

## **Funcionamiento** 

Cuando un microservicio inicia: 

1. Se conecta al Discovery Server. 

2. Registra su nombre. 

3. Registra su dirección IP. 

4. Registra su puerto de ejecución. 

5. Queda disponible para otros servicios. 

1 

## **Flujo de Registro** 

Event Service → Eureka Server 

Order Service → Eureka Server 

Payment Service → Eureka Server 

Ticket Service → Eureka Server 

Notification Service → Eureka Server 

Auth Service → Eureka Server 

API Gateway → Eureka Server 

## **Flujo de Descubrimiento** 

1. Un servicio necesita comunicarse con otro. 

2. Consulta el Discovery Server. 

3. Obtiene la ubicación actual del servicio requerido. 

4. Realiza la comunicación utilizando la información obtenida. 

## **Beneficios Arquitectónicos** 

## **Desacoplamiento** 

Los servicios no necesitan conocer direcciones IP ni puertos de otros servicios. 

## **Escalabilidad** 

Es posible desplegar múltiples instancias de un mismo servicio. 

## **Flexibilidad** 

Los servicios pueden cambiar de ubicación sin afectar a otros componentes. 

## **Mantenibilidad** 

Reduce la necesidad de configuraciones manuales. 

2 

## **Requisitos No Funcionales Cubiertos** 

## **Escalabilidad** 

Permite agregar nuevas instancias de servicios sin modificar código. 

## **Disponibilidad** 

Facilita la recuperación y redistribución de servicios. 

## **Mantenibilidad** 

Centraliza la gestión de descubrimiento. 

## **Flexibilidad** 

Permite cambios de infraestructura con impacto mínimo. 

## **Integración con la Arquitectura VivaEventos** 

```
                    Discovery Server
                           │
    ┌──────────────────────┼──────────────────────┐
    │                      │                      │
```

API Gateway Auth Service Event Service │ │ │ 

├──────────────┬───────┴──────────────┬───────┤ │ │ │ Order Service Payment Service Ticket Service │ │ │ └──────────────┴──────────────┬───────┘ │ Notification Service 

Todos los servicios registran automáticamente su ubicación en Eureka Server y pueden descubrir dinámicamente a los demás componentes del sistema. 

## **Justificación Arquitectónica** 

El uso de Eureka permite cumplir con el requisito del gerente de construir una solución basada en microservicios que pueda crecer de manera independiente, soportar nuevos despliegues y facilitar el mantenimiento sin necesidad de reconfigurar manualmente las comunicaciones entre servicios. 

3 

