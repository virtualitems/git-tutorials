---
title: "git remote"
source: "https://git-scm.com/docs/git-remote"
section: "sharing-and-updating-projects"
status: "expanded"
---

# `git remote`

Este caso usa `git remote` para crear y administrar nombres para repositorios remotos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git remote anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en crear y administrar nombres para repositorios remotos.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el repositorio, las referencias y el sentido de la transferencia. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | crear y administrar nombres para repositorios remotos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: crear y administrar nombres para repositorios remotos. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git remote -v`, `git branch -vv`, `git ls-remote` y el log de las referencias. |

## Requisitos y laboratorio

Usa un repositorio bare local como remoto. Permite probar fetch, pull y push sin credenciales ni red.

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

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

Para comprobar el resultado: las referencias locales y remotas permiten separar descarga, integración y publicación. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git remote add origin https://example.test/equipo/biblioteca.git
git remote -v
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el repositorio, las referencias y el sentido de la transferencia.
- La operación observable es: crear y administrar nombres para repositorios remotos.
- La comprobación se realiza mediante: las referencias locales y remotas permiten separar descarga, integración y publicación.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git remote [-v | --verbose]
git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=(fetch|push)] <name> <URL>
git remote rename [--[no-]progress] <old> <new>
git remote remove <name>
```

### Uso verificado con `git version 2.51.1`

```text
git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename [--[no-]progress] <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git remote -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | crear y administrar nombres para repositorios remotos | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git remote a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Simulación | Calcular el efecto sin escribir el estado principal. | Compara la simulación con la selección prevista. |
| Validación | Comprobar el resultado de git remote con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `-t` | Activa el modo `-t`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--tags` | Incluye o selecciona etiquetas según la operación. |
| `--mirror` | Activa el modo `--mirror`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--no-tags` | Desactiva el comportamiento `tags` para esta invocación. |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `--auto` | Activa el modo `--auto`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-d` | Activa la forma corta de eliminación o una opción propia de la orden. |
| `--delete` | Elimina el elemento seleccionado. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--dry-run` | Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--prune` | Retira entradas que ya no cumplen la condición documentada. |
| `--add` | Permite crear o escribir el elemento seleccionado. |
| `--push` | Activa el modo `--push`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |

## Selección de entradas

Resuelve por separado origen, destino y política de actualización. Una URL identifica un transporte; un refspec asigna referencias; un filtro limita objetos. Registra cada valor sin incluir credenciales.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El refspec no coincide | La parte de origen no resuelve una referencia | Comprueba la referencia local y escribe el refspec completo. |
| La actualización se rechaza | El destino perdería commits o una política lo impide | Integra primero o usa una protección con lease tras verificar el remoto. |
| La rama no tiene upstream | No existe asociación entre rama local y remota | Configura el upstream y confirma con `git branch -vv`. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear y administrar nombres para repositorios remotos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)
- [`git push`](../sharing-and-updating-projects/push.md)
- [`git submodule`](../sharing-and-updating-projects/submodule.md)

## Fuente

- [git-remote - Manage set of tracked repositories](https://git-scm.com/docs/git-remote)
