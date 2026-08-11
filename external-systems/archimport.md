---
title: "git archimport"
source: "https://git-scm.com/docs/git-archimport"
section: "external-systems"
status: "expanded"
---

# `git archimport`

Este caso usa `git archimport` para importar un repositorio de GNU Arch. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git archimport traduce historial, referencias e identidades entre Git y otro sistema. Recibe como entrada la ubicación y los nombres que deben traducirse desde el sistema de origen. La operación consiste en importar un repositorio de GNU Arch.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | la ubicación y los nombres que deben traducirse desde el sistema de origen. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | importar un repositorio de GNU Arch. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: importar un repositorio de GNU Arch. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa conteo de revisiones, autores, marcas, ramas y una comparación de contenido. |

## Requisitos y laboratorio

Usa una copia del origen y una rama de migración. Conserva un mapa de identidades y revisiones.

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

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

Para comprobar el resultado: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git archimport archivo/linea:main
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- La operación observable es: importar un repositorio de GNU Arch.
- La comprobación se realiza mediante: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git archimport [-h] [-v] [-o] [-a] [-f] [-T] [-D <depth>] [-t <tempdir>]
	       <archive>/<branch>[:<git-branch>]…
```

### Uso verificado con `git version 2.51.1`

```text
git archimport     # fetch/update GIT from Arch
       [ -h ] [ -v ] [ -o ] [ -a ] [ -f ] [ -T ] [ -D depth ] [ -t tempdir ]
       repository/arch-branch [ repository/arch-branch] ...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git archimport -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | importar un repositorio de GNU Arch | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git archimport a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git archimport con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-h` | Muestra ayuda corta cuando la orden admite esta convención. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `-o` | Activa la forma corta de salida o una opción propia de la orden. |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `-f` | Activa la forma corta de la operación forzada. |
| `-T` | Activa el modo `-T`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-D` | Activa el modo `-D`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-t` | Activa el modo `-t`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Resuelve por separado origen, destino y política de actualización. Una URL identifica un transporte; un refspec asigna referencias; un filtro limita objetos. Registra cada valor sin incluir credenciales.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Faltan revisiones | El rango, rama o marcador de importación las excluye | Compara conteos y el último identificador importado. |
| La identidad cambia | No existe una regla de mapeo estable | Define el mapa antes de repetir la importación. |
| La sincronización duplica cambios | Se perdió el marcador entre sistemas | Restaura el punto de control y prueba sobre una copia. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: importar un repositorio de GNU Arch. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git cvsexportcommit`](../external-systems/cvsexportcommit.md)
- [`git cvsimport`](../external-systems/cvsimport.md)

## Fuente

- [git-archimport - Import a GNU Arch repository into Git](https://git-scm.com/docs/git-archimport)
