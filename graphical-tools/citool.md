---
title: "git citool"
source: "https://git-scm.com/docs/git-citool"
section: "graphical-tools"
status: "expanded"
---

# `git citool`

Este caso usa `git citool` para preparar y crear commits desde una interfaz gráfica. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git citool presenta commits, cambios o acciones mediante una interfaz de escritorio o HTTP. Recibe como entrada el repositorio y la vista u operación elegida en la interfaz. La operación consiste en preparar y crear commits desde una interfaz gráfica.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el repositorio y la vista u operación elegida en la interfaz. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | preparar y crear commits desde una interfaz gráfica. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: preparar y crear commits desde una interfaz gráfica. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa la referencia seleccionada, el diff mostrado y `git status` después de una acción. |

## Requisitos y laboratorio

Usa un repositorio de prueba y un puerto local. No expongas la interfaz fuera de la máquina sin control de acceso.

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

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

Para comprobar el resultado: los comandos de consulta confirman el mismo estado que presenta la interfaz. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git citool
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el repositorio y la vista u operación elegida en la interfaz.
- La operación observable es: preparar y crear commits desde una interfaz gráfica.
- La comprobación se realiza mediante: los comandos de consulta confirman el mismo estado que presenta la interfaz.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git citool
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git citool -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | preparar y crear commits desde una interfaz gráfica | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git citool a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git citool con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |



## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La interfaz no inicia | Falta el entorno gráfico, un intérprete o un puerto | Comprueba dependencias y ejecuta desde el repositorio. |
| No aparecen cambios | La herramienta abrió otra ruta o referencia | Confirma la raíz y la referencia mostradas. |
| El servicio queda activo | El proceso web se ejecuta en segundo plano | Usa la orden de parada de la herramienta y verifica el puerto. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: preparar y crear commits desde una interfaz gráfica. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git gui`](../graphical-tools/gui.md)
- [`git instaweb`](../graphical-tools/instaweb.md)

## Fuente

- [git-citool - Graphical alternative to git-commit](https://git-scm.com/docs/git-citool)
