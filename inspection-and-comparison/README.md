# Inspección y comparación

Esta sección selecciona objetos o rangos y produce una vista sin cambiar el repositorio. Lee revisiones, rangos, rutas y opciones de formato y puede escribir ningún estado salvo archivos de salida pedidos por el usuario.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | revisiones, rangos, rutas y opciones de formato. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | selecciona objetos o rangos y produce una vista sin cambiar el repositorio. | Comprueba el resultado con una orden de lectura. |
| Persistencia | ningún estado salvo archivos de salida pedidos por el usuario | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa el hash, el rango y el pathspec impresos junto al resultado. |

## Preparación

Crea dos commits y una rama. Compara cada par de estados con una ruta explícita y después sin limitar la ruta.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git describe`](describe.md) | nombrar un commit con la referencia cercana que lo alcanza |
| [`git diff`](diff.md) | comparar contenido entre el área de trabajo, el índice y commits |
| [`git difftool`](difftool.md) | ver comparaciones con una herramienta externa |
| [`git last-modified`](last-modified.md) | mostrar el commit que modificó por última vez cada ruta |
| [`git log`](log.md) | consultar commits con filtros y formatos de salida |
| [`git range-diff`](range-diff.md) | comparar dos versiones de una serie de commits |
| [`git shortlog`](shortlog.md) | agrupar el historial por autor y resumir sus commits |
| [`git show-branch`](show-branch.md) | comparar el desarrollo representado por varias ramas |
| [`git show`](show.md) | mostrar un objeto y la información asociada a su tipo |
| [`git verify-commit`](verify-commit.md) | verificar la firma criptográfica de commits |
| [`git verify-tag`](verify-tag.md) | verificar la firma criptográfica de etiquetas |
| [`git whatchanged`](whatchanged.md) | mostrar commits junto con diferencias en formato sin procesar |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La salida está vacía | El rango o el pathspec no contiene cambios | Resuelve cada revisión con `git rev-parse --verify`. |
| El orden no coincide con el esperado | La función usa un recorrido o criterio de orden | Declara el criterio con opciones de fecha, topología o formato. |
| Un script interpreta colores | La salida está destinada a terminal | Usa una forma de formato y desactiva color para datos de máquina. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
