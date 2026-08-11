# Guías conceptuales

Esta sección define reglas compartidas por comandos, archivos y flujos de trabajo. Lee patrones, archivos de control, revisiones o convenciones y puede escribir solo los archivos o configuraciones creados por el usuario.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | patrones, archivos de control, revisiones o convenciones. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | define reglas compartidas por comandos, archivos y flujos de trabajo. | Comprueba el resultado con una orden de lectura. |
| Persistencia | solo los archivos o configuraciones creados por el usuario | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa una consulta que muestre la regla efectiva y su origen. |

## Preparación

Crea un repositorio con dos commits y archivos bajo dos directorios. Cambia una regla por vez y registra el resultado.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`gitattributes`](gitattributes.md) | asignar atributos a rutas para diff, merge, exportación y filtros |
| [`gitcli`](gitcli.md) | interpretar opciones, revisiones y rutas en la línea de comandos |
| [`gitcore-tutorial`](gitcore-tutorial.md) | construir commits con objetos, árboles, el índice y referencias |
| [`gitcredentials`](gitcredentials.md) | configurar la obtención y el almacenamiento de credenciales |
| [`gitcvs-migration`](gitcvs-migration.md) | trasladar prácticas y datos de CVS a Git |
| [`gitdiffcore`](gitdiffcore.md) | entender las transformaciones que producen la salida de diff |
| [`giteveryday`](giteveryday.md) | resolver tareas diarias con un conjunto de comandos |
| [`gitfaq`](gitfaq.md) | resolver preguntas sobre configuración, historial y archivos |
| [`gitglossary`](gitglossary.md) | relacionar los términos usados por la documentación de Git |
| [`githooks`](githooks.md) | ejecutar programas en puntos definidos del flujo de Git |
| [`gitignore`](gitignore.md) | declarar patrones de archivos que Git debe dejar sin seguimiento |
| [`gitmailmap`](gitmailmap.md) | unificar nombres y correos que representan a una misma persona |
| [`gitmodules`](gitmodules.md) | declarar la ruta, URL y comportamiento de submódulos |
| [`gitnamespaces`](gitnamespaces.md) | aislar conjuntos de referencias dentro de un repositorio servidor |
| [`gitremote-helpers`](gitremote-helpers.md) | implementar transportes mediante procesos auxiliares |
| [`gitrepository-layout`](gitrepository-layout.md) | identificar los archivos y directorios internos de un repositorio |
| [`gitrevisions`](gitrevisions.md) | seleccionar commits y rangos mediante la sintaxis de revisiones |
| [`gitsubmodules`](gitsubmodules.md) | entender el modelo de repositorios anidados como submódulos |
| [`gittutorial-2`](gittutorial-2.md) | relacionar el índice, los objetos y las referencias detrás de los comandos |
| [`gittutorial`](gittutorial.md) | recorrer el ciclo de crear, registrar, inspeccionar y compartir cambios |
| [`gitworkflows`](gitworkflows.md) | organizar ramas, integración y publicación en un equipo |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La regla no se aplica | El patrón, alcance o precedencia no coincide | Consulta la regla efectiva y el archivo que la definió. |
| Una revisión se interpreta como ruta | El nombre es ambiguo | Separa revisiones y rutas con `--`. |
| El resultado cambia entre equipos | La regla vive en configuración no compartida | Decide qué parte debe versionarse en el repositorio. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
