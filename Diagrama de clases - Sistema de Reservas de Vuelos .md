# TP1 - Practica de UML

## 3. Sistema de Reserva de Vuelos

Se desea modelar un sistema de reservas de vuelos. El sistema permite a los clientes buscar y reservar vuelos, que conectan aeropuertos específicos en determinadas fechas y horas.

**Requisitos:**

- Un vuelo tiene un número de vuelo, una aerolínea, una fecha y una hora de salida y llegada,
y está asociado a un avión.
- Los clientes pueden reservar asientos en los vuelos, y cada reserva tiene un número de
confirmación, la fecha de la reserva y el asiento asignado.
- Cada avión tiene un modelo, una capacidad máxima de pasajeros y pertenece a una
aerolínea.
- Los aeropuertos tienen un código único, un nombre y una ciudad.

### Diagrama de clases

```mermaid
classDiagram

    class Vuelo {
        - numVuelo : int
        - salida : DateTime
        - llegada : DateTime
        - avion : Avion
        - aerolinea : Aerolinea
        - aeropuertoSalida : Aeropuerto
        - aeropuertoLlegada : Aeropuerto
        - estado : estadoVuelo

        + cambiarEstado(estado : EstadoVuelo) : void
    }

    class Cliente {
        - dni : int
        - nombre : String
        - apellido : String
        - reservas[] : Reserva
        
        + reservarVuelo(vuelo : Vuelo, numAsientos[] : int) : void
    }

    class Reserva {
        - numConfirmacion : int
        - fechaReserva : Date
        - estado : EstadoReserva
        - vuelo : Vuelo
        - asientosAsignados[] : int

        + cambiarEstado(estado : EstadoReserva) : void 
    }

    class Aerolinea {
        - nombre : String
        - vuelos[] : Vuelo
        
        + agregarVuelo() : void
        + reprogramarVuelo(salida : DateTime) : void
    }

    class Aeropuerto {
        - codigo : int
        - nombre : String
        - ciudad : String
        - vuelos[] : Vuelo
    }

    class Avion {
        - matricula : String
        - modelo : String
        - capacidadMaxima : int
        - aerolinea : Aerolinea
        - asientos[] : Asiento

        + ocuparAsientos(asientosParaOcupar[] : int) : void
    }

    class Asiento {
        - numero : int
        - estado : EstadoAsiento
        
        + cambiarEstado(estado : EstadoAsiento) : void
    }

    class EstadoReserva {
        <<enumeration>>
        
        ABIERTA
        CERRADA
        CANCELADA
    }

    class EstadoAsiento {
        <<enumeration>>
        
        LIBRE
        OCUPADO
    }

    class EstadoVuelo {
        <<enumeration>>
        
        PROGRAMADO
        EMBARCANDO
        EN_RUTA
        ATRASADO
        CANCELADO
        DESVIADO
        FINALIZADO
    }

    Vuelo "1" --> "1" Avion : asignado
    Vuelo "1" --> "1" Aeropuerto : salida
    Vuelo "1" --> "1" Aeropuerto : llegada
    Aerolinea "1" --o "0..*" Vuelo : tiene
    Cliente "1" --o "0..*" Reserva : realiza
    Reserva "1" -- "1" Vuelo : se asocia
    Reserva "1" -- "1..*" Asiento : reserva
    Avion "1" -- "1" Aerolinea : pertenece
    Avion "1" --* "*" Asiento : tiene
    Vuelo -- EstadoVuelo
    Asiento -- EstadoAsiento
    Reserva -- EstadoReserva

```

#### Aclaración

Algunos atributos y/o métodos no eran pedidos expresos en la consigna, pero creí que era apropiado agregarlos.
