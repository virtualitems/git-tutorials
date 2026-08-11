# Administración del repositorio

Esta sección comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Lee objetos, referencias, reflogs, packs y configuración de mantenimiento y puede escribir packs, referencias auxiliares o datos inalcanzables según la operación.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | objetos, referencias, reflogs, packs y configuración de mantenimiento. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. | Comprueba el resultado con una orden de lectura. |
| Persistencia | packs, referencias auxiliares o datos inalcanzables según la operación | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git fsck`, `git count-objects -vH` y una lista de referencias antes y después. |

## Preparación

Clona o copia un repositorio de prueba. Registra referencias y tamaño antes de una operación que elimine datos.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git archive`](archive.md) | crear un archivo tar o zip a partir de un árbol de Git |
| [`git backfill`](backfill.md) | descargar en lotes los objetos que faltan en un clon parcial |
| [`git clean`](clean.md) | eliminar archivos que Git no sigue |
| [`git count-objects`](count-objects.md) | medir objetos sueltos, packs y espacio ocupado |
| [`git filter-branch`](filter-branch.md) | reescribir ramas mediante filtros sobre cada commit |
| [`git fsck`](fsck.md) | comprobar conectividad y validez de los objetos |
| [`git gc`](gc.md) | compactar el almacenamiento y retirar datos que ya pueden podarse |
| [`git maintenance`](maintenance.md) | ejecutar o programar tareas de mantenimiento del repositorio |
| [`git pack-refs`](pack-refs.md) | compactar referencias sueltas dentro del archivo packed-refs |
| [`git prune`](prune.md) | eliminar objetos sueltos que ningún objeto alcanzable necesita |
| [`git reflog`](reflog.md) | consultar y administrar el registro de cambios de referencias |
| [`git repack`](repack.md) | reorganizar objetos dentro de archivos pack |
| [`git replace`](replace.md) | sustituir un objeto por otro durante el recorrido del repositorio |
| [`scalar`](scalar.md) | administrar repositorios con funciones orientadas a conjuntos de archivos extensos |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Un objeto aparece como inalcanzable | Ninguna referencia o reflog lo conserva | Determina si debe recuperarse antes de podar. |
| El tamaño no disminuye | Los objetos siguen alcanzables o aún están protegidos por reflogs | Inspecciona alcanzabilidad y vencimientos. |
| La operación se interrumpe | Otro proceso mantiene un lock | Comprueba procesos activos antes de retirar un lock obsoleto. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
