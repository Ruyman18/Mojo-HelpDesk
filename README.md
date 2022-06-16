# Mojo-HelpDesk

# Documentación de Mojo Helpdesk API v2

Mojo Helpdesk es un software de seguimiento de tickets como servicio (Saas). Está desarrollado por Metadot.
Este documento describe su API pública v2. La API v1 está en desuso.

## Acerca de la API del servicio de asistencia de Mojo

La API de Mojo Helpdesk es fácil de usar. Permite a los desarrolladores de terceros crear aplicaciones web, de escritorio y de servidor o scripts simples que pueden comunicarse directamente con el servicio de asistencia técnica de Mojo. La comunicación se realiza mediante RESTful HTTPsolicitudes en JSONformato. XMLno es apoyado.

# Documentación de la API del servicio de asistencia técnica de Mojo

## Autenticación

En el código a continuación, reemplace access_keyel parámetro con su clave de acceso (se puede encontrar en su perfil).
La API de Mojo Helpdesk requiere una clave de acceso que se encuentra en el perfil de usuario de Mojo Helpdesk.

## Entradas

### Listar entradas

    curl https://app.mojohelpdesk.com/api/v2/tickets?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

    curl https://app.mojohelpdesk.com/api/v2/tickets?access_key=9c9745101d12aed4d5a67d43747824451f9251d4\&per_page=20\&page=3


### Mostrar boleto

    curl https://app.mojohelpdesk.com/api/v2/tickets/88?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear Ticket

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"title":"Test ticket","description":"Testing API for ticket creation","ticket_queue_id":"8","priority_id":"30"}'
    
### Crear TicketCrear ticket con el usuario

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"title":"Test ticket","description":"Testing API for ticket creation","ticket_queue_id":"8","priority_id":"30", "user":{"email":"customer@someplace.com"}}'

#### Parámetros adicionales

suprimir_usuario_notificación: booleano cuando se establece en trueno enviará ningún correo electrónico para notificar la creación del ticket

### Actualizar boleto

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets/113?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X PUT -d '{"title":"Test ticket API"}'

### Lista de eventos para un boleto

    curl https://app.mojohelpdesk.com/api/v2/tickets/113/events?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Agregar etiqueta a un ticket

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets/113/add_tag?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"tag_label":"Test"}'

### Eliminar etiqueta de un ticket

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets/113/remove_tag?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"tag_label":"Test"}'

### Destruir boleto

    curl https://app.mojohelpdesk.com/api/v2/tickets/113?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE


## Comentarios de entradas

### Listado de comentarios para un ticket

    curl https://app.mojohelpdesk.com/api/v2/tickets/114/comments?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear comentario

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets/88/comments?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"body":"New comment"}'

### Campos de entrada de comentarios

- cuerpo - Cuerda
- time_spent - Entero
- cc - Cadena

### Notas del personal de entradas

- suppress_user_notification - Boolean

### Listado de notas del personal para un ticket

    curl https://app.mojohelpdesk.com/api/v2/tickets/114/staff_notes?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear nota para el personal

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets/88/staff_notes?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"body":"New staff note"}'

### Campos de entrada de notas del personal

- cuerpo - Cuerda
- cc - Cadena
- time_spent - Entero

## Archivos adjuntos de boletos

### Enumerar archivos adjuntos para un ticket

    curl https://app.mojohelpdesk.com/api/v2/tickets/211402/attachments?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Agregar archivo adjunto a un ticket

    curl -F "file=@/home/user/my-file.txt" https://app.mojohelpdesk.com/api/v2/tickets/211402/attachments?staff_only=true\&access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST

Additional url params:

- `staff_only` - true/false

### Descargar un archivo adjunto

    curl https://app.mojohelpdesk.com/api/v2/attachments/6422878?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Eliminar un archivo adjunto

    curl https://app.mojohelpdesk.com/api/v2/attachments/6422878?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE

### Todas las entradas abiertas

    curl https://app.mojohelpdesk.com/api/v2/tickets/search?query=status.id:\(\<50\)\&sf=created_on\&r=0\&access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Todos los tickets abiertos urgentes

    curl https://app.mojohelpdesk.com/api/v2/tickets/search?query=priority.id:\(\<=20\)%20AND%20status.id:\(\<50\)&sf=created_on\&r=0\&access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Todos los tickets abiertos en cierta cola

    curl https://app.mojohelpdesk.com/api/v2/tickets/search?query=queue.id:19647%20AND%20status.id:\(\<50\)\&sf=created_on\&r=0\&access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Todos los boletos con fecha de vencimiento

    curl https://app.mojohelpdesk.com/api/v2/tickets/search?query=_exists_:due_on\&sf=created_on\&r=0\&access_key=9c9745101d12aed4d5a67d43747824451f9251d4

## Colas de entradas

### Lista de colas de boletos

    curl https://app.mojohelpdesk.com/api/v2/ticket_queues?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### La lista de colas de tickets admite paginación, con parámetros opcionales por_página y parámetros de página. Si falta per_page, de forma predeterminada devolverá 30 elementos por página

    curl https://app.mojohelpdesk.com/api/v2/ticket_queues?access_key=9c9745101d12aed4d5a67d43747824451f9251d4\&per_page=10\&page=2

### Mostrar cola de boletos
    curl https://app.mojohelpdesk.com/api/v2/ticket_queues/8?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear cola de tickets

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/ticket_queues?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"name":"My queue"}'

### Actualizar cola de tickets

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/ticket_queues/11?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X PUT -d '{"name":"My precious queue"}'

### Destruir la cola de boletos

    curl https://app.mojohelpdesk.com/api/v2/ticket_queues/10?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE

## Grupos (anteriormente llamados empresas)

### Lista de grupos

    curl https://app.mojohelpdesk.com/api/v2/groups?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### La lista de grupos admite paginación, con parámetros opcionales por_página y parámetros de página. Si falta per_page, de forma predeterminada devolverá 30 elementos por página

    curl https://app.mojohelpdesk.com/api/v2/groups?access_key=9c9745101d12aed4d5a67d43747824451f9251d4\&per_page=10\&page=2

### Crea un grupo

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/groups?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"name":"My very own group"}'

### Actualizar grupo

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/groups/1999?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X PUT -d '{"website-url":"www.google.com"}'

### Destruir grupo

    curl https://app.mojohelpdesk.com/api/v2/groups/1999?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE

## Usuarios

### Lista de usuarios

    curl https://app.mojohelpdesk.com/api/v2/users?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Lista de agentes

    curl https://app.mojohelpdesk.com/api/v2/users/techs?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### La lista de usuarios admite paginación, con parámetros opcionales por_página y parámetros de página. Si falta per_page, de forma predeterminada devolverá 30 elementos por página

    curl https://app.mojohelpdesk.com/api/v2/users?access_key=9c9745101d12aed4d5a67d43747824451f9251d4\&per_page=10\&page=2

### Mostrar usuario

    curl https://app.mojohelpdesk.com/api/v2/users/1?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Obtener usuario por dirección de correo electrónico

    curl https://app.mojohelpdesk.com/api/v2/users/get_by_email?email=someone@company.com&access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear usuario

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/users?access_key=9c9745101d12aed4d5a67d43747824451f9251d4\&send_welcome_email=1 -X POST -d '{"email":"ivaylo+test@metadot.com","first_name":"Ivaylo","last_name":"Georgiev","company_id":"888","password":"111111"}'

### Actualizar usuario

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/users/1999?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X PUT -d '{"user_notes":"Thats me again."}'

### Destruir usuario

    curl https://app.mojohelpdesk.com/api/v2/users/1999?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE

## Etiquetas de entradas

### Lista de etiquetas de entradas

    curl https://app.mojohelpdesk.com/api/v2/tags?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### La lista de etiquetas admite la paginación, con parámetros opcionales por_página y parámetros de página. Si falta per_page, de forma predeterminada devolverá 30 elementos por página

    curl https://app.mojohelpdesk.com/api/v2/tags?access_key=9c9745101d12aed4d5a67d43747824451f9251d4\&per_page=10\&page=2

### Mostrar etiqueta

    curl https://app.mojohelpdesk.com/api/v2/tags/8?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear etiqueta

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tags?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"label":"Test","color":"#777777"}'

### Actualizar etiqueta

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tags/11?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X PUT -d '{"color":"#ff0000"}'

### Destruir etiqueta

    curl https://app.mojohelpdesk.com/api/v2/tags/10?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE

## Tareas de tickets

### Lista de tareas del ticket

    curl https://app.mojohelpdesk.com/api/v2/tickets/88/tasks?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear tarea de ticket

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets/88/tasks?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"title":"Test"}'

### Actualizar tarea de ticket

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/tickets/88/tasks/777?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X PUT -d '{"notes":"Help"}'

### Destruir tarea de ticket

    curl https://app.mojohelpdesk.com/api/v2/tickets/88/tasks/777?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE

## Derechos de acceso a las colas de tickets

### Lista de derechos de acceso para agentes restringidos

    curl https://app.mojohelpdesk.com/api/v2/access_rights/restricted_agents?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Lista de derechos de acceso para grupos

    curl https://app.mojohelpdesk.com/api/v2/access_rights/groups?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Mostrar derechos de acceso para un agente restringido

    curl https://app.mojohelpdesk.com/api/v2/users/1819458/access_rights?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Mostrar derechos de acceso para un grupo

    curl https://app.mojohelpdesk.com/api/v2/groups/124147/access_rights?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Establezca el derecho de acceso para un agente restringido en una sola cola

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/users/1819458/access_rights?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"ticket_queue_id":"94748","has_access":"true"}'

### Establezca el derecho de acceso para un agente restringido en varias colas

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/users/1819458/access_rights/set?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"keys":["94748","15"],"has_access":"true"}'

### Establecer el derecho de acceso para un grupo en una sola cola

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/groups/124147/access_rights?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"ticket_queue_id":"94748","has_access":"true"}'

### Establecer el derecho de acceso para un grupo en todas las colas

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/groups/124147/access_rights?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"has_access_to_all_ticket_queues":"true"}'

### Establecer el derecho de acceso para un grupo en varias colas

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/groups/124147/access_rights/set?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"keys":["94748","15"],"has_access":"true"}'


## Formularios de entradas

### Lista de formularios de ticket

    curl https://app.mojohelpdesk.com/api/v2/ticket_forms?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

List all forms with some basic information for them.

### Mostrar formularios de ticket

    curl https://app.mojohelpdesk.com/api/v2/ticket_forms/2700?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

Returns all relevant information for a form, including the list of field attributes, and field rules.

## Acceso a tickets grupales para usuarios

### Listar todos los accesos de tickets de grupos para un usuario

    curl https://app.mojohelpdesk.com/api/v2/users/14/group_access?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Obtenga acceso a tickets de un solo grupo para un usuario

    curl https://app.mojohelpdesk.com/api/v2/users/14/group_access/1234?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Establecer acceso a tickets de un solo grupo para un usuario

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/users/14/group_access/1234?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"access":"1"}'

## Tipos de boletos

### Lista de tipos de boletos

    curl https://app.mojohelpdesk.com/api/v2/ticket_types?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Mostrar tipo de entrada

    curl https://app.mojohelpdesk.com/api/v2/ticket_type/8?access_key=9c9745101d12aed4d5a67d43747824451f9251d4

### Crear tipo de boleto

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/ticket_types?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X POST -d '{"name":"My type"}'

### Actualizar tipo de boleto

    curl -H 'Content-type: application/json' https://app.mojohelpdesk.com/api/v2/ticket_types/11?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X PUT -d '{"name":"My precious type"}'

### Destruir tipo de ticket

    curl https://app.mojohelpdesk.com/api/v2/ticket_types/10?access_key=9c9745101d12aed4d5a67d43747824451f9251d4 -X DELETE
    
Y esto sería todo o practicamente todo lo que se puede hacer en Mojo-HelpDesk.
