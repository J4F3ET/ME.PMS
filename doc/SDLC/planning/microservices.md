# Microservicios del sistema

## Gestion de habitaciones
**Responsabilidad**: Manejar toda la información relacionada con las habitaciones, incluyendo su estado (disponible, ocupada, reservada), tipos de habitaciones, número de camas, y características adicionales (como vistas, comodidades).
- **Funciones**:
  - CRUD de habitaciones.
  - Consulta de disponibilidad.
  - Definición de precios en función de características (número de camas, categoría, etc.).
## Gestion de reservas
**Responsabilidad**: Manejar todo el ciclo de vida de las reservas de los clientes, desde la creación de una reserva hasta su confirmación y finalización.
- **Funciones**:
  - Creación y cancelación de reservas.
  - Asociación de habitaciones a una reserva.
  - Revisión de historial de reservas.
  - Modificación de reservas (cambios en fechas o habitaciones).
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