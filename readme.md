# Guía técnica de Git basada en ejemplos

El conjunto contiene una guía canónica para cada URL de `sitemap.xml`. Cada página define responsabilidad, estado leído y escrito, laboratorio, sintaxis, casos de uso, opciones, selección de entradas, códigos de terminación, diagnóstico, automatización y recuperación.

## Cobertura

- URLs del sitemap: **194**.
- Guías canónicas: **194**.
- URLs sin guía: **0**.
- Guías canónicas fuera del sitemap: **0**.
- Rutas duplicadas conservadas y documentadas: **28**.
- Archivos Markdown vacíos: **0**.

La correspondencia completa está en [`coverage-report.tsv`](coverage-report.tsv). El archivo [`sitemap.xml`](sitemap.xml) acompaña la entrega para repetir la validación.

## Secciones

- [Mapa de la referencia](overview/README.md): 1 páginas canónicas.
- [Configuración y entorno](setup-and-config/README.md): 6 páginas canónicas.
- [Creación y obtención de proyectos](getting-and-creating-projects/README.md): 3 páginas canónicas.
- [Área de trabajo, índice y commits](basic-snapshotting/README.md): 8 páginas canónicas.
- [Ramas y fusiones](branching-and-merging/README.md): 12 páginas canónicas.
- [Aplicación y reorganización de cambios](patching/README.md): 5 páginas canónicas.
- [Búsqueda y depuración](debugging/README.md): 4 páginas canónicas.
- [Inspección y comparación](inspection-and-comparison/README.md): 12 páginas canónicas.
- [Repositorios remotos](sharing-and-updating-projects/README.md): 8 páginas canónicas.
- [Administración del repositorio](administration/README.md): 14 páginas canónicas.
- [Interfaces gráficas y web](graphical-tools/README.md): 5 páginas canónicas.
- [Parches por correo](email-and-patches/README.md): 4 páginas canónicas.
- [Integración con otros sistemas](external-systems/README.md): 9 páginas canónicas.
- [Plomería para modificar datos internos](plumbing-write/README.md): 18 páginas canónicas.
- [Plomería para consultar datos internos](plumbing-read/README.md): 23 páginas canónicas.
- [Servidor y transporte](server-and-transport/README.md): 11 páginas canónicas.
- [Automatización y comandos auxiliares](scripting-and-helpers/README.md): 19 páginas canónicas.
- [Guías conceptuales](guides/README.md): 21 páginas canónicas.
- [Formatos y protocolos](formats-and-protocols/README.md): 11 páginas canónicas.

## Convenciones del laboratorio

1. Los ejemplos que escriben estado usan un repositorio creado bajo `mktemp -d`.
2. Los commits de prueba definen nombre y correo solo en el repositorio.
3. `example.com` representa un dominio sin servicio de producción.
4. Las rutas, revisiones y URL se sustituyen después de identificar su tipo.
5. Las operaciones sobre referencias u objetos se prueban sobre datos sin valor antes de usarse en otro repositorio.

## Lectura por flujo

1. Empieza por [el mapa](overview/README.md).
2. Continúa con [creación de proyectos](getting-and-creating-projects/README.md) y [snapshots](basic-snapshotting/README.md).
3. Revisa [ramas](branching-and-merging/README.md), [comparación](inspection-and-comparison/README.md) y [remotos](sharing-and-updating-projects/README.md).
4. Usa [plomería de lectura](plumbing-read/README.md) antes de [plomería de escritura](plumbing-write/README.md).
5. Consulta [formatos y protocolos](formats-and-protocols/README.md) cuando implementes un productor, consumidor o analizador.

## Política de versión

La URL `source` de cada guía apunta a la referencia de Git. Antes de automatizar una opción, registra `git --version` y ejecuta la ayuda de esa instalación. Una guía explica contratos y verificaciones; la lista de opciones disponible depende de la versión instalada.
