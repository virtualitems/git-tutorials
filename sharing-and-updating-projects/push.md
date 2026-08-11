---
title: "git push"
source: "https://git-scm.com/docs/git-push"
section: "sharing-and-updating-projects"
status: "expanded"
---

# `git push`

Este caso usa `git push` para actualizar referencias de un repositorio remoto y enviar sus objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git push anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en actualizar referencias de un repositorio remoto y enviar sus objetos.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el repositorio, las referencias y el sentido de la transferencia. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | actualizar referencias de un repositorio remoto y enviar sus objetos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: actualizar referencias de un repositorio remoto y enviar sus objetos. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git push -u origin tema-portada
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el repositorio, las referencias y el sentido de la transferencia.
- La operación observable es: actualizar referencias de un repositorio remoto y enviar sus objetos.
- La comprobación se realiza mediante: las referencias locales y remotas permiten separar descarga, integración y publicación.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git push [--all | --branches | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	 [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-q | --quiet] [-v | --verbose]
	 [-u | --set-upstream] [-o <string> | --push-option=<string>]
	 [--[no-]signed | --signed=(true|false|if-asked)]
```

### Uso verificado con `git version 2.51.1`

```text
git push [<options>] [<repository> [<refspec>...]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git push -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | actualizar referencias de un repositorio remoto y enviar sus objetos | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git push a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Simulación | Calcular el efecto sin escribir el estado principal. | Compara la simulación con la selección prevista. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git push con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `--branches` | Incluye o selecciona ramas según la operación. |
| `--mirror` | Activa el modo `--mirror`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--tags` | Incluye o selecciona etiquetas según la operación. |
| `--follow-tags` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `--atomic` | Exige que el conjunto se aplique completo o no se aplique. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--dry-run` | Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio. |
| `--receive-pack` | Activa el modo `--receive-pack`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--repo` | Activa el modo `--repo`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--force` | Omite una protección concreta; úsala solo después de verificar el estado objetivo. |
| `-d` | Activa la forma corta de eliminación o una opción propia de la orden. |
| `--delete` | Elimina el elemento seleccionado. |
| `--prune` | Retira entradas que ya no cumplen la condición documentada. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--set-upstream` | Activa el modo `--set-upstream`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-o` | Activa la forma corta de salida o una opción propia de la orden. |
| `--push-option` | Activa el modo `--push-option`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--signed` | Activa el modo `--signed`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--porcelain` | Produce un contrato de salida destinado a scripts. |
| `--force-with-lease` | Omite una protección concreta de la orden; requiere verificar origen y destino. |
| `--force-if-includes` | Omite una protección concreta de la orden; requiere verificar origen y destino. |
| `--recurse-submodules` | Propaga la operación a submódulos dentro del alcance. |
| `--thin` | Activa el modo `--thin`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--exec` | Activa el modo `--exec`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--no-verify` | Desactiva el comportamiento `verify` para esta invocación. |
| `--verify` | Exige que el nombre o estructura cumpla el contrato antes de continuar. |
| `-4` | Activa el modo `-4`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ipv4` | Activa el modo `--ipv4`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-6` | Activa el modo `-6`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ipv6` | Activa el modo `--ipv6`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

Persistencia: Puede persistir el estado implicado por esta operación: actualizar referencias de un repositorio remoto y enviar sus objetos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git remote`](../sharing-and-updating-projects/remote.md)
- [`git pull`](../sharing-and-updating-projects/pull.md)
- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)

## Fuente

- [git-push - Update remote refs along with associated objects](https://git-scm.com/docs/git-push)
