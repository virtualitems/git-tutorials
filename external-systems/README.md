# Integración con otros sistemas

Esta sección traduce historial, referencias e identidades entre Git y otro sistema. Lee metadatos y cambios del sistema de origen y puede escribir commits, referencias o cambios en el sistema de destino.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | metadatos y cambios del sistema de origen. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | traduce historial, referencias e identidades entre Git y otro sistema. | Comprueba el resultado con una orden de lectura. |
| Persistencia | commits, referencias o cambios en el sistema de destino | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa conteo de revisiones, autores, marcas, ramas y una comparación de contenido. |

## Preparación

Usa una copia del origen y una rama de migración. Conserva un mapa de identidades y revisiones.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git archimport`](archimport.md) | importar un repositorio de GNU Arch |
| [`git cvsexportcommit`](cvsexportcommit.md) | aplicar un commit de Git sobre un checkout de CVS |
| [`git cvsimport`](cvsimport.md) | importar historial desde CVS |
| [`git cvsserver`](cvsserver.md) | permitir que clientes CVS accedan a un repositorio Git |
| [`git fast-export`](fast-export.md) | emitir historial y referencias en un flujo para migración |
| [`git fast-import`](fast-import.md) | crear historial y referencias a partir de un flujo de importación |
| [`git p4`](p4.md) | importar desde Perforce y enviar cambios de vuelta |
| [`git quiltimport`](quiltimport.md) | importar una serie de parches administrada por quilt |
| [`git svn`](svn.md) | usar un repositorio Subversion desde un repositorio Git |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Faltan revisiones | El rango, rama o marcador de importación las excluye | Compara conteos y el último identificador importado. |
| La identidad cambia | No existe una regla de mapeo estable | Define el mapa antes de repetir la importación. |
| La sincronización duplica cambios | Se perdió el marcador entre sistemas | Restaura el punto de control y prueba sobre una copia. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
