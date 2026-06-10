## **API Gateway** 

## **Descripción** 

El API Gateway es el punto de entrada único para todos los clientes que consumen la plataforma VivaEventos. 

Su principal responsabilidad es centralizar el acceso a los microservicios, aplicando mecanismos de autenticación, autorización y enrutamiento antes de reenviar las solicitudes al servicio correspondiente. 

Esta aproximación permite desacoplar a los clientes de la estructura interna del sistema y simplifica la gestión de la seguridad. 

## **Responsabilidades** 

El API Gateway es responsable de: 

- Recibir todas las solicitudes externas. 

- Validar tokens JWT. 

- Aplicar filtros de seguridad. 

- Enrutar peticiones hacia los microservicios correspondientes. 

- Comunicarse con Auth Service para validar autenticación. 

- Ocultar la topología interna del sistema. 

- Centralizar políticas de acceso. 

## **Arquitectura Interna** 

## **Configuración** 

## **GatewayAuthProperties** 

Contiene las propiedades necesarias para la integración con el sistema de autenticación. 

Permite configurar: 

- URLs de validación. 

- Endpoints protegidos. 

- Parámetros de seguridad. 

## **WebClientConfig** 

Configura el cliente HTTP utilizado para la comunicación entre el Gateway y otros microservicios. 

1 

Se utiliza principalmente para: 

- Consultar Auth Service. 

- Validar tokens JWT. 

- Realizar llamadas internas de forma no bloqueante. 

## **Filtros** 

## **JwtAuthenticationFilter** 

Intercepta todas las solicitudes entrantes. 

Funciones principales: 

- Extraer el token JWT. 

- Validar el token. 

- Consultar Auth Service cuando sea necesario. 

- Autorizar o rechazar solicitudes. 

- Propagar información del usuario a los microservicios. 

## **Flujo de Solicitudes** 

## **Solicitud Autenticada** 

1. El cliente envía una solicitud al API Gateway. 

2. Incluye el token JWT en el encabezado Authorization. 

3. JwtAuthenticationFilter intercepta la solicitud. 

4. Se valida el token. 

5. Si el token es válido, la solicitud es reenviada. 

6. El microservicio procesa la operación. 

7. La respuesta retorna al cliente a través del Gateway. 

## **Solicitud No Autenticada** 

1. El cliente envía una solicitud protegida. 

2. No se encuentra un token válido. 

3. El Gateway rechaza la solicitud. 

4. Se devuelve un error de autorización. 

2 

## **Seguridad** 

## **JWT** 

El Gateway utiliza autenticación basada en JSON Web Tokens (JWT). 

Beneficios: 

- Stateless. 

- Escalable. 

- Compatible con microservicios. 

- Bajo acoplamiento. 

## **Validación Centralizada** 

Toda validación de acceso se realiza antes de llegar a los microservicios. 

Esto permite: 

- Reducir duplicación de código. 

- Simplificar mantenimiento. 

- Aplicar políticas uniformes. 

## **Integración con Auth Service** 

El Gateway se comunica con Auth Service para: 

- Validar tokens. 

- Obtener información del usuario. 

- Verificar permisos. 

## **Beneficios Arquitectónicos** 

## **Seguridad Centralizada** 

La autenticación se administra desde un único punto. 

## **Escalabilidad** 

Los microservicios pueden crecer independientemente. 

3 

## **Desacoplamiento** 

Los clientes no necesitan conocer la ubicación de los servicios internos. 

## **Mantenibilidad** 

Las reglas de acceso se administran en un único componente. 

## **Requisitos del Negocio Cubiertos** 

## **Control de Acceso** 

Evita que usuarios no autorizados accedan a recursos protegidos. 

## **Protección de Datos** 

Garantiza que únicamente usuarios autenticados puedan realizar operaciones sensibles. 

## **Seguridad** 

Centraliza la validación de credenciales y permisos. 

## **Escalabilidad** 

Permite agregar nuevos microservicios sin modificar los clientes. 

## **Requisitos No Funcionales** 

## **Seguridad** 

Todas las solicitudes protegidas deben validarse antes de acceder a los servicios. 

## **Disponibilidad** 

El Gateway debe permanecer disponible para permitir el acceso a la plataforma. 

## **Escalabilidad** 

Debe soportar múltiples solicitudes concurrentes. 

## **Trazabilidad** 

Permite registrar el flujo de solicitudes hacia los microservicios. 

4 

## **Integración con la Arquitectura VivaEventos** 

Cliente → API Gateway → Auth Service → Event Service → Order Service → Payment Service → Ticket Service → Notification Service 

El API Gateway actúa como puerta de entrada única para toda la plataforma, proporcionando seguridad, control de acceso y enrutamiento centralizado. 

5 

