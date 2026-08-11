# Repositorios remotos

Esta sección anuncia, descarga o actualiza objetos y referencias entre repositorios. Lee refspecs, URL, configuración de remotos y objetos alcanzables y puede escribir referencias locales o remotas, objetos y configuración del remoto.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | refspecs, URL, configuración de remotos y objetos alcanzables. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | anuncia, descarga o actualiza objetos y referencias entre repositorios. | Comprueba el resultado con una orden de lectura. |
| Persistencia | referencias locales o remotas, objetos y configuración del remoto | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git remote -v`, `git branch -vv`, `git ls-remote` y el log de las referencias. |

## Preparación

Usa un repositorio bare local como remoto. Permite probar fetch, pull y push sin credenciales ni red.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git bundle`](bundle.md) | transportar objetos y referencias dentro de un solo archivo |
| [`git fetch`](fetch.md) | descargar objetos y referencias sin integrar la rama actual |
| [`git ls-remote`](ls-remote.md) | enumerar referencias anunciadas por un repositorio remoto |
| [`git pull`](pull.md) | descargar cambios e integrarlos en la rama actual |
| [`git push`](push.md) | actualizar referencias de un repositorio remoto y enviar sus objetos |
| [`git remote`](remote.md) | crear y administrar nombres para repositorios remotos |
| [`git request-pull`](request-pull.md) | generar un resumen para solicitar que otra persona integre cambios |
| [`git submodule`](submodule.md) | administrar repositorios incluidos dentro de otro repositorio |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El refspec no coincide | La parte de origen no resuelve una referencia | Comprueba la referencia local y escribe el refspec completo. |
| La actualización se rechaza | El destino perdería commits o una política lo impide | Integra primero o usa una protección con lease tras verificar el remoto. |
| La rama no tiene upstream | No existe asociación entre rama local y remota | Configura el upstream y confirma con `git branch -vv`. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
