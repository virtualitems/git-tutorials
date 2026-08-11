# Plomería para consultar datos internos

Esta sección consulta objetos, referencias, índices, packs y relaciones entre commits. Lee identificadores, revisiones, formatos y filtros y puede escribir ningún dato persistente salvo archivos solicitados de forma explícita.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | identificadores, revisiones, formatos y filtros. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | consulta objetos, referencias, índices, packs y relaciones entre commits. | Comprueba el resultado con una orden de lectura. |
| Persistencia | ningún dato persistente salvo archivos solicitados de forma explícita | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa tipo, tamaño, hash, referencia o etapa impresos por una segunda consulta. |

## Preparación

Crea un commit base, conserva sus hashes con `git rev-parse` y consulta cada objeto por tipo y contenido.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git cat-file`](cat-file.md) | consultar el tipo, tamaño o contenido de objetos |
| [`git cherry`](cherry.md) | detectar commits cuyo parche todavía no aparece en una rama base |
| [`git diff-files`](diff-files.md) | comparar el área de trabajo con el índice |
| [`git diff-index`](diff-index.md) | comparar un árbol con el índice o el área de trabajo |
| [`git diff-pairs`](diff-pairs.md) | comparar pares de blobs recibidos por la entrada estándar |
| [`git diff-tree`](diff-tree.md) | comparar los blobs y modos de dos árboles |
| [`git for-each-ref`](for-each-ref.md) | filtrar, ordenar y formatear referencias |
| [`git for-each-repo`](for-each-repo.md) | ejecutar un comando Git en repositorios enumerados por configuración |
| [`git format-rev`](format-rev.md) | formatear revisiones recibidas por la entrada estándar |
| [`git get-tar-commit-id`](get-tar-commit-id.md) | extraer el identificador incluido por git archive en un tar |
| [`git ls-files`](ls-files.md) | enumerar entradas del índice y su relación con el área de trabajo |
| [`git ls-tree`](ls-tree.md) | enumerar el contenido de un objeto árbol |
| [`git merge-base`](merge-base.md) | calcular ancestros comunes para una fusión |
| [`git name-rev`](name-rev.md) | expresar identificadores mediante nombres relativos a referencias |
| [`git pack-redundant`](pack-redundant.md) | detectar packs cuyo contenido ya está cubierto por otros packs |
| [`git repo`](repo.md) | consultar propiedades y estructura del repositorio |
| [`git rev-list`](rev-list.md) | enumerar commits alcanzables según límites y filtros |
| [`git rev-parse`](rev-parse.md) | resolver revisiones y separar opciones para scripts |
| [`git show-index`](show-index.md) | leer la tabla de objetos de un índice de pack |
| [`git show-ref`](show-ref.md) | enumerar o comprobar referencias del repositorio local |
| [`git unpack-file`](unpack-file.md) | crear un archivo temporal con el contenido de un blob |
| [`git var`](var.md) | mostrar variables lógicas calculadas por Git |
| [`git verify-pack`](verify-pack.md) | comprobar un pack mediante su archivo de índice |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El objeto no existe | El identificador no resuelve o no está disponible en un clon parcial | Valida el hash y la política de descarga. |
| La salida se separa mal | Un nombre contiene espacios o saltos de línea | Usa terminación NUL cuando la función la admita. |
| El recorrido incluye más commits | El rango expresa alcanzabilidad y no una lista literal | Comprueba extremos positivos y negativos del rango. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
