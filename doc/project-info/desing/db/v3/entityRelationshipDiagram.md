# Base de datos v3
Todas las entidades y atributos son esenciales para los requeriminetos del sistema **modularizados en microservicios**
> [!IMPORTANT]
> Esta es la tercera version del diccionario de datos de la base de datos
> contiene las entidades tablas de cada microservicio
## Gestion de habitaciones
```mermaid
---
title: BD Gestion de habitacion
---
erDiagram
    hotel ||--|{ log_category_update_hotel : register
    log_category_update_hotel{
        int id_log PK
        int id_holtel PK,FK
        floar new_category
        date date_registration
    }
    hotel{
        int id_hotel PK
        int number_of_floors
        int year_of_inauguration
        int antiquity
        float category
        string address
        string name
    }
    hotel ||--|{ phone_hotel : use
    phone_hotel{
        int id_hotel PK,FK
        int phone PK
    }
    hotel ||--|{ room : has
    room{
        int id_hotel PK,FK
        int floor PK
        int cost
        boolean status
        int type_of_room FK
    }
    type_room ||--|{ room : define
    type_room{
        int id_type_room PK
        int number_of_beds
        string description
    }
```
## Gestion de reservas
```mermaid
---
title: BD Gestion de reservas
---
erDiagram
    id_responsible_guest{
        int id_user PK
        int id_guest PK
    }
    id_agency{
        int id_user PK
        int id_agency PK
    }
    id_responsible_guest ||--|{ reservation : responsible
    id_agency ||--|{ reservation : responsible
    reservation{
        int id_reservation PK
        int id_user FK
        int id_guest FK
        int id_agency FK
        int id_user_agency FK
        int number_of_people
        int cost
        boolean status
        date date_registration
        date date_init
        date date_end
    }
    id_room{
        int id_hotel PK
        int floor PK
    }
    id_room ||--|{ reservation_room : reserved
    reservation ||--|{ reservation_room : reserve
    reservation_room{
        int id_reservation PK,FK
        int id_hotel PK,FK
        int floor PK,FK
    }
    reservation ||--|{ service_reservation : request
    service ||--|{ service_reservation : use
    service_reservation{
        int id_reservation PK,FK
        int id_service PK,FK
    }
    service{
        int id_service PK
        int cost
        string name
    }
```
## Gestion de registros
```mermaid
---
title: BD Gestion de reservas
---
erDiagram
    id_reservation{
        int id_reservation PK
    }
    id_responsible_guest{
        int id_user PK
        int id_guest PK
    }
    id_responsible_guest ||--|{ no_user_guest : responsible
    no_user_guest{
        int id_user PK,FK
        int id_guest PK,FK
        int id_no_user_guest PK
        string name
    }
    id_room{
        int id_hotel PK
        int floor PK
    }
    id_room ||--|{ registration : reserved
    id_reservation ||--|{ registration : income
    registration{
        int id_reservation PK,FK
        int id_hotel PK,FK
        int floor PK,FK
        boolean minor
        boolean pet
    }
    registration ||--|{ registration_guest : reserved
    no_user_guest ||--|{ registration_guest : reserved
    registration_guest{
        int id_reservation PK,FK
        int id_hotel PK,FK
        int floor PK,FK
        int id_user PK,FK
        int id_guest PK,FK
        int id_no_user_guest PK,FK
    }
```
## Facturacion
```mermaid
---
title: BD facturacion
---
erDiagram
    method_of_payment ||--|{ invoice_fee_reservation: use
    reservation ||--|{ invoice_fee_reservation: pay
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
    reservation{
        int id_reservation PK
        int cost
    }
```
## Gestion de usuarios
```mermaid
---
title: BD Gestion de usuarios
---
erDiagram
    user{
        int id_user PK
        string name
        string email
        string password
        string address
    }
    user ||--|{ user_phone:has
    user_phone{
        int id_user PK,FK
        int phone PK
        int country_code
    }
    user ||--|{ agency: is
    agency{
        int id_user PK,FK
        int id_agency PK
        string name_of_agency
    }
    user ||--|{ guest:is
    guest{
        int id_user PK,FK
        int id_guest PK
        int age
    }
    user ||--|{ employee:is
    employee{
        int id_user PK,FK
        int id_employee PK
        int id_hotel FK
        string role
    }
```