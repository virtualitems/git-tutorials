# Interfaces gráficas y web

Esta sección presenta commits, cambios o acciones mediante una interfaz de escritorio o HTTP. Lee el repositorio y la configuración de la herramienta y puede escribir solo las acciones confirmadas desde la interfaz o archivos de servicio.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el repositorio y la configuración de la herramienta. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | presenta commits, cambios o acciones mediante una interfaz de escritorio o HTTP. | Comprueba el resultado con una orden de lectura. |
| Persistencia | solo las acciones confirmadas desde la interfaz o archivos de servicio | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa la referencia seleccionada, el diff mostrado y `git status` después de una acción. |

## Preparación

Usa un repositorio de prueba y un puerto local. No expongas la interfaz fuera de la máquina sin control de acceso.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git citool`](citool.md) | preparar y crear commits desde una interfaz gráfica |
| [`gitk`](gitk.md) | explorar el historial y sus relaciones en una interfaz gráfica |
| [`gitweb`](gitweb.md) | publicar repositorios mediante una interfaz web |
| [`git gui`](gui.md) | usar una interfaz gráfica para preparar cambios y crear commits |
| [`git instaweb`](instaweb.md) | iniciar una instancia temporal de gitweb |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La interfaz no inicia | Falta el entorno gráfico, un intérprete o un puerto | Comprueba dependencias y ejecuta desde el repositorio. |
| No aparecen cambios | La herramienta abrió otra ruta o referencia | Confirma la raíz y la referencia mostradas. |
| El servicio queda activo | El proceso web se ejecuta en segundo plano | Usa la orden de parada de la herramienta y verifica el puerto. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
