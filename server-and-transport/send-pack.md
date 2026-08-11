---
title: "git send-pack"
source: "https://git-scm.com/docs/git-send-pack"
section: "server-and-transport"
status: "expanded"
---

# `git send-pack`

Este caso usa `git send-pack` para enviar objetos y actualizaciones de referencias al receptor. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Alcance y responsabilidad

git send-pack expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en enviar objetos y actualizaciones de referencias al receptor.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | la ruta del repositorio, el servicio y los parámetros de transporte. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | enviar objetos y actualizaciones de referencias al receptor. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: enviar objetos y actualizaciones de referencias al receptor. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa referencias anunciadas, logs del servicio, permisos y una transferencia desde un cliente de prueba. |

## Requisitos y laboratorio

Vincula el servicio a localhost y usa un repositorio bare sin datos de producción.

```bash
lab_dir="$(mktemp -d)"
git init "$lab_dir/proyecto"
git -C "$lab_dir/proyecto" config user.name "Persona de prueba"
git -C "$lab_dir/proyecto" config user.email "prueba@example.test"
printf 'línea base\n' > "$lab_dir/proyecto/archivo.txt"
git -C "$lab_dir/proyecto" add archivo.txt
git -C "$lab_dir/proyecto" commit -m "base"
cd "$lab_dir/proyecto"
```

Antes de ejecutar el ejemplo, confirma la raíz con `git rev-parse --show-toplevel` cuando exista un repositorio. Registra `git status --short` y las referencias que puedan cambiar.

## Modelo de funcionamiento

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

Para comprobar el resultado: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git send-pack https://example.test/equipo/biblioteca.git refs/heads/main
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: la ruta del repositorio, el servicio y los parámetros de transporte.
- La operación observable es: enviar objetos y actualizaciones de referencias al receptor.
- La comprobación se realiza mediante: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git send-pack [--mirror] [--dry-run] [--force]
		[--receive-pack=<git-receive-pack>]
		[--verbose] [--thin] [--atomic]
		[--[no-]signed | --signed=(true|false|if-asked)]
```

### Uso verificado con `git version 2.51.1`

```text
git send-pack [--mirror] [--dry-run] [--force]
                     [--receive-pack=<git-receive-pack>]
                     [--verbose] [--thin] [--atomic]
                     [--[no-]signed | --signed=(true|false|if-asked)]
                     [<host>:]<directory> (--all | <ref>...)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git send-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | enviar objetos y actualizaciones de referencias al receptor | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git send-pack a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Simulación | Calcular el efecto sin escribir el estado principal. | Compara la simulación con la selección prevista. |
| Validación | Comprobar el resultado de git send-pack con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--mirror` | Activa el modo `--mirror`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--dry-run` | Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio. |
| `--force` | Omite una protección concreta; úsala solo después de verificar el estado objetivo. |
| `--receive-pack` | Activa el modo `--receive-pack`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `--thin` | Activa el modo `--thin`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--atomic` | Exige que el conjunto se aplique completo o no se aplique. |
| `--signed` | Activa el modo `--signed`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--exec` | Activa el modo `--exec`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--remote` | Activa el modo `--remote`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--push-option` | Activa el modo `--push-option`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--stateless-rpc` | Activa el modo `--stateless-rpc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stdin` | Lee registros o nombres desde la entrada estándar. |
| `--helper-status` | Activa el modo `--helper-status`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--force-with-lease` | Omite una protección concreta de la orden; requiere verificar origen y destino. |
| `--force-if-includes` | Omite una protección concreta de la orden; requiere verificar origen y destino. |

## Selección de entradas

Resuelve por separado origen, destino y política de actualización. Una URL identifica un transporte; un refspec asigna referencias; un filtro limita objetos. Registra cada valor sin incluir credenciales.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El repositorio no se anuncia | La ruta, exportación o política no lo permite | Comprueba la raíz del servicio y los marcadores de exportación. |
| La negociación se corta | Cliente y servidor no acuerdan capacidad o protocolo | Registra trazas sin incluir credenciales y compara versiones. |
| La recepción se rechaza | Los permisos o hooks bloquean la referencia | Revisa la política del repositorio y el mensaje del hook. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: enviar objetos y actualizaciones de referencias al receptor. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git shell`](../server-and-transport/shell.md)
- [`git receive-pack`](../server-and-transport/receive-pack.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)

## Fuente

- [git-send-pack - Push objects over Git protocol to another repository](https://git-scm.com/docs/git-send-pack)
