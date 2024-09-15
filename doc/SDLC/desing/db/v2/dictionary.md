# Base de datos v2
Todas las entidades y atributos son esenciales para los requeriminetos del sistema **modularizados en microservicios**
> [!IMPORTANT]
> Esta es la primera version de la base de datos no esta acorde con el objetivo que es implementar micro servicios
> , por lo anterior se infiere es que de esta version se desacoplara distintos sistemas como
> usuarios, transacciones, negocio
## BD Gestion de habitacion
Son las entidades para manejar toda la información relacionada con las habitaciones, incluyendo su estado (disponible, ocupada, reservada), tipos de habitaciones, número de camas, y características adicionales (como vistas, comodidades).

**Hotel**
```mermaid
---

---
erDiagram
    hotel{
        int id_hotel PK
        int number_of_floors "La cantidad de pisos es importante para la nomenclatura de las piezas"
        int year_of_inauguration
        int antiquity "La antiguedad es derivada del año de inauguración"
        float category
        string address
        string name
    }
    phone_hotel{
        int id_hotel PK,FK
        int phone PK
    }
```
**Habitación**: El costo de una habitacion dependera del tipo de habitación y de la categoria del hotel
```mermaid
---

---
erDiagram
    room{
        int id_hotel PK,FK
        int floor PK
        int cost "El costo dependera de la categoria y el tipo de abitación"
        int type_of_room FK
        int id_reservation FK
    }
    type_room{
        int id_type_room PK
        int number_of_beds
        string description
    }
```
## Gestion de reservas
Son las entidades que de alguna u otra forma esta relacionada con la reserva por ejemplo el *registro* del usuario al llegar al hotel.

Manejar todo el ciclo de vida de las reservas de los clientes, desde la creación de una reserva hasta su confirmación y finalización.

**reservation**: La reservacion que hace o la agencia o el usuario responsable.

**service**: Servicios que puede tener la reservacion, por ejemplo:
 - Cuidado de mascotas
 - Parqueadero

**registration**: Registro de la reserva y la habitacion

**registration_guest**: Registro que asocia la habitacion al usuario
```mermaid
---
title: Entidades de reserva
---
erDiagram
    reservation{
        int id_reservation PK
        int id_hotel FK "id de la sala"
        int floor FK "id de la sala"
        int id_agency FK
        int number_of_people
        int cost
        boolean status
        date date_registration
        date date_init
        date date_end
    }
    service_reservation{
        int id_reservation PK,FK
        int id_service PK,FK
    }
    service{
        int id_service PK
        int cost
        string name
    }
    registration{
        int id_reservation PK,FK
        int id_hotel PK,FK "id de la sala"
        int floor PK,FK "id de la sala"
        boolean minor
        boolean pet
    }
    registration_guest{
        int id_reservation PK,FK
        int id_hotel PK,FK "id de la sala"
        int floor PK,FK "id de la sala"
        int id_user PK,FK "id del usuario"
        int id_guest PK,FK "id del usuario"
    }
```
## Facturacion
Manejar todo lo relacionado con los pagos, facturas y métodos de pago.

**invoice_fee_reservation**: Las cuotas de pago de la reserva

**method_of_payment**: Metodos de pago que tiene la plataforma
```mermaid
---
title: Entidades de registro
---
erDiagram
    invoice_fee_reservation{
        int id_reservation PK,FK
        int id_fee PK
        int value
        int id_method_of_payment FK
        date date_registration
    }
    method_of_payment{
        int id_method_of_payment PK
        string name
    }
```

## Gestion de usuarios
Son las entidades encargadas de definir roles y datos de todos los usuarios del sistema.

Gestionar tanto los perfiles de los huéspedes como del personal del hotel, con roles y permisos específicos.

**user**: Usuario del sistema

**agency**: Tipo de usuario (Rol)

**guest**: Tipo de usuario (Rol)

**employee**: Tipo de usuario (Rol)

```mermaid
---
title: Entidades de usuario
---
erDiagram
    user{
        int id_user PK
        string name
        string address
    }
    user_phone{
        int id_user PK,FK
        int phone PK
        int country_code
    }
    agency{
        int id_user PK,FK
        int id_agency PK
        string name_of_agency
    }
    guest{
        int id_user PK,FK
        int id_guest PK
        int age
    }
    employee{
        int id_user PK,FK
        int id_employee PK
        int id_hotel FK
        string role
    }
```
## Otras entidades
Estas son entidades del sistema, datos que se usaran para algun analisis o otra funcionalidad.

**log_category_update_hotel**: Los hoteles inician por defecto una categoria de 0 y al momento de poner su verdadera categoria se genera un log ese debera ser el primer log y la categoria verdadera del hotel
```mermaid
---
title: Otras entidades
---
erDiagram
    log_category_update_hotel{
        int id_log PK
        int id_holtel PK,FK
        floar new_category "La categoria nueva"
        date date_registration
    }
```