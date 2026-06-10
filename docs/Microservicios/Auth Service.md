## **Auth Service** 

## **Descripción** 

El Auth Service es el microservicio responsable de la autenticación y autorización de usuarios dentro de la plataforma VivaEventos. 

Su objetivo es garantizar que únicamente los usuarios autenticados puedan acceder a los recursos protegidos del sistema y que cada usuario tenga permisos acordes a su rol. 

Este servicio implementa autenticación basada en JWT (JSON Web Token), permitiendo una arquitectura desacoplada y escalable para el ecosistema de microservicios. 

## **Responsabilidades** 

El Auth Service es responsable de: 

- Registrar nuevos usuarios. 

- Autenticar usuarios existentes. 

- Generar tokens JWT. 

- Validar tokens JWT. 

- Gestionar roles y permisos. 

- Proteger endpoints del sistema. 

- Administrar usuarios con privilegios administrativos. 

- Centralizar la lógica de seguridad. 

## **Arquitectura Interna** 

## **Controllers** 

## **AuthController** 

Expone los endpoints relacionados con autenticación y gestión de usuarios. 

Funciones principales: 

- Registro de usuarios. 

- Inicio de sesión. 

- Validación de tokens. 

- Creación de administradores. 

## **GlobalExceptionHandler** 

Gestiona de forma centralizada las excepciones generadas por el servicio. 

1 

Permite devolver respuestas consistentes ante errores de validación o negocio. 

## **DTOs** 

## **RegisterRequest** 

Representa la información necesaria para registrar un usuario. 

## **LoginRequest** 

Representa las credenciales enviadas durante el inicio de sesión. 

## **AuthResponse** 

Contiene la información retornada después de una autenticación exitosa, incluyendo el token JWT. 

## **ValidateResponse** 

Contiene el resultado de la validación de un token. 

## **CreateAdminRequest** 

Permite la creación de usuarios con privilegios administrativos. 

## **MessageResponse** 

Se utiliza para respuestas simples de confirmación o error. 

## **Persistencia** 

## **User** 

Entidad principal que representa a los usuarios del sistema. 

Información almacenada: 

- Identificador único. 

- Nombre. 

- Correo electrónico. 

- Contraseña cifrada. 

- Rol. 

- Fecha de creación. 

## **UserRepository** 

Permite acceder y administrar los usuarios almacenados en la base de datos. 

2 

## **Seguridad** 

## **JwtService** 

Responsable de: 

- Generar tokens JWT. 

- Validar tokens JWT. 

- Extraer información del usuario desde el token. 

## **JwtAuthenticationFilter** 

Intercepta las solicitudes HTTP y verifica la validez del token JWT antes de permitir el acceso. 

## **CustomUserDetailsService** 

Carga la información de usuarios desde la base de datos para el proceso de autenticación. 

## **SecurityConfig** 

Define: 

- Endpoints públicos. 

- Endpoints protegidos. 

- Reglas de autorización. 

- Configuración de filtros de seguridad. 

## **Flujo de Registro** 

1. El usuario envía un RegisterRequest. 

2. El sistema valida la información recibida. 

3. Se verifica que el correo no exista previamente. 

4. Se crea el usuario. 

5. Se almacena en la base de datos. 

- Se devuelve una respuesta de confirmación. 

6. 

## **Flujo de Inicio de Sesión** 

1. El usuario envía un LoginRequest. 

2. El sistema valida las credenciales. 

3. Se genera un token JWT. 

4. Se devuelve un AuthResponse con el token. 

5. El cliente almacena el token para futuras solicitudes. 

3 

## **Flujo de Autorización** 

1. El cliente envía una solicitud protegida. 

2. Incluye el token JWT en el encabezado Authorization. 

3. JwtAuthenticationFilter intercepta la solicitud. 

4. Se valida la firma y vigencia del token. 

5. Si es válido, se autoriza el acceso. 

6. Si es inválido, se rechaza la solicitud. 

## **Manejo de Excepciones** 

## **EmailAlreadyExistsException** 

Se lanza cuando un usuario intenta registrarse utilizando un correo ya existente. 

## **AdminCreationException** 

Se lanza cuando ocurre un error durante la creación de un usuario administrador. 

## **Roles del Sistema** 

La plataforma contempla diferentes tipos de usuarios para controlar el acceso a las funcionalidades. 

## **ADMIN** 

Responsable de: 

- Administrar la plataforma. 

- Gestionar usuarios. 

- Supervisar eventos. 

- Consultar estadísticas globales. 

## **ORGANIZER** 

Responsable de: 

- Crear eventos. 

- Modificar eventos. 

- Gestionar promociones. 

- Consultar ventas de sus eventos. 

4 

## **CUSTOMER** 

Responsable de: 

- Consultar eventos. 

- Comprar entradas. 

- Solicitar devoluciones. 

- Validar información de sus compras. 

## **Reglas de Negocio** 

## **RN-01** 

Todo usuario debe autenticarse para acceder a recursos protegidos. 

## **RN-02** 

No pueden existir dos usuarios con el mismo correo electrónico. 

## **RN-03** 

Los tokens JWT deben ser válidos y no estar expirados. 

## **RN-04** 

Cada usuario solo puede acceder a los recursos permitidos por su rol. 

## **RN-05** 

Las credenciales deben validarse antes de generar un token JWT. 

## **Requisitos No Funcionales** 

## **Seguridad** 

Todos los endpoints protegidos requieren autenticación mediante JWT. 

## **Integridad** 

La información de usuarios debe mantenerse consistente y protegida. 

## **Escalabilidad** 

La autenticación está desacoplada del resto de microservicios. 

5 

## **Disponibilidad** 

La validación de tokens no depende de otros servicios externos. 

## **Mantenibilidad** 

La lógica de autenticación y autorización está centralizada en un único microservicio. 

## **Casos de Uso Relacionados** 

## **CU-01 – Registro de Usuario** 

Permite que un nuevo usuario cree una cuenta dentro de la plataforma. 

## **Actor Principal** 

Usuario 

## **Resultado** 

Usuario registrado exitosamente. 

## **CU-02 – Inicio de Sesión** 

Permite que un usuario autenticado obtenga un token JWT. 

## **Actor Principal** 

Usuario 

## **Resultado** 

Token JWT generado correctamente. 

## **CU-03 – Validación de Token** 

Permite verificar si un token JWT es válido. 

## **Actor Principal** 

Microservicios de VivaEventos 

6 

## **Resultado** 

Confirmación de autenticación y autorización. 

## **Integración con la Arquitectura VivaEventos** 

El Auth Service actúa como proveedor central de identidad para todos los microservicios del sistema. 

Arquitectura simplificada: 

Cliente → API Gateway → Auth Service → Generación JWT → Acceso a Event Service → Acceso a Order Service → Acceso a Payment Service → Acceso a Ticket Service → Acceso a Notification Service 

Esta arquitectura permite garantizar seguridad, trazabilidad y control de acceso en toda la plataforma VivaEventos. 

7 

