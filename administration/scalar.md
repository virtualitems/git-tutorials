---
title: "scalar"
source: "https://git-scm.com/docs/scalar"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `scalar`

Este caso usa `scalar` para administrar repositorios con funciones orientadas a conjuntos de archivos extensos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
scalar clone https://example.com/equipo/biblioteca.git biblioteca
scalar list
```

La invocación `scalar clone https://example.com/equipo/biblioteca.git biblioteca` ejecuta esta operación: administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
scalar clone [--single-branch] [--branch <main-branch>] [--full-clone]
	[--[no-]src] [--[no-]tags] [--[no-]maintenance] <url> [<enlistment>]
scalar list
scalar register [--[no-]maintenance] [<enlistment>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
scalar [-C <directory>] [-c <key>=<value>] <command> [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `scalar -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--single-branch`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
scalar --single-branch clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
scalar --branch clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--full-clone`

Activa full clone durante administrar repositorios con funciones orientadas a conjuntos de archivos extensos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
scalar --full-clone clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--src`

Activa src durante administrar repositorios con funciones orientadas a conjuntos de archivos extensos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
scalar --src clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
scalar --tags clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--maintenance`

Activa maintenance durante administrar repositorios con funciones orientadas a conjuntos de archivos extensos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
scalar --maintenance clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
scalar -C clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
scalar -c clone https://example.com/equipo/biblioteca.git biblioteca
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git replace`](../administration/replace.md)
- [`git repack`](../administration/repack.md)

## Fuente

- [scalar - A tool for managing large Git repositories](https://git-scm.com/docs/scalar)
