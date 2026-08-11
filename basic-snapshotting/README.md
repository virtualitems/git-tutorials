# Área de trabajo, índice y commits

Esta sección mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Lee rutas, pathspecs y contenido de `HEAD` o del índice y puede escribir el índice, el área de trabajo, commits o notas según la operación.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | rutas, pathspecs y contenido de `HEAD` o del índice. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. | Comprueba el resultado con una orden de lectura. |
| Persistencia | el índice, el área de trabajo, commits o notas según la operación | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status --short`, `git diff` y `git diff --cached`. |

## Preparación

Crea un repositorio con un commit base. Observa `HEAD`, el índice y el archivo antes y después de cada orden.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git add`](add.md) | copiar cambios del área de trabajo al índice |
| [`git commit`](commit.md) | registrar en el historial el contenido preparado en el índice |
| [`git mv`](mv.md) | mover o renombrar una ruta seguida por Git |
| [`git notes`](notes.md) | asociar anotaciones a objetos sin cambiar los objetos |
| [`git reset`](reset.md) | mover HEAD o restablecer el índice y, según el modo, el área de trabajo |
| [`git restore`](restore.md) | recuperar contenido de rutas en el índice o el área de trabajo |
| [`git rm`](rm.md) | retirar rutas del índice y, por defecto, del área de trabajo |
| [`git status`](status.md) | comparar el área de trabajo y el índice con el commit actual |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El cambio no entra al commit | El índice no contiene la versión esperada | Compara `git diff` con `git diff --cached`. |
| Un pathspec no coincide | La ruta se evalúa desde otro directorio o está ignorada | Usa `git status --short --untracked-files=all` y separa opciones con `--`. |
| Se reemplaza contenido local | La orden escribe el área de trabajo | Guarda el diff o crea un stash antes de repetir la operación. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
