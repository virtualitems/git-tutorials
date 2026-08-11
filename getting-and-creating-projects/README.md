# Creación y obtención de proyectos

Esta sección crea la base de datos local de objetos y prepara el área de trabajo. Lee una ruta local, una URL o reglas de selección y puede escribir `.git`, referencias, objetos y archivos del área de trabajo.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | una ruta local, una URL o reglas de selección. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | crea la base de datos local de objetos y prepara el área de trabajo. | Comprueba el resultado con una orden de lectura. |
| Persistencia | `.git`, referencias, objetos y archivos del área de trabajo | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git remote -v` y `git rev-parse --show-toplevel`. |

## Preparación

Usa dos directorios bajo una ruta creada con `mktemp -d`: uno como origen y otro como destino.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git clone`](clone.md) | crear un repositorio local a partir de otro repositorio |
| [`git init`](init.md) | crear un repositorio vacío o reinicializar uno existente |
| [`git sparse-checkout`](sparse-checkout.md) | materializar solo una parte de los archivos seguidos |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El destino ya contiene archivos | La creación o clonación requiere una ruta compatible | Elige un directorio vacío o inicializa la ruta de forma explícita. |
| No se recibe una referencia | El remoto no la anuncia o el filtro la excluye | Ejecuta `git ls-remote <url>` y revisa los filtros. |
| Falla la autenticación | La URL o el helper de credenciales no entrega acceso | Comprueba la URL sin registrar credenciales en el historial del shell. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
