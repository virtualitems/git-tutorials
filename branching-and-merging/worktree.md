---
title: "git worktree"
source: "https://git-scm.com/docs/git-worktree"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git worktree`

Este caso usa `git worktree` para vincular varias áreas de trabajo al mismo repositorio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git worktree add ../biblioteca-release release
git worktree list
```

La invocación `git worktree add ../biblioteca-release release` ejecuta esta operación: vincular varias áreas de trabajo al mismo repositorio. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git worktree add [-f] [--detach] [--checkout] [--lock [--reason <string>]]
		 [--orphan] [(-b | -B) <new-branch>] <path> [<commit-ish>]
git worktree list [-v | --porcelain [-z]]
git worktree lock [--reason <string>] <worktree>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git worktree add [-f] [--detach] [--checkout] [--lock [--reason <string>]]
                        [--orphan] [(-b | -B) <new-branch>] <path> [<commit-ish>]
   or: git worktree list [-v | --porcelain [-z]]
   or: git worktree lock [--reason <string>] <worktree>
   or: git worktree move <worktree> <new-path>
   or: git worktree prune [-n] [-v] [--expire <expire>]
   or: git worktree remove [-f] <worktree>
   or: git worktree repair [<path>...]
   or: git worktree unlock <worktree>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git worktree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-f`

Activa f durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree -f add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach`

Hace que `HEAD` apunte directamente a un commit.

```bash
git worktree --detach add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--checkout`

Activa checkout durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree --checkout add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--lock`

Activa lock durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree --lock add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reason`

Activa reason durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree --reason add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--orphan`

Crea o cambia a una rama sin padres en el historial existente.

```bash
git worktree --orphan add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-b`

Activa b durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree -b add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-B`

Activa B durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree -B add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree -v add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

```bash
git worktree --porcelain add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git worktree -z add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Activa n durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git worktree -n add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire`

Aplica una fecha, duración o política de vencimiento.

```bash
git worktree --expire add ../biblioteca-release release
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force`

Omite protecciones distintas según el subcomando. `add` permite reutilizar una rama ya extraída o una ruta administrativa faltante; `move` permite destinos registrados pero ausentes; `remove` acepta un worktree con cambios. Un worktree bloqueado requiere dos usos de `--force` en los casos que indica el manual.

```bash
git worktree remove --force ../revision-temporal
git worktree list --porcelain
```

### `--checkout` y `--no-checkout`

`worktree add` extrae el commit de destino de forma predeterminada. `--no-checkout` crea los metadatos sin poblar el worktree, lo que permite configurar antes un sparse checkout.

```bash
git worktree add --no-checkout ../docs main
git -C ../docs sparse-checkout init --cone
git -C ../docs sparse-checkout set guides
git -C ../docs checkout
```

### `--guess-remote` y `--no-guess-remote`

Si `worktree add <ruta>` omite el commit y existe una sola rama remota cuyo nombre coincide con el nombre base de la ruta, `--guess-remote` crea una rama local que la sigue. La forma negativa desactiva esa búsqueda.

```bash
git worktree add --guess-remote ../tema
git -C ../tema branch --show-current
```

### `--relative-paths` y `--no-relative-paths`

Registran enlaces entre worktrees como rutas relativas o absolutas. La forma absoluta es la predeterminada; ambas sustituyen `worktree.useRelativePaths`. Con `repair`, también convierten los enlaces existentes.

```bash
git worktree repair --relative-paths
git worktree list --porcelain
```

### `--track` y `--no-track`

Al crear una rama con `worktree add`, `--track` configura el commit remoto como upstream. Esto ocurre de forma predeterminada si el punto inicial es una rama de seguimiento remoto. `--no-track` impide esa asociación.

```bash
git worktree add --track -b tema ../tema origin/main
git -C ../tema branch --verbose --verbose
```

### `--dry-run`, `--quiet` y `--verbose`

`prune --dry-run` enumera worktrees administrativos que retiraría. `add --quiet` suprime mensajes de progreso. `--verbose` muestra las eliminaciones de `prune` o información adicional de `list`.

```bash
git worktree prune --dry-run --verbose
git worktree list --verbose
```

## Páginas relacionadas

- [`git tag`](../branching-and-merging/tag.md)
- [`git switch`](../branching-and-merging/switch.md)

## Fuente

- [git-worktree - Manage multiple working trees](https://git-scm.com/docs/git-worktree)
