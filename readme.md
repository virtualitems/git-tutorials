# Guía de Git basada en ejemplos

Cada página parte de un caso, explica el cambio de estado y deriva el modelo de Git que interviene. El inventario procede de `sitemap.xml` y contiene una guía por cada URL.

## Secciones

- [Mapa de la referencia](overview/README.md) (1 páginas)
- [Configuración y entorno](setup-and-config/README.md) (6 páginas)
- [Creación y obtención de proyectos](getting-and-creating-projects/README.md) (3 páginas)
- [Área de trabajo, índice y commits](basic-snapshotting/README.md) (8 páginas)
- [Ramas y fusiones](branching-and-merging/README.md) (12 páginas)
- [Aplicación y reorganización de cambios](patching/README.md) (5 páginas)
- [Búsqueda y depuración](debugging/README.md) (4 páginas)
- [Inspección y comparación](inspection-and-comparison/README.md) (12 páginas)
- [Repositorios remotos](sharing-and-updating-projects/README.md) (8 páginas)
- [Administración del repositorio](administration/README.md) (14 páginas)
- [Interfaces gráficas y web](graphical-tools/README.md) (5 páginas)
- [Parches por correo](email-and-patches/README.md) (4 páginas)
- [Integración con otros sistemas](external-systems/README.md) (9 páginas)
- [Plomería para modificar datos internos](plumbing-write/README.md) (18 páginas)
- [Plomería para consultar datos internos](plumbing-read/README.md) (23 páginas)
- [Servidor y transporte](server-and-transport/README.md) (11 páginas)
- [Automatización y comandos auxiliares](scripting-and-helpers/README.md) (19 páginas)
- [Guías conceptuales](guides/README.md) (21 páginas)
- [Formatos y protocolos](formats-and-protocols/README.md) (11 páginas)

## Ruta de aprendizaje

1. Empieza por [el mapa de la referencia](overview/reference-index.md).
2. Recorre [creación de proyectos](getting-and-creating-projects/README.md) y [snapshots](basic-snapshotting/README.md).
3. Continúa con [ramas](branching-and-merging/README.md), [comparación](inspection-and-comparison/README.md) y [remotos](sharing-and-updating-projects/README.md).
4. Usa [plomería de lectura](plumbing-read/README.md) antes de [plomería de escritura](plumbing-write/README.md).
5. Consulta [formatos y protocolos](formats-and-protocols/README.md) cuando necesites interpretar datos internos o tráfico entre procesos.

## Convenciones

Los ejemplos usan nombres como `main`, `tema-portada` y `biblioteca`. Los dominios `example.test` no representan servicios reales. Ejecuta operaciones de escritura en un repositorio temporal hasta comprobar su efecto.
