# Base de datos v1
Todas las entidades y atributos son esenciales para los requeriminetos del sistema
> [!IMPORTANT]
> Esta es la primera version de la base de datos no esta acorde con el objetivo que es implementar micro servicios
> , por lo anterior se infiere es que de esta version se desacoplara distintos sistemas como
> usuarios, transacciones, negocio
## Entidades negocio en general
Son entidades generales del negocio
```mermaid
---
title: Entidades generales de negocio
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
## Entidades que reserva
Son las entidades que de alguna u otra forma esta relacionada con la reserva por ejemplo el *registro* del usuario al llegar al hotel
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
## Entidades de usuario
Son las entidades encargadas de definir roles y datos de todos los usuarios del sistema
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
## Diagrama relacional v1
Este diagrama no sera el definitivo pero es el mas fiel a los requerimientos dados por la [premisa](../../planning/problem.md)
```mermaid
---
title: Diagrama relacional
---
erDiagram
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
    reservation ||--|{ room : reserved
    type_room ||--|{ room : has_a_type
    room{
        int id_hotel PK,FK
        int floor PK
        int type_of_room FK
        int id_reservation FK
    }
    type_room{
        int id_type_room PK
        int cost
        int number_of_beds
        string description
    }
    agency o|--|{ reservation : has
    guest ||--|{ reservation : responsible
    reservation{
        int id_reservation PK
        int id_agency FK
        int id_user FK
        int id_guest FK
        int number_of_people
        int cost
        boolean status
        date date_registration
        date date_init
        date date_end
    }
    reservation ||--o{ service_reservation : acquires
    service ||--o{ service_reservation : use
    service_reservation{
        int id_reservation PK,FK
        int id_service PK,FK
    }
    service{
        int id_service PK
        int cost
        string name
    }
    reservation ||--|{ invoice_fee_reservation : payment
    method_of_payment || --|{invoice_fee_reservation: use
    invoice_fee_reservation{
        int id_reservation PK,FK
        int id_fee PK
        int value
        int id_method_of_payment FK
        date date_registration
    }
    user ||--|{ agency : is
    agency{
        int id_agency PK
        string name_of_agency
    }
    method_of_payment{
        int id_method_of_payment PK
        string name
    }
    reservation ||--|{ registration : has
    room ||--|{ registration : host
    registration{
        int id_reservation PK,FK
        int id_hotel PK,FK
        int floor PK,FK
        boolean minor
        boolean pet
    }
    registration ||--|{ registration_guest: accommodate
    guest ||--|{ registration_guest: accommodate
    registration_guest{
        int id_reservation PK,FK
        int id_hotel PK,FK
        int floor PK,FK
        int id_user PK,FK
        int id_guest PK,FK
    }
    user{
        int id_user PK
        int age
        string name
        string address
    }
    user ||--|{ user_phone : use
    user_phone{
        int id_user PK,FK
        int phone PK
        int country_code
    }
    user ||--|{ guest : is
    guest{
        int id_user PK,FK
        int id_guest PK
    }
    user ||--|{ employee : is
    hotel ||--|{employee: has
    employee{
        int id_user PK,FK
        int id_employee PK
        int id_hotel FK
        string role
    }
```