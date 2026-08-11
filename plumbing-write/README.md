# Plomería para modificar datos internos

Esta sección crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Lee bytes, identificadores, árboles, índices y entradas estructuradas y puede escribir la base de objetos, el índice, packs o referencias.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | bytes, identificadores, árboles, índices y entradas estructuradas. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | crea objetos, índices, packs o referencias mediante contratos de bajo nivel. | Comprueba el resultado con una orden de lectura. |
| Persistencia | la base de objetos, el índice, packs o referencias | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git fsck`, `git cat-file`, `git ls-tree`, `git show-ref` y el hash devuelto. |

## Preparación

Usa un repositorio sin datos de valor. Guarda los hashes producidos y crea referencias solo con actualización condicional.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git checkout-index`](checkout-index.md) | copiar archivos del índice al área de trabajo |
| [`git commit-graph`](commit-graph.md) | escribir y verificar el archivo que acelera recorridos de commits |
| [`git commit-tree`](commit-tree.md) | crear un objeto commit a partir de un árbol y sus padres |
| [`git hash-object`](hash-object.md) | calcular el identificador de un objeto y guardarlo si se solicita |
| [`git index-pack`](index-pack.md) | crear un índice para un pack y comprobar sus objetos |
| [`git merge-file`](merge-file.md) | fusionar tres versiones de un archivo |
| [`git merge-index`](merge-index.md) | ejecutar un programa de fusión para entradas sin resolver |
| [`git mktag`](mktag.md) | validar y crear un objeto de etiqueta anotada |
| [`git mktree`](mktree.md) | crear un objeto árbol a partir de una lista de entradas |
| [`git multi-pack-index`](multi-pack-index.md) | administrar un índice que cubre varios archivos pack |
| [`git pack-objects`](pack-objects.md) | crear un archivo pack a partir de objetos |
| [`git prune-packed`](prune-packed.md) | eliminar objetos sueltos que ya existen dentro de packs |
| [`git read-tree`](read-tree.md) | cargar información de árboles en el índice |
| [`git symbolic-ref`](symbolic-ref.md) | leer o cambiar una referencia simbólica |
| [`git unpack-objects`](unpack-objects.md) | extraer objetos de un flujo pack |
| [`git update-index`](update-index.md) | modificar directamente entradas y bits del índice |
| [`git update-ref`](update-ref.md) | actualizar referencias con comprobaciones de valor anterior |
| [`git write-tree`](write-tree.md) | crear un objeto árbol a partir del índice |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El hash no coincide | Los bytes, el tipo o la longitud difieren | Compara la entrada byte por byte y no normalices el contenido. |
| La referencia no se actualiza | El valor anterior no coincide con la condición | Lee el valor actual y repite con una condición nueva. |
| El índice queda sin resolver | Una entrada tiene etapas de conflicto | Inspecciona `git ls-files --stage` antes de escribir un árbol. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
