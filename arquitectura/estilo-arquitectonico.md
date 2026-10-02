## Diagrama del estilo arquitectónico

```mermaid
flowchart TB
    actores["Cliente, Seller y Administrador"]
    web["Frontend web"]

    subgraph monolito["Backend — Monolito modular"]
        direction TB

        subgraph presentacion["Capa de presentación"]
            api["API REST y controladores"]
        end

        subgraph negocio["Capa de lógica de negocio"]
            modulos["Módulos: Usuarios, Catálogo, Carrito, Pedidos y Pagos"]
        end

        subgraph datos["Capa de acceso a datos e integraciones"]
            repositorios["Repositorios"]
            adaptadores["Adaptadores de servicios externos"]
        end

        api --> modulos
        modulos --> repositorios
        modulos --> adaptadores
    end

    bd[("Base de datos")]
    pasarela["Pasarela de pago externa"]

    actores --> web
    web -->|"HTTPS / REST"| api
    repositorios --> bd
    adaptadores -->|"API del proveedor"| pasarela
```

El backend utiliza un estilo monolítico modular: sus módulos y capas forman parte de una misma aplicación y se despliegan juntos.

La organización por capas separa las siguientes responsabilidades:

- **Presentación:** recibe las solicitudes del frontend mediante la API REST.
- **Lógica de negocio:** aplica las reglas y coordina las operaciones de los módulos.
- **Acceso a datos e integraciones:** gestiona la persistencia y la comunicación con servicios externos.

El frontend, la base de datos y la pasarela de pago se encuentran fuera del monolito del backend. Las flechas representan llamadas entre componentes de la arquitectura propuesta.