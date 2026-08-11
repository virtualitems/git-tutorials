# Mapa de la referencia

Esta sección organiza las páginas por estado, tipo de entrada y efecto observable. Lee el inventario de comandos y guías y puede escribir ningún estado del repositorio.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el inventario de comandos y guías. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | organiza las páginas por estado, tipo de entrada y efecto observable. | Comprueba el resultado con una orden de lectura. |
| Persistencia | ningún estado del repositorio | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git help -a` y los enlaces del índice. |

## Preparación

No requiere un repositorio. Usa `git --version` y `git help -a` para comparar la instalación con el índice.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`Referencia de Git`](reference-index.md) | localizar comandos y guías dentro de la referencia de Git |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Una página no aparece | La versión instalada no contiene ese comando | Consulta `git --version` y la fuente enlazada. |
| Un nombre no se reconoce | Se confundió una orden con una guía o un formato | Comprueba si se invoca como `git <orden>` o se consulta como documento. |
| La ruta lleva a otra sección | Una función participa en más de un flujo | Usa la página canónica indicada por el índice. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
