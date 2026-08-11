# Ramas y fusiones

Esta sección consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Lee nombres de referencia, commits y bases de fusión y puede escribir referencias, `HEAD`, el índice y el área de trabajo según la operación.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | nombres de referencia, commits y bases de fusión. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | consulta o cambia referencias, `HEAD`, worktrees y estados de integración. | Comprueba el resultado con una orden de lectura. |
| Persistencia | referencias, `HEAD`, el índice y el área de trabajo según la operación | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git branch -vv`, `git log --graph --oneline --decorate --all`. |

## Preparación

Crea un commit base y dos ramas con un cambio distinto. Ejecuta la operación desde la rama indicada en el ejemplo.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git branch`](branch.md) | listar, crear, renombrar y eliminar ramas |
| [`git checkout`](checkout.md) | cambiar de rama o restaurar rutas desde otro estado |
| [`git history`](history.md) | reescribir commits con operaciones de corrección, mensaje o división |
| [`git merge-tree`](merge-tree.md) | calcular una fusión y exponer su resultado sin cambiar el índice |
| [`git merge`](merge.md) | integrar una o más líneas de desarrollo en la rama actual |
| [`git mergetool`](mergetool.md) | abrir una herramienta para resolver conflictos de fusión |
| [`git refs`](refs.md) | consultar y modificar referencias mediante transacciones |
| [`git rerere`](rerere.md) | recordar resoluciones de conflictos y reutilizarlas |
| [`git stash`](stash.md) | guardar cambios sin commit y recuperar un área de trabajo limpia |
| [`git switch`](switch.md) | cambiar de rama o crear una rama antes de cambiar |
| [`git tag`](tag.md) | crear, listar, verificar y eliminar etiquetas |
| [`git worktree`](worktree.md) | vincular varias áreas de trabajo al mismo repositorio |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La referencia es ambigua | Un nombre coincide con más de un objeto o una ruta | Usa `--` para separar rutas y una revisión completa para el objeto. |
| El cambio de rama se rechaza | Hay modificaciones que serían sobrescritas | Confirma el estado y decide entre commit, stash o descarte. |
| La integración se detiene | Dos cambios afectan la misma región o ruta | Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
