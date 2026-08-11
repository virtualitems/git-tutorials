# Búsqueda y depuración

Esta sección localiza texto, autores, líneas o el commit que introdujo un comportamiento. Lee commits, blobs, rutas y patrones y puede escribir solo el estado de una sesión de depuración cuando la función lo requiere.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | commits, blobs, rutas y patrones. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | localiza texto, autores, líneas o el commit que introdujo un comportamiento. | Comprueba el resultado con una orden de lectura. |
| Persistencia | solo el estado de una sesión de depuración cuando la función lo requiere | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa la salida, el código de terminación y una revisión manual del commit hallado. |

## Preparación

Crea tres commits que cambien la misma línea. Usa un patrón que exista y otro que no exista para observar los códigos de salida.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git annotate`](annotate.md) | atribuir cada línea de un archivo a un commit |
| [`git bisect`](bisect.md) | localizar por búsqueda binaria el commit que introdujo un cambio |
| [`git blame`](blame.md) | mostrar el commit y autor asociados con cada línea de un archivo |
| [`git grep`](grep.md) | buscar texto en archivos del área de trabajo o de un árbol |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| No hay coincidencias | El patrón, la revisión o la ruta no abarca el dato | Prueba el patrón sobre `HEAD` y separa la ruta con `--`. |
| La atribución parece incorrecta | El archivo se movió o el bloque se reformateó | Activa detección de movimiento o copia y compara el commit. |
| La búsqueda binaria no avanza | La prueba no clasifica el commit | Marca el commit como `skip` o corrige el comando de prueba. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
