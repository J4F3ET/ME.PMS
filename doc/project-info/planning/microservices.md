# Microservicios del sistema

## Gestion de habitaciones
**Responsabilidad**: Manejar toda la informacion relacionada con el hotel, incluyendo su categoria y sus cambios de categoria.<br>
**Responsabilidad**: Manejar toda la información relacionada con las habitaciones, incluyendo su estado (disponible, ocupada, reservada), tipos de habitaciones, número de camas, y su costo.
- **Funciones**:
  - CRUD de habitaciones.
  - Consulta de estado de habitaciones.
  - Actualizar estado de habitacion.
  - Definición de precios en función de características (número de camas, categoría del hotel, etc.).
  - Cambio de categoria del hotel.
  - Cambio de precios de las habitaciones de un hotel
  - Registro de cambio de categoria de un hotel

## Gestion de reservas
**Responsabilidad**: Manejar todo el ciclo de vida de las reservas de los clientes, desde la creación de una reserva hasta su confirmación y finalización.
- **Funciones**:
  - CRUD de reservas
  - Creación y cancelación de reservas.
  - Asociación de habitaciones a una reserva.
  - Revisión de historial de reservas.
  - Modificación de reservas (cambios en fechas o habitaciones).
  - Cancelacion por tiempo de expiracion de pagos de una reserva.
  - Calcular costos de una reserva (deacuerdo a servicios adicionales costos de habitacion)

## Gestion de registros
 **Responsabilidad**:  Gestionar los registro del los usuarios responsables y los invitados del usuario al hotel.
 - **Funciones**
   - Registrar el ingreso de los huespedes de una reserva
   - Asociar registro a habitacion y a huesped
   - Cada huesped alojado tiene un usuario resposable asociado a el

## Gestion de usuarios
**Responsabilidad**: Gestionar tanto los perfiles de los huéspedes como del personal del hotel, con roles y permisos específicos.
- **Funciones**:
  - Registro y autenticación de usuarios.
  - Administración de perfiles (huéspedes, administradores, recepcionistas).
  - Asignación de roles y permisos.
  - Consultar historial de estancias de un huésped.
## Facturacion
**Responsabilidad**: Manejar todo lo relacionado con los pagos, facturas y métodos de pago.
- **Funciones**:
  - Generación de facturas basadas en reservas.
  - Integración con pasarelas de pago.
  - Registro de pagos parciales o totales.
  - Control de facturas y gestión de cobros.
---
## Proximamente
- **Gestor de tarifas**: Controlar y definir las tarifas de las habitaciones basadas en varios factores como la temporada, ocupación y categoría del hotel.
- **Gestor servicios adicionales**: Manejar los servicios adicionales que el hotel ofrece (desayuno, lavandería, transporte, etc.) y su facturación.
- **Notificacion y comunicacion**: Manejar el envío de notificaciones a los usuarios y el personal, tanto por email como por SMS o push notifications.