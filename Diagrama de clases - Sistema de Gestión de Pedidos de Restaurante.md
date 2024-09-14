# TP1 - Practica de UML

## 2. Sistema de Gestión de Pedidos de Restaurante

Se desea desarrollar un sistema para gestionar los pedidos de un restaurante. El sistema debe permitir registrar los pedidos que realizan los clientes, asociarlos a las mesas y hacer un seguimiento del estado de cada pedido.

**Requisitos:**

- Un pedido contiene uno o varios platos, y cada plato tiene un nombre, un precio y una
categoría (entrada, plato principal, postre).
- Un cliente puede hacer varios pedidos, y un pedido puede estar asociado a una mesa del
restaurante.
- Las mesas tienen un número de identificación único.
- Los pedidos tienen un estado (pendiente, en preparación, servido) y una hora de creación.

### Diagrama de clases

```mermaid
classDiagram

    class Pedido {
        - estado : EstadoPedido
        - horaCreacion : DateTime
        
        + actualizarEstado() : void
        + agregarPlato(plato : Plato, cantidad : int) : void
    }

    class Plato {
        - nombre : String
        - precio : double
        - categoria : CategoriaPlato
        - estado : EstadoPlato
    }

    class Cliente {
        - nombre : String
        - apellido : String

        + hacerPedido() : void
    }

    class Mesa {
        - idMesa : int
        
        + asociarPedido() : void 
    }

    class EstadoPedido {
        <<enumeration>>
        
        PENDIENTE
        EN_PREPARACION
        SERVIDO
        DEVUELTO
        CANCELADO
    }

    class CategoriaPlato {
        <<enumeration>>
        
        ENTRADA
        PLATO_PRINCIPAL
        POSTRE
    }

    class EstadoPlato {
        <<enumeration>>
        
        DISPONIBLE
        NO_DISPONIBLE
    }

    Cliente "1" -- "0..*" Pedido : realiza
    Pedido "1" -- "1" Mesa : se asocia
    Pedido "0..*" o-- "1..*" Plato : tiene
    Plato -- CategoriaPlato
    Pedido -- EstadoPedido
    Plato -- EstadoPlato

```

#### Aclaración

Algunos atributos y/o métodos no eran pedidos expresos en la consigna, pero creí que era apropiado agregarlos.
