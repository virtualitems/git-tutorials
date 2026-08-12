# Guía técnica de Git en español

Índice de **194 guías canónicas**, organizadas en **19 secciones**. Cada tema tiene una sola página para que las correcciones y los ejemplos no diverjan entre rutas duplicadas.

Cada enlace abre una guía con sintaxis, ejemplos, casos de uso, opciones, diagnóstico, automatización, recuperación y su fuente oficial.

## Menú de secciones

- [Visión general](#overview) — 1 contenido
- [Configuración y entorno](#setup-and-config) — 6 contenidos
- [Creación y obtención de proyectos](#getting-and-creating-projects) — 3 contenidos
- [Snapshots básicos](#basic-snapshotting) — 8 contenidos
- [Ramas y fusiones](#branching-and-merging) — 12 contenidos
- [Aplicación y reorganización de cambios](#patching) — 5 contenidos
- [Búsqueda y depuración](#debugging) — 4 contenidos
- [Inspección y comparación](#inspection-and-comparison) — 12 contenidos
- [Repositorios remotos](#sharing-and-updating-projects) — 8 contenidos
- [Administración del repositorio](#administration) — 14 contenidos
- [Herramientas gráficas y web](#graphical-tools) — 5 contenidos
- [Correo y parches](#email-and-patches) — 4 contenidos
- [Integración con sistemas externos](#external-systems) — 9 contenidos
- [Plomería de lectura](#plumbing-read) — 23 contenidos
- [Plomería de escritura](#plumbing-write) — 18 contenidos
- [Servidor y transporte](#server-and-transport) — 11 contenidos
- [Automatización y comandos auxiliares](#scripting-and-helpers) — 19 contenidos
- [Guías conceptuales](#guides) — 21 contenidos
- [Formatos y protocolos](#formats-and-protocols) — 11 contenidos

---

<a id="overview"></a>
## Visión general

Mapa y punto de entrada de la referencia.

- [Referencia de Git](overview/reference-index.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="setup-and-config"></a>
## Configuración y entorno

Configuración, ayuda, versión y diagnóstico de Git.

- [git bugreport](setup-and-config/bugreport.md)
- [git config](setup-and-config/config.md)
- [git diagnose](setup-and-config/diagnose.md)
- [git](setup-and-config/git.md)
- [git help](setup-and-config/help.md)
- [git version](setup-and-config/version.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="getting-and-creating-projects"></a>
## Creación y obtención de proyectos

Inicialización, clonación y checkout disperso.

- [git clone](getting-and-creating-projects/clone.md)
- [git init](getting-and-creating-projects/init.md)
- [git sparse-checkout](getting-and-creating-projects/sparse-checkout.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="basic-snapshotting"></a>
## Snapshots básicos

Área de trabajo, índice y creación de commits.

- [git add](basic-snapshotting/add.md)
- [git commit](basic-snapshotting/commit.md)
- [git mv](basic-snapshotting/mv.md)
- [git notes](basic-snapshotting/notes.md)
- [git reset](basic-snapshotting/reset.md)
- [git restore](basic-snapshotting/restore.md)
- [git rm](basic-snapshotting/rm.md)
- [git status](basic-snapshotting/status.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="branching-and-merging"></a>
## Ramas y fusiones

Ramas, merges, etiquetas, stash, referencias y worktrees.

- [git branch](branching-and-merging/branch.md)
- [git checkout](branching-and-merging/checkout.md)
- [git history](branching-and-merging/history.md)
- [git merge-tree](branching-and-merging/merge-tree.md)
- [git merge](branching-and-merging/merge.md)
- [git mergetool](branching-and-merging/mergetool.md)
- [git refs](branching-and-merging/refs.md)
- [git rerere](branching-and-merging/rerere.md)
- [git stash](branching-and-merging/stash.md)
- [git switch](branching-and-merging/switch.md)
- [git tag](branching-and-merging/tag.md)
- [git worktree](branching-and-merging/worktree.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="patching"></a>
## Aplicación y reorganización de cambios

Parches, cherry-pick, rebase, replay y revert.

- [git apply](patching/apply.md)
- [git cherry-pick](patching/cherry-pick.md)
- [git rebase](patching/rebase.md)
- [git replay](patching/replay.md)
- [git revert](patching/revert.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="debugging"></a>
## Búsqueda y depuración

Búsqueda, autoría y localización de regresiones.

- [git annotate](debugging/annotate.md)
- [git bisect](debugging/bisect.md)
- [git blame](debugging/blame.md)
- [git grep](debugging/grep.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="inspection-and-comparison"></a>
## Inspección y comparación

Historial, diferencias, firmas y descripción de revisiones.

- [git describe](inspection-and-comparison/describe.md)
- [git diff](inspection-and-comparison/diff.md)
- [git difftool](inspection-and-comparison/difftool.md)
- [git last-modified](inspection-and-comparison/last-modified.md)
- [git log](inspection-and-comparison/log.md)
- [git range-diff](inspection-and-comparison/range-diff.md)
- [git shortlog](inspection-and-comparison/shortlog.md)
- [git show-branch](inspection-and-comparison/show-branch.md)
- [git show](inspection-and-comparison/show.md)
- [git verify-commit](inspection-and-comparison/verify-commit.md)
- [git verify-tag](inspection-and-comparison/verify-tag.md)
- [git whatchanged](inspection-and-comparison/whatchanged.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="sharing-and-updating-projects"></a>
## Repositorios remotos

Intercambio, sincronización y publicación de cambios.

- [git bundle](sharing-and-updating-projects/bundle.md)
- [git fetch](sharing-and-updating-projects/fetch.md)
- [git ls-remote](sharing-and-updating-projects/ls-remote.md)
- [git pull](sharing-and-updating-projects/pull.md)
- [git push](sharing-and-updating-projects/push.md)
- [git remote](sharing-and-updating-projects/remote.md)
- [git request-pull](sharing-and-updating-projects/request-pull.md)
- [git submodule](sharing-and-updating-projects/submodule.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="administration"></a>
## Administración del repositorio

Integridad, mantenimiento, limpieza y empaquetado.

- [git archive](administration/archive.md)
- [git backfill](administration/backfill.md)
- [git clean](administration/clean.md)
- [git count-objects](administration/count-objects.md)
- [git filter-branch](administration/filter-branch.md)
- [git fsck](administration/fsck.md)
- [git gc](administration/gc.md)
- [git maintenance](administration/maintenance.md)
- [git pack-refs](administration/pack-refs.md)
- [git prune](administration/prune.md)
- [git reflog](administration/reflog.md)
- [git repack](administration/repack.md)
- [git replace](administration/replace.md)
- [scalar](administration/scalar.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="graphical-tools"></a>
## Herramientas gráficas y web

Interfaces visuales y publicación web.

- [git citool](graphical-tools/citool.md)
- [gitk](graphical-tools/gitk.md)
- [gitweb](graphical-tools/gitweb.md)
- [git gui](graphical-tools/gui.md)
- [git instaweb](graphical-tools/instaweb.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="email-and-patches"></a>
## Correo y parches

Creación, envío y aplicación de series de parches.

- [git am](email-and-patches/am.md)
- [git format-patch](email-and-patches/format-patch.md)
- [git imap-send](email-and-patches/imap-send.md)
- [git send-email](email-and-patches/send-email.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="external-systems"></a>
## Integración con sistemas externos

Interoperabilidad con SVN, CVS, Perforce y otros sistemas.

- [git archimport](external-systems/archimport.md)
- [git cvsexportcommit](external-systems/cvsexportcommit.md)
- [git cvsimport](external-systems/cvsimport.md)
- [git cvsserver](external-systems/cvsserver.md)
- [git fast-export](external-systems/fast-export.md)
- [git fast-import](external-systems/fast-import.md)
- [git p4](external-systems/p4.md)
- [git quiltimport](external-systems/quiltimport.md)
- [git svn](external-systems/svn.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="plumbing-read"></a>
## Plomería de lectura

Consulta de objetos, índices, referencias y paquetes.

- [git cat-file](plumbing-read/cat-file.md)
- [git cherry](plumbing-read/cherry.md)
- [git diff-files](plumbing-read/diff-files.md)
- [git diff-index](plumbing-read/diff-index.md)
- [git diff-pairs](plumbing-read/diff-pairs.md)
- [git diff-tree](plumbing-read/diff-tree.md)
- [git for-each-ref](plumbing-read/for-each-ref.md)
- [git for-each-repo](plumbing-read/for-each-repo.md)
- [git format-rev](plumbing-read/format-rev.md)
- [git get-tar-commit-id](plumbing-read/get-tar-commit-id.md)
- [git ls-files](plumbing-read/ls-files.md)
- [git ls-tree](plumbing-read/ls-tree.md)
- [git merge-base](plumbing-read/merge-base.md)
- [git name-rev](plumbing-read/name-rev.md)
- [git pack-redundant](plumbing-read/pack-redundant.md)
- [git repo](plumbing-read/repo.md)
- [git rev-list](plumbing-read/rev-list.md)
- [git rev-parse](plumbing-read/rev-parse.md)
- [git show-index](plumbing-read/show-index.md)
- [git show-ref](plumbing-read/show-ref.md)
- [git unpack-file](plumbing-read/unpack-file.md)
- [git var](plumbing-read/var.md)
- [git verify-pack](plumbing-read/verify-pack.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="plumbing-write"></a>
## Plomería de escritura

Creación y modificación de objetos, índices y referencias.

- [git checkout-index](plumbing-write/checkout-index.md)
- [git commit-graph](plumbing-write/commit-graph.md)
- [git commit-tree](plumbing-write/commit-tree.md)
- [git hash-object](plumbing-write/hash-object.md)
- [git index-pack](plumbing-write/index-pack.md)
- [git merge-file](plumbing-write/merge-file.md)
- [git merge-index](plumbing-write/merge-index.md)
- [git mktag](plumbing-write/mktag.md)
- [git mktree](plumbing-write/mktree.md)
- [git multi-pack-index](plumbing-write/multi-pack-index.md)
- [git pack-objects](plumbing-write/pack-objects.md)
- [git prune-packed](plumbing-write/prune-packed.md)
- [git read-tree](plumbing-write/read-tree.md)
- [git symbolic-ref](plumbing-write/symbolic-ref.md)
- [git unpack-objects](plumbing-write/unpack-objects.md)
- [git update-index](plumbing-write/update-index.md)
- [git update-ref](plumbing-write/update-ref.md)
- [git write-tree](plumbing-write/write-tree.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="server-and-transport"></a>
## Servidor y transporte

Servicios, transporte HTTP y transferencia de datos.

- [git daemon](server-and-transport/daemon.md)
- [git fetch-pack](server-and-transport/fetch-pack.md)
- [git http-backend](server-and-transport/http-backend.md)
- [git http-fetch](server-and-transport/http-fetch.md)
- [git http-push](server-and-transport/http-push.md)
- [git receive-pack](server-and-transport/receive-pack.md)
- [git send-pack](server-and-transport/send-pack.md)
- [git shell](server-and-transport/shell.md)
- [git update-server-info](server-and-transport/update-server-info.md)
- [git upload-archive](server-and-transport/upload-archive.md)
- [git upload-pack](server-and-transport/upload-pack.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="scripting-and-helpers"></a>
## Automatización y comandos auxiliares

Credenciales, hooks, validadores y utilidades para scripts.

- [git check-attr](scripting-and-helpers/check-attr.md)
- [git check-ignore](scripting-and-helpers/check-ignore.md)
- [git check-mailmap](scripting-and-helpers/check-mailmap.md)
- [git check-ref-format](scripting-and-helpers/check-ref-format.md)
- [git column](scripting-and-helpers/column.md)
- [git credential-cache](scripting-and-helpers/credential-cache.md)
- [git credential-store](scripting-and-helpers/credential-store.md)
- [git credential](scripting-and-helpers/credential.md)
- [git fmt-merge-msg](scripting-and-helpers/fmt-merge-msg.md)
- [git hook](scripting-and-helpers/hook.md)
- [git interpret-trailers](scripting-and-helpers/interpret-trailers.md)
- [git mailinfo](scripting-and-helpers/mailinfo.md)
- [git mailsplit](scripting-and-helpers/mailsplit.md)
- [git merge-one-file](scripting-and-helpers/merge-one-file.md)
- [git patch-id](scripting-and-helpers/patch-id.md)
- [git sh-i18n](scripting-and-helpers/sh-i18n.md)
- [git sh-setup](scripting-and-helpers/sh-setup.md)
- [git stripspace](scripting-and-helpers/stripspace.md)
- [git url-parse](scripting-and-helpers/url-parse.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="guides"></a>
## Guías conceptuales

Tutoriales, modelos y flujos de trabajo transversales.

- [gitattributes](guides/gitattributes.md)
- [gitcli](guides/gitcli.md)
- [gitcore-tutorial](guides/gitcore-tutorial.md)
- [gitcredentials](guides/gitcredentials.md)
- [gitcvs-migration](guides/gitcvs-migration.md)
- [gitdiffcore](guides/gitdiffcore.md)
- [giteveryday](guides/giteveryday.md)
- [gitfaq](guides/gitfaq.md)
- [gitglossary](guides/gitglossary.md)
- [githooks](guides/githooks.md)
- [gitignore](guides/gitignore.md)
- [gitmailmap](guides/gitmailmap.md)
- [gitmodules](guides/gitmodules.md)
- [gitnamespaces](guides/gitnamespaces.md)
- [gitremote-helpers](guides/gitremote-helpers.md)
- [gitrepository-layout](guides/gitrepository-layout.md)
- [gitrevisions](guides/gitrevisions.md)
- [gitsubmodules](guides/gitsubmodules.md)
- [gittutorial-2](guides/gittutorial-2.md)
- [gittutorial](guides/gittutorial.md)
- [gitworkflows](guides/gitworkflows.md)

[↑ Volver al menú](#menú-de-secciones)

<a id="formats-and-protocols"></a>
## Formatos y protocolos

Formatos internos y protocolos de comunicación de Git.

- [gitformat-bundle](formats-and-protocols/gitformat-bundle.md)
- [gitformat-chunk](formats-and-protocols/gitformat-chunk.md)
- [gitformat-commit-graph](formats-and-protocols/gitformat-commit-graph.md)
- [gitformat-index](formats-and-protocols/gitformat-index.md)
- [gitformat-pack](formats-and-protocols/gitformat-pack.md)
- [gitformat-signature](formats-and-protocols/gitformat-signature.md)
- [gitprotocol-capabilities](formats-and-protocols/gitprotocol-capabilities.md)
- [gitprotocol-common](formats-and-protocols/gitprotocol-common.md)
- [gitprotocol-http](formats-and-protocols/gitprotocol-http.md)
- [gitprotocol-pack](formats-and-protocols/gitprotocol-pack.md)
- [gitprotocol-v2](formats-and-protocols/gitprotocol-v2.md)

[↑ Volver al menú](#menú-de-secciones)

---

## Alcance y convenciones

La referencia toma Git 2.55.0 como versión objetivo. Una instalación anterior puede carecer de opciones documentadas aquí. Comprueba la versión instalada con `git --version` y la sintaxis disponible con `git <comando> --help-all`.

Las [convenciones de la CLI](guides/gitcli.md) explican el orden de argumentos, la negación de opciones, los valores opcionales, el separador `--`, los pathspecs y los códigos de terminación. El [laboratorio base](getting-and-creating-projects/init.md#laboratorio-base) proporciona un repositorio desechable para ejecutar los ejemplos que modifican estado.

## Cambios de la revisión del 11 de agosto de 2026

- Se eliminaron 28 páginas alias de `email`, `plumbing-commands` y `server-admin`; el índice enlaza únicamente la ubicación canónica de cada tema.
- Se centralizaron las reglas compartidas de invocación y verificación en `guides/gitcli.md` para evitar que cada guía repita explicaciones divergentes.
- Se fijó Git 2.55.0 como versión documental y se contrastaron las opciones con la documentación oficial de esa versión.

## Licencia

Este proyecto se distribuye bajo la [Licencia MIT](LICENSE). La documentación oficial enlazada desde cada guía pertenece a sus respectivos titulares.
