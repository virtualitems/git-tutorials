---
title: "git push"
source: "https://git-scm.com/docs/git-push"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git push`

Este caso usa `git push` para actualizar referencias de un repositorio remoto y enviar sus objetos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git push -u origin tema-portada
```

La invocación `git push -u origin tema-portada` ejecuta esta operación: actualizar referencias de un repositorio remoto y enviar sus objetos. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git push [--all | --branches | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	 [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-q | --quiet] [-v | --verbose]
	 [-u | --set-upstream] [-o <string> | --push-option=<string>]
	 [--[no-]signed | --signed=(true|false|if-asked)]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git push [<options>] [<repository> [<refspec>...]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git push -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git push --all -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branches`

Incluye o selecciona ramas según la operación.

```bash
git push --branches -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mirror`

Activa espejo durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mirror all refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git push --mirror -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
git push --tags -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--follow-tags`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git push --follow-tags -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--atomic`

Exige que el conjunto se aplique completo o no se aplique.

```bash
git push --atomic -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git push --dry-run -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--receive-pack`

Activa receive pack durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git push --receive-pack=valor -u origin tema-portada
git branch -vv
```

### `--repo`

Activa repo durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git push --repo=valor -u origin tema-portada
git branch -vv
```

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git push --force -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-d` y `--delete`

Elimina el elemento seleccionado.

#### Ejemplo con `--delete`

```bash
git push --delete -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--prune`

Retira entradas que ya no cumplen la condición documentada.

```bash
git push --prune -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git push --quiet -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git push --verbose -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-u` y `--set-upstream`

Configura la asociación upstream después de actualizar la referencia remota. En Git 2.51.1, la ayuda corta expresa el contrato como `set upstream for git pull/status`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--set-upstream`

```bash
git push --set-upstream origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-o` y `--push-option`

Activa push option durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--push-option`

```bash
git push --push-option=valor -u origin tema-portada
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `--signed`

Activa firmado durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign the push`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git push --signed=valor -u origin tema-portada
git branch -vv
```

### `--porcelain`

Produce un contrato de salida destinado a scripts.

```bash
git push --porcelain -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-with-lease`

Omite una protección concreta de la orden; requiere verificar origen y destino.

```bash
git push --force-with-lease=main -u origin tema-portada
git branch -vv
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-if-includes`

Omite una protección concreta de la orden; requiere verificar origen y destino.

```bash
git push --force-if-includes -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git push --recurse-submodules=valor -u origin tema-portada
git branch -vv
```

### `--thin`

Define thin para esta ejecución de `git push`. En Git 2.51.1, la ayuda corta expresa el contrato como `use thin pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git push --thin -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exec`

Activa exec durante actualizar referencias de un repositorio remoto y enviar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git push --exec=valor -u origin tema-portada
git branch -vv
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git push --progress -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

```bash
git push --no-verify -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

```bash
git push --verify -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-4` y `--ipv4`

Limita actualizar referencias de un repositorio remoto y enviar sus objetos al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv4`

```bash
git push --ipv4 -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-6` y `--ipv6`

Limita actualizar referencias de un repositorio remoto y enviar sus objetos al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv6`

```bash
git push --ipv6 -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--no-follow-tags`

Desactiva para esta invocación el comportamiento que habilita `--follow-tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-follow-tags -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-atomic`

Desactiva para esta invocación el comportamiento que habilita `--atomic`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-atomic -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-force -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signed`

Desactiva para esta invocación el comportamiento que habilita `--signed`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-signed -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-with-lease`

Desactiva para esta invocación el comportamiento que habilita `--force-with-lease`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-force-with-lease -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-if-includes`

Desactiva para esta invocación el comportamiento que habilita `--force-if-includes`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-force-if-includes -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-recurse-submodules -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-thin`

Desactiva para esta invocación el comportamiento que habilita `--thin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git push --no-thin -u origin tema-portada
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git remote`](../sharing-and-updating-projects/remote.md)
- [`git pull`](../sharing-and-updating-projects/pull.md)
- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)

## Fuente

- [git-push - Update remote refs along with associated objects](https://git-scm.com/docs/git-push)
