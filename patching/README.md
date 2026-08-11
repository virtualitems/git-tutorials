# Aplicación y reorganización de cambios

Esta sección aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Lee parches, commits, rangos y opciones de estrategia y puede escribir el área de trabajo, el índice, commits y referencias.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | parches, commits, rangos y opciones de estrategia. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | aplica diffs o commits y mantiene un estado que puede continuar o abortarse. | Comprueba el resultado con una orden de lectura. |
| Persistencia | el área de trabajo, el índice, commits y referencias | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git diff --check` y `git log --oneline --decorate -n 10`. |

## Preparación

Trabaja sobre una rama de prueba y crea una etiqueta o rama de respaldo antes de aplicar una serie.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git apply`](apply.md) | aplicar un parche sobre archivos o sobre el índice |
| [`git cherry-pick`](cherry-pick.md) | aplicar en la rama actual el cambio de commits existentes |
| [`git rebase`](rebase.md) | reaplicar commits sobre una base distinta |
| [`git replay`](replay.md) | reproducir commits sobre una base y comunicar el cambio de referencias |
| [`git revert`](revert.md) | crear un commit que invierte el efecto de otro commit |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Un parche no aplica | El contexto no coincide con el contenido actual | Inspecciona los rechazos o resuelve el conflicto antes de continuar. |
| La secuencia queda en pausa | Git espera una resolución o una decisión | Consulta `git status` y usa `--continue`, `--skip` o `--abort`. |
| El resultado contiene commits vacíos | Los cambios ya existen o se resolvieron sin diferencias | Revisa el diff y aplica la política de commits vacíos de la orden. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
