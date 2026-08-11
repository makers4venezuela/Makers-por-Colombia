# Publicar la app

La app se publica en:

```
https://kafetin.co/makersporcolombia/
```

## Por qué desde `kafetin-web` y no desde este repo

`kafetin.co` es un dominio propio puesto sobre el repo de proyecto **`makers4venezuela/kafetin-web`** (tiene el archivo `CNAME`). En GitHub Pages, un dominio propio aplicado a un repo de proyecto **no se hereda** a los demás repos de la cuenta: `kafetin.co/loquesea` se busca dentro de `kafetin-web`, no en otro repositorio.

Por eso la app vive como una carpeta dentro de ese sitio:

```
kafetin-web/
├── index.html                  kafetin.co
├── kafetin-makers.html         kafetin.co/kafetin-makers.html
├── CNAME                       kafetin.co
└── makersporcolombia/
    ├── index.html              kafetin.co/makersporcolombia/   ← la app
    └── Codigo-AppsScript.gs
```

Sin transferir repos, sin renombrar, sin tocar DNS.

## Publicar un cambio

En GitHub Desktop, cambia al repo **kafetin-web**:

1. Verás la carpeta `makersporcolombia/` en la lista de cambios
2. Mensaje: `App Makers por Colombia`
3. **Commit to main** → **Push origin**

GitHub Pages republica en un minuto. Si no ves el cambio, es caché del navegador: `Ctrl+F5`.

## Los dos repositorios

| Repo | Para qué |
|---|---|
| `kafetin-web` | Lo **publicado**. Aquí vive la copia que sirve kafetin.co |
| `Makers-por-Colombia` | El **proyecto**: documentación, respaldo del esquema de datos, miniaturas del catálogo |

> Cuidado con la deriva: si editas `index.html` en un repo y no en el otro, quedan versiones distintas. Lo práctico es tratar `kafetin-web/makersporcolombia/index.html` como el archivo bueno y copiarlo al otro repo solo cuando quieras dejar constancia de una versión.

## Prueba de humo

Abre <https://kafetin.co/makersporcolombia/> en el celular:

1. Regístrate como voluntario
2. Elige una férula del catálogo — **no debe pedirte foto**
3. Pon unidades y destino, guarda
4. Abre la hoja **Makers por Colombia**: la fila debe aparecer

Repite con *✏️ Otro modelo*: ahí **sí** pide foto, y en la columna `Foto` debe quedar un enlace de Drive.

Si la fila no llega, casi siempre falta re-implementar el Apps Script: **Implementar → Gestionar implementaciones → ✏️ → Versión: Nueva versión**.

## Repartir el link

En el celular: **Compartir → Añadir a pantalla de inicio**. Queda como una app, con su ícono, y no hay que buscar el mensaje cada vez.

Si quieres, se le puede añadir un botón desde el sitio de Kafetin — en la sección *Zona Maker* de `index.html`, junto al enlace a `kafetin-makers.html`.

## Dos advertencias

**La URL del Apps Script va dentro de `index.html`.** No es un secreto —cualquiera que use la app puede verla— pero el repo es público. Quien la tenga puede escribir filas en tu hoja; no puede leer correos ni teléfonos. Si aparece basura, se corta generando una implementación nueva y actualizando `SHEET_URL`.

**Los repos están dentro de OneDrive.** Funciona, pero OneDrive y Git a veces pelean sincronizando `.git` y se corrompe el historial. Si ves errores raros de Git, mueve las carpetas a algo como `C:\Users\sebas\GitHub\`.

## Sobre la licencia

**MIT**: cualquiera puede usar, copiar y modificar la app, incluso comercialmente, conservando el aviso de autoría, y nadie puede reclamarte nada si algo falla.

Cubre el código y las miniaturas, **no los `.stl`** de las férulas ni la marca KAFETIN: los modelos vienen de proyectos de terceros con sus propias condiciones, y el logo es tuyo, no software libre.
