# Arquitectura inicial del sistema

## Organización en tres capas

| Capa | Responsabilidad | Elementos |
|---|---|---|
| Presentación | Permitir que los usuarios interactúen con el marketplace. | Aplicación web y API REST. |
| Lógica de negocio | Ejecutar las funciones y reglas del marketplace. | Usuarios, sellers, catálogo, carrito y pedidos. |
| Datos | Almacenar y consultar la información del sistema. | Base de datos. |

El cliente, el seller y el administrador interactúan mediante la aplicación web. Las solicitudes llegan a los módulos de lógica de negocio a través de la API REST. Estos módulos consultan o guardan información en la base de datos.

El sistema también se relaciona con una pasarela de pago y un servicio de envío externos para completar las operaciones asociadas a los pedidos.


## Diagrama de arquitectura

```mermaid
flowchart TD
    subgraph Actores
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    subgraph Presentacion["PRESENTACIÓN"]
        Web["Aplicación web"]
        API["API REST"]
    end

    subgraph Negocio["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
    end

    subgraph Datos["DATOS"]
        BD["Base de datos"]
    end

    subgraph Externos["SISTEMAS EXTERNOS"]
        Pago["Pasarela de pago"]
        Envio["Servicio de envío"]
    end

    Cliente --> Web
    Seller --> Web
    Admin --> Web
    Web --> API

    API --> Usuarios
    API --> Sellers
    API --> Catalogo
    API --> Carrito
    API --> Pedidos

    Usuarios --> BD
    Sellers --> BD
    Catalogo --> BD
    Carrito --> BD
    Pedidos --> BD

    Pedidos --> Pago
    Pedidos --> Envio
```

## Descripción del diagrama

Los actores utilizan la aplicación web, que se comunica con los módulos del sistema mediante la API REST. Los módulos de lógica de negocio consultan y almacenan información en la base de datos. El módulo de pedidos se integra con la pasarela de pago y el servicio de envío.
