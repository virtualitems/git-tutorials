---
title: "git submodule"
source: "https://git-scm.com/docs/git-submodule"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git submodule`

Este caso usa `git submodule` para administrar repositorios incluidos dentro de otro repositorio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git submodule add https://example.com/equipo/tema.git temas/base
git submodule update --init --recursive
```

La invocación `git submodule add https://example.com/equipo/tema.git temas/base` ejecuta esta operación: administrar repositorios incluidos dentro de otro repositorio. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git submodule [--quiet] [--cached]
git submodule [--quiet] add [<options>] [--] <repository> [<path>]
git submodule [--quiet] status [--cached] [--recursive] [--] [<path>…]
git submodule [--quiet] init [--] [<path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git submodule [--quiet] [--cached]
   or: git submodule [--quiet] add [-b <branch>] [-f|--force] [--name <name>] [--reference <repository>] [--] <repository> [<path>]
   or: git submodule [--quiet] status [--cached] [--recursive] [--] [<path>...]
   or: git submodule [--quiet] init [--] [<path>...]
   or: git submodule [--quiet] deinit [-f|--force] (--all| [--] <path>...)
   or: git submodule [--quiet] update [--init [--filter=<filter-spec>]] [--remote] [-N|--no-fetch] [-f|--force] [--checkout|--merge|--rebase] [--[no-]recommend-shallow] [--reference <repository>] [--recursive] [--[no-]single-branch] [--] [<path>...]
   or: git submodule [--quiet] set-branch (--default|--branch <branch>) [--] <path>
   or: git submodule [--quiet] set-url [--] <path> <newurl>
   or: git submodule [--quiet] summary [--cached|--files] [--summary-limit <n>] [commit] [--] [<path>...]
   or: git submodule [--quiet] foreach [--recursive] <command>
   or: git submodule [--quiet] sync [--recursive] [--] [<path>...]
   or: git submodule [--quiet] absorbgitdirs [--] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git submodule -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git submodule --quiet add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

```bash
git submodule --cached add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recursive`

Extiende la operación de forma recursiva al ámbito documentado.

```bash
git submodule --recursive add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-b`

Activa b durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule -b add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Activa f durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule -f add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

```bash
git submodule --force add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name`

Activa nombre durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --name add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reference`

Activa reference durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --reference add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git submodule --all add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--init`

Activa init durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --init add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial.

```bash
git submodule --filter add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remote`

Activa remote durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --remote add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-N`

Activa N durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule -N add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fetch`

Desactiva el comportamiento `fetch` para esta invocación.

```bash
git submodule --no-fetch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--checkout`

Activa checkout durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --checkout add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merge`

Activa merge durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --merge add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rebase`

Activa rebase durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --rebase add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recommend-shallow`

Activa recommend historial shallow durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --recommend-shallow add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--single-branch`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git submodule --single-branch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--default`

Activa default durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git submodule --default add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git submodule --branch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--files`

Activa files durante administrar repositorios incluidos dentro de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git submodule` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git submodule --files add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--summary-limit`

Establece un límite numérico para la selección o el recorrido.

```bash
git submodule --summary-limit add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recommend-shallow`

Desactiva para esta invocación el comportamiento que habilita `--recommend-shallow`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git submodule --no-recommend-shallow add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-single-branch`

Desactiva para esta invocación el comportamiento que habilita `--single-branch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git submodule --no-single-branch add https://example.com/equipo/tema.git temas/base
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Fuerza los mensajes de progreso en stderr aunque ese canal no esté conectado a una terminal. Solo se acepta con `submodule add` y `submodule update`.

```bash
git submodule update --init --progress
```

### `--dissociate`

Después de clonar mediante un repositorio de referencia, copia los objetos prestados para que el submódulo deje de depender de ese repositorio. Solo se acepta con `add` y `update` y se transmite al `git clone` interno.

```bash
git submodule update --init \
  --reference ../cache-objetos --dissociate
```

### `--depth`

Con `add` o `update`, crea los clones nuevos con la historia limitada al número de revisiones indicado.

```bash
git submodule update --init --depth=1
git -C ruta/del/submodulo rev-list --count HEAD
```

### `--jobs` y `-j`

Con `update`, clona submódulos nuevos en paralelo con la cantidad de trabajos indicada. Si se omite, Git consulta `submodule.fetchJobs`.

```bash
git submodule update --init --recursive --jobs=4
git submodule status --recursive
```

## Páginas relacionadas

- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)

## Fuente

- [git-submodule - Initialize, update or inspect submodules](https://git-scm.com/docs/git-submodule)
