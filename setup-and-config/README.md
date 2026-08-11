# Configuración y entorno

Esta sección define cómo Git localiza configuración, ejecutables, repositorios y diagnósticos. Lee argumentos, variables de entorno y archivos de configuración y puede escribir configuración o artefactos de diagnóstico cuando la orden lo solicita.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | argumentos, variables de entorno y archivos de configuración. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | define cómo Git localiza configuración, ejecutables, repositorios y diagnósticos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | configuración o artefactos de diagnóstico cuando la orden lo solicita | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git config --show-origin --list`, `git version` o el archivo generado. |

## Preparación

Crea un repositorio de prueba y aplica cambios de configuración con `--local`. Así evitas modificar la configuración global.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git bugreport`](bugreport.md) | reunir información para informar un problema de Git |
| [`git config`](config.md) | leer y cambiar opciones de configuración por ámbito |
| [`git diagnose`](diagnose.md) | generar un archivo con datos de diagnóstico del repositorio |
| [`git`](git.md) | invocar Git, elegir el repositorio y aplicar opciones globales |
| [`git help`](help.md) | abrir la ayuda de un comando o concepto |
| [`git version`](version.md) | mostrar la versión de Git y datos del proceso de compilación |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El valor aplicado no coincide | Otra capa de configuración tiene precedencia | Ejecuta `git config --show-origin --get-all <clave>`. |
| Git no localiza el repositorio | `--git-dir`, `--work-tree` o el directorio actual apuntan a otra ruta | Ejecuta `git rev-parse --show-toplevel`. |
| La orden no existe | La versión instalada no incluye la función | Comprueba `git --version` y `git help -a`. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
