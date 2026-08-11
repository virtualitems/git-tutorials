---
title: "git daemon"
source: "https://git-scm.com/docs/git-daemon"
section: "server-admin"
canonical_file: "server-and-transport/daemon.md"
status: "expanded"
---

# `git daemon`

> Esta ruta conserva la clasificación `server-admin`. La guía canónica está en [`server-and-transport/daemon.md`](../server-and-transport/daemon.md). Ambas documentan la misma URL del sitemap.

Este caso usa `git daemon` para servir repositorios mediante el protocolo git. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Alcance y responsabilidad

git daemon expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en servir repositorios mediante el protocolo git.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | la ruta del repositorio, el servicio y los parámetros de transporte. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | servir repositorios mediante el protocolo git. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura. | Compara el estado antes y después. |
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
git daemon --reuseaddr --base-path=/srv/git /srv/git
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: la ruta del repositorio, el servicio y los parámetros de transporte.
- La operación observable es: servir repositorios mediante el protocolo git.
- La comprobación se realiza mediante: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git daemon [--verbose] [--syslog] [--export-all]
	   [--timeout=<n>] [--init-timeout=<n>] [--max-connections=<n>]
	   [--strict-paths] [--base-path=<path>] [--base-path-relaxed]
	   [--user-path | --user-path=<path>]
```

### Uso verificado con `git version 2.51.1`

```text
git daemon [--verbose] [--syslog] [--export-all]
           [--timeout=<n>] [--init-timeout=<n>] [--max-connections=<n>]
           [--strict-paths] [--base-path=<path>] [--base-path-relaxed]
           [--user-path | --user-path=<path>]
           [--interpolated-path=<path>]
           [--reuseaddr] [--pid-file=<file>]
           [--(enable|disable|allow-override|forbid-override)=<service>]
           [--access-hook=<path>]
           [--inetd | [--listen=<host_or_ipaddr>] [--port=<n>]
                      [--detach] [--user=<user> [--group=<group>]]
           [--log-destination=(stderr|syslog|none)]
           [<directory>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git daemon -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | servir repositorios mediante el protocolo git | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git daemon a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git daemon con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `--syslog` | Activa el modo `--syslog`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--export-all` | Incluye elementos adicionales dentro del alcance indicado. |
| `--timeout` | Activa el modo `--timeout`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--init-timeout` | Activa el modo `--init-timeout`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--max-connections` | Establece un límite numérico para la selección o el recorrido. |
| `--strict-paths` | Activa el modo `--strict-paths`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--base-path` | Activa el modo `--base-path`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--base-path-relaxed` | Activa el modo `--base-path-relaxed`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--user-path` | Activa el modo `--user-path`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--interpolated-path` | Activa el modo `--interpolated-path`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reuseaddr` | Activa el modo `--reuseaddr`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--pid-file` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `--access-hook` | Activa el modo `--access-hook`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--inetd` | Activa el modo `--inetd`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--listen` | Activa el modo `--listen`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--port` | Activa el modo `--port`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--detach` | Hace que `HEAD` apunte directamente a un commit. |
| `--user` | Activa el modo `--user`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--group` | Activa el modo `--group`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--log-destination` | Activa el modo `--log-destination`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

Persistencia: Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git fetch-pack`](../server-and-transport/fetch-pack.md)
- [`git http-backend`](../server-and-transport/http-backend.md)

## Fuente

- [git-daemon - A really simple server for Git repositories](https://git-scm.com/docs/git-daemon)
