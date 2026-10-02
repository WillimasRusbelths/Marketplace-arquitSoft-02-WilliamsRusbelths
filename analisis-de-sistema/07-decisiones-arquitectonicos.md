# Decisiones arquitectónicas

Las siguientes decisiones definen cómo se organizará el marketplace de productos para mascotas. Cada decisión responde a uno o más drivers arquitectónicos identificados en el análisis del sistema.

Un ADR (Architecture Decision Record) es un registro que documenta una decisión arquitectónica y su justificación.

## Registro de decisiones

| ID | Decisión arquitectónica | Driver relacionado | Justificación | Resultado esperado |
|---|---|---|---|---|
| ADR-001 | Monolito modular | DA01 — Escalabilidad; DA06 — Mantenibilidad | Organizar las funcionalidades en módulos con responsabilidades definidas dentro de una misma aplicación desplegable. Permite comenzar con un despliegue sencillo y preparar la aplicación para ejecutar varias instancias cuando aumente la demanda. | Módulos de Usuarios, Catálogo, Carrito, Pedidos y Pagos dentro de una misma aplicación. |
| ADR-002 | Clean Architecture | DA06 — Mantenibilidad | Separar las reglas de negocio de la interfaz de usuario y de los detalles tecnológicos. Las dependencias del código deben apuntar hacia el núcleo del negocio. | Organización en Dominio, Aplicación, Infraestructura y Presentación. |
| ADR-003 | Estrategia de caché | DA02 — Rendimiento | Reducir las consultas repetitivas a la fuente de datos para mejorar los tiempos de respuesta durante una alta concurrencia. | Caché para consultas frecuentes del catálogo, con reglas de expiración e invalidación cuando cambien los datos. |
| ADR-004 | Integración de pagos mediante interfaces y adaptadores | DA04 — Pasarela de pago | Desacoplar los casos de uso del proveedor de pagos para facilitar su mantenimiento o sustitución. | Una interfaz de pagos definida en Aplicación y un adaptador de la pasarela externa implementado en Infraestructura. |

## Consideraciones

- El monolito modular requiere mantener límites claros entre sus módulos. El escalamiento horizontal también exige revisar el manejo de sesiones y el acceso a la base de datos.
- Clean Architecture requiere respetar la dirección de las dependencias para conservar la independencia de las reglas de negocio.
- La caché debe actualizarse o invalidarse para evitar mostrar información desactualizada. El stock y el precio deben verificarse al confirmar la compra.
- El adaptador de pagos debe gestionar errores de comunicación y evitar el procesamiento duplicado de una misma operación.