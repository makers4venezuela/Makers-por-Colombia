# Publicar con GitHub Desktop y GitHub Pages

Repo: **github.com/makers4venezuela/Makers-por-Colombia**

El archivo de bloqueo que daba el error *"A lock file already exists in the repository"* ya está borrado. GitHub Desktop debería funcionar normalmente.

## 1. Subir el código

En GitHub Desktop:

1. Verás los archivos en la lista de cambios
2. Mensaje de commit: `App de registro de donacion medica con marca KAFETIN`
3. **Commit to main**
4. **Push origin** (o **Publish repository** si es la primera vez — desmarca *Keep this code private*)

> El repositorio tiene que ser **público** para que GitHub Pages funcione gratis.

## 2. Activar GitHub Pages

En el navegador, dentro del repo:

1. **Settings** (pestaña de arriba)
2. **Pages**, en el menú de la izquierda
3. En *Source*, elige **Deploy from a branch**
4. Branch: **main** · Carpeta: **/ (root)**
5. **Save**

En uno o dos minutos la página queda en:

```
https://makers4venezuela.github.io/Makers-por-Colombia/
```

Esa es la dirección que le repartes a los voluntarios. En el celular: **Compartir → Añadir a pantalla de inicio**, y funciona como una app.

> Si prefieres una dirección más corta, en esa misma pantalla puedes conectar un dominio propio con **Custom domain**.

## 3. Prueba de humo

Abre el link en el celular y haz un registro real:

1. Regístrate como voluntario
2. Elige una férula del catálogo — **no debe pedirte foto**
3. Pon unidades y destino, guarda
4. Abre la hoja **Makers por Colombia**: la fila debe aparecer

Repite eligiendo *✏️ Otro modelo*: ahí **sí** pide foto, y en la columna `Foto` debe quedar un enlace de Drive.

Si la fila no llega, casi siempre es que el Apps Script no está re-implementado: **Implementar → Gestionar implementaciones → ✏️ → Versión: Nueva versión**.

## Para actualizar más adelante

Editas los archivos → en GitHub Desktop escribes el mensaje → **Commit to main** → **Push origin**. GitHub Pages republica solo en un minuto.

Si no ves el cambio, es la caché del navegador: recarga con `Ctrl+F5`.

---

## Qué hay en el repo

```
index.html                            la app completa (256 KB)
Codigo-AppsScript.gs                  el backend, para pegar en Apps Script
README.md
LICENSE                               MIT
.gitignore
.nojekyll                             evita que Pages procese el sitio con Jekyll
docs/DESPLIEGUE.md                    guía de puesta en marcha
docs/GITHUB.md                        este archivo
docs/catalogo-miniaturas.png          las 17 miniaturas
docs/Makers-por-Colombia-datos.xlsx   respaldo del esquema de datos
```

`.nojekyll` está vacío a propósito: su sola presencia le dice a GitHub Pages que publique los archivos tal cual, sin pasarlos por Jekyll. Sin él, Pages ignora cualquier archivo o carpeta que empiece por guion bajo.

## Qué queda fuera, a propósito

- `.claude/` y los archivos de bloqueo de LibreOffice
- **Cualquier CSV exportado desde la app.** Llevan nombres, correos y teléfonos de voluntarios reales, y el repositorio es público. No los subas nunca

## Dos advertencias

**La URL del Apps Script va dentro de `index.html`.** No es un secreto —cualquiera que use la app puede verla— pero al hacer el repo público queda a la vista. Quien la tenga puede escribir filas en tu hoja; no puede leer correos ni teléfonos. Si aparece basura, se corta generando una implementación nueva y actualizando `SHEET_URL`.

**El repo está dentro de OneDrive.** Funciona, pero OneDrive y Git a veces pelean sincronizando la carpeta `.git` y se corrompe el historial. Si empiezas a ver errores raros de Git, mueve el repo a algo como `C:\Users\sebas\GitHub\`.

## Sobre la licencia

**MIT**: cualquiera puede usar, copiar y modificar la app, incluso comercialmente, siempre que conserve el aviso de autoría, y nadie puede reclamarte nada si algo falla.

Cubre el código y las miniaturas, **no los `.stl`** de las férulas ni la marca KAFETIN: los modelos vienen de proyectos de terceros con sus propias condiciones, y el logo es tuyo, no software libre.
