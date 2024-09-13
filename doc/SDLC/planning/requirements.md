# Requerimientos
## Requerimientos del negocio
### Reglas explicitas
- LLevar el log de cambios en la categoria de cada hotel
- Cada habitacion tiene una identificacion particular para lograr identificarlas al momento de asignarlas (Nomenclatura)
- La categorizacion del hotel va de estrellas 5,4,...1
- Las habitaciones pueden ser reservadas por los huespedes directamente
- El valor del 20% de la reserva debera cancelarse antes de 24 horas, si no la reserva pasara a inactiva y por ende sus habitaciones liberadas
- El 80% de la reserva se cancela en el registro dentro del rango horario de  3 pm hasta las 7 pm
- Si no se cancela el 80% de la reserva en el rango estipulado la reserva queda inactiva
- Se debe de adicionar costos a la reserva y al finalizar deberan culminar 100% de los costos por servicios extra
- Los huespedes para entragar las habitaciones deberan cancelar el 100% de reserva con servicios excla incluidos
- El costo de una habitacion dependera del tipo de habitación y de la categoria del hotel
**Se debe poder consultar los siguientes datos**
- Reservas realizadas en un período de tiempo.
- Reservas que fueron canceladas sin pagar el valor del 20% de anticipo.
- Reservas que no fueron utilizadas y pagaron el 20% de anticipo.
- Reservas que tuvieron registro de llegada de los huéspedes a tiempo (registraron 3 pm a 7 pm de lo contrario no llegaron a tiempo).
- Reservas que registraron huéspedes menores de edad y/o mascotas.
- Reservas que pagaron servicios adicionales.
- Datos de los huéspedes correspondientes a una reserva particular.

### Entidades
|Entidad|Atributos|Relacion|
|------|------|------|
|Hotel|Id_Hotel,numero de pisos,Nombre, Direccion,Telefonos (multivalueado),Año de inauguracion, Antiguedad, Categoria|Tiene(1:M)Habitaciones|
|Habitacion|Id_Hotel,piso,Tipo de habitacion|pertenece_a(M:1)Tipo de habitacion|
|Huesped|numero de identificacion, nombre, direccion,telefonos,edad||
|Agencia|identificacion,nombre|Hacer(M:N)Reserva|
|Reserva|id_reserva,id_responsable,agencia,fecha de registro,fecha de inicio de reserva, fecha de fin de la reserva,cantidad de personas, cantidad de habitaciones,habitaciones(multivalueado)servicios adicionales(mutivaluado),costo,ctiva,facturas(multivaluado)|
|Registro|id_reserva,id_habitacion,huespedes(multivaluado)||
|Tipo de habitacion|id,costo,numero de camas||
|Usuario|||
|Empleado|||



## Requerimientos del sistema

- 1 base de datos relacional
