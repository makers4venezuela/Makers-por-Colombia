# Makers por Colombia — puesta en marcha

Todo vive en la nube. El voluntario solo abre un link: **no configura nada**.

```
App (Netlify)  ──POST──▶  Apps Script  ──▶  Sheet «Makers por Colombia»
                                        └─▶  Drive «Makers por Colombia - Fotos»
       ▲                                          │
       └──────────── JSONP (totales) ─────────────┘
```

Hay un solo paso manual, y es de una sola vez: **la URL del Apps Script no existe hasta que lo implementas**, así que hay que pegarla en la app después.

---

## 1. Backend: el Apps Script

1. Abre la hoja [**Makers por Colombia**](https://docs.google.com/spreadsheets/d/1bl2fDagcAf5IuiMqRDGWEjuqiwXOEQaDq2nGLeSHdQk/edit)
2. **Extensiones → Apps Script**. Borra lo que haya
3. Pega el código: está en la app, botón **⚙️ → Para la coordinación → Copiar código**
4. Arriba, en el selector de funciones, elige **`setup`** y pulsa **Ejecutar**
5. Acepta los permisos (Google avisará que la app "no está verificada" — es tuya: *Configuración avanzada → Ir a…*)

`setup` deja todo listo solo:

- Renombra la pestaña a **Registro** y escribe las 16 columnas con formato
- Crea la pestaña **Resumen** con los KPIs y el desglose por categoría y por modelo, todo con fórmulas
- Crea la carpeta de Drive **Makers por Colombia - Fotos**

## 2. Publicar el Apps Script

**Implementar → Nueva implementación → Aplicación web**

| Campo | Valor |
|---|---|
| Ejecutar como | **Yo** |
| Quién tiene acceso | **Cualquier persona** |

Copia la URL. Termina en `/exec`.

> «Cualquier persona» suena fuerte, pero es necesario: los voluntarios no inician sesión en Google. El script solo acepta escribir filas y devolver totales — y el `doGet` **no expone correo ni teléfono**.

## 3. Conectar la app — ✅ ya hecho

La URL ya está puesta en `index.html`:

```js
var SHEET_URL = "https://script.google.com/macros/s/AKfycbzCt5O_…/exec";
```

Solo hay que volver a tocarla si algún día creas una **implementación nueva** en vez de actualizar la existente, porque eso genera otra URL.

## 4. Publicar la app

Arrastra la carpeta a [app.netlify.com/drop](https://app.netlify.com/drop) y ponle nombre en *Site configuration → Change site name*.

Si conectaste el repo de GitHub (ver [`GITHUB.md`](GITHUB.md)), basta con hacer `git push`.

## 5. Repartir

Manda el link a los voluntarios. En el celular: **Compartir → Añadir a pantalla de inicio**.

---

## Cada vez que cambies el Apps Script

Hay que **volver a implementar** para que los cambios salgan al aire:

**Implementar → Gestionar implementaciones → ✏️ → Versión: Nueva versión → Implementar**

La URL `/exec` no cambia, así que no hay que tocar la app.

---

## Las 16 columnas de «Registro»

| # | Columna | Contenido |
|---|---|---|
| A | Fecha | `AAAA-MM-DD` |
| B | Voluntario | Nombre y apellido |
| C | Correo | **Dato personal** |
| D | Telefono | **Dato personal**, opcional |
| E | Taller | Taller o makerspace |
| F | Ciudad | |
| G | Pais | |
| H | Categoria | Dedos · Mano y metacarpo · Muñeca · Antebrazo y codo · Pie · Otro |
| I | Modelo | Nombre del catálogo |
| J | Archivo | El `.stl` real. Vacío si escribieron «Otro modelo» |
| K | Variante | Material, lateralidad, talla |
| L | Fabricadas | Unidades de **este lote**. Entero |
| M | Destino | A dónde va el lote: ciudad, departamento o institución |
| N | Notas | |
| O | Consentimiento | Sello ISO de la autorización (Ley 1581 de 2012) |
| P | Foto | Enlace de Drive. **Solo** la traen los modelos creados desde la app |

No cambies el orden: el script escribe y lee **por posición**.

---

## Destino en vez de «entregadas»

Cada registro es **un lote con un destino**: «fabriqué 20 unidades para Armenia». Si el mismo taller hace después 100 para el Chocó, son dos registros del mismo modelo.

El destino se escribe libre, pero la app sugiere los ya usados en toda la red y, al guardar, adopta la grafía existente. Así `armenia, quindio` y `Armenia, Quindío` terminan siendo el mismo destino en el panel.

El panel tiene un ranking **Por destino** con unidades, modelos y talleres involucrados. En el Sheet, la pestaña `Resumen` lo resuelve con un `QUERY` sobre `Registro!L2:M`, así que la lista de destinos crece sola sin tocar fórmulas.

> Se perdió el seguimiento de «fabricado pero aún no despachado». Fue una decisión deliberada: el registro refleja cómo trabajan los talleres, por lotes con un destino, en vez de pedir un número que nadie iba a mantener al día.

---

## Fotos

**Solo se piden al crear un modelo nuevo.** Si el voluntario elige una férula del catálogo —oficial o de la comunidad— la app no pide foto: ese modelo ya tiene su imagen. La foto es lo que hace que un modelo nuevo sea reconocible para los demás, no un comprobante de cada lote.

Se comprimen en el teléfono a 640 px JPEG antes de salir, así que pesan ~60–120 KB. El script las guarda en Drive con enlace de solo lectura y deja la URL en la columna P.

Van de **3 registros por envío**: con mala señal, un cuerpo con diez fotos se cae entero y se pierde el lote completo. En tandas de tres, lo que llega, llega.

Consumen tu cuota de Drive. A 100 KB por foto, 1 GB da para unas 10.000 piezas.

---

## Qué pasa sin señal

La app guarda todo en el teléfono y marca los registros como pendientes. Al recuperar conexión, **↻ Sincronizar** los envía y trae los totales de toda la red. El contador de pendientes está en ⚙️.

---

## Catálogo de productos

El selector es una cuadrícula de tarjetas con imagen. Desde agosto de 2026 el catálogo son **productos completos** —una férula terminada, que puede constar de una o dos piezas— y no piezas sueltas como antes.

| Categoría | Producto | Archivo | Impresora | Piezas |
|---|---|---|---|---|
| Braquiopalmar | Braquiopalmar termoformada — Adulto | `Braquiopalmar-Adulto.3mf` | Grande | 2 (brazo + antebrazo) |
| Braquiopalmar | Braquiopalmar termoformada — Infantil | `Braquiopalmar-Infantil.3mf` | Mediana | 2 |
| Carpo-Palmar | Carpo-Palmar termoformada — Mediano | `Carpo-Palmar-Mediano.3mf` | Grande | 1 |
| Carpo-Palmar | Carpo-Palmar termoformada — Pequeño | `Carpo-Palmar-Pequeno.3mf` | Mediana | 1 |
| Dedo | Fijación de dedo | `Dedo.3mf` | Mediana y pequeña | 17 por juego de placas |

Las miniaturas de estos cinco son **fotos reales de las piezas impresas**, extraídas de los propios `.3mf` (`Auxiliaries/.thumbnails/`). La del dedo es el render de placa del archivo, teñido con el ámbar de la marca porque no traía foto.

### Archivo

Los 17 modelos de la etapa anterior siguen en el catálogo, en una sección **🗄️ Archivo** al final. No estorban al elegir, pero permiten registrar impresiones pendientes y —lo importante— **los registros históricos siguen sumando en el Resumen**. Sus miniaturas se redujeron a 120 px para no cargar el archivo.

### Para cambiar el catálogo

Edita el array `MODELOS` en `index.html` — `{ n: "nombre visible", a: "archivo", p: "impresora y piezas" }` — y el array `CATALOGO` del Apps Script.

> **Los nombres deben coincidir carácter por carácter entre los dos**, tildes y rayas incluidas: el Resumen los cruza con `SUMIF`, que compara texto exacto. `Adulto` y `— Adulto` con raya distinta son dos productos diferentes para la hoja.

Las descargas se editan en el modal `id="m-files"` de `index.html`, y los `.3mf` viven en `makersporcolombia/archivos/`.

---

## Catálogo de la comunidad

Cuando alguien registra un modelo con **✏️ Otro modelo**, su foto de Drive se convierte en una tarjeta que ven todos los demás, en la sección **🌱 De la comunidad** del catálogo. No hay que aprobar nada: aparece en cuanto los otros teléfonos sincronizan.

Cada tarjeta muestra cuántos talleres lo han hecho y cuántas unidades llevan, así se distingue lo consolidado de lo anecdótico.

**Contra los nombres repetidos** hay tres capas:

1. La sección de comunidad se ve antes de llegar al botón de escribir a mano
2. Mientras escribe, la app sugiere lo que ya existe y basta tocarlo
3. Al guardar, el nombre se normaliza — sin tildes, sin mayúsculas, sin espacios de más — y si coincide con algo existente se adopta el nombre ya registrado

Esa tercera capa hace que `FERULA  DEDO   PULGAR` y `Férula dedo pulgar` terminen siendo la misma fila del Resumen. Y si escriben mal un modelo **oficial** («fijacion de dedo v3»), la app lo reconoce y recupera su `.stl` y su categoría.

Dos límites que conviene tener presentes:

- La sección solo aparece **después de sincronizar**. Un teléfono recién estrenado y sin señal no la ve.
- La deduplicación es por **texto normalizado**, no por parecido. `Férula pulgar` y `Férula de pulgar` seguirán siendo dos modelos distintos. Si se acumula ruido, se limpia editando la columna `Modelo` en el Sheet: al unificar el texto ahí, las tarjetas se fusionan solas.

Para **promover** un modelo de la comunidad al catálogo oficial: consigue el `.stl`, genera su miniatura y agrégalo a `MODELOS` y a `CATALOGO` con el mismo nombre. Los registros históricos se reagrupan solos.

---

## Tratamiento de datos

- El registro inicial exige **nombre, taller, ciudad y correo**, más la casilla de autorización, que guarda un sello de tiempo en la columna `Consentimiento`.
- La política está en `index.html`, busca `id="m-pol"`.
- El `doGet` que alimenta el panel **no devuelve correo ni teléfono**.

> **Antes de publicar:** en esa política reemplaza el responsable y pon un correo de contacto real para peticiones de habeas data. Sin eso el aviso está incompleto frente a la Ley 1581.

Las fotos ahora **sí salen del dispositivo** y viven en Drive. Los voluntarios deben fotografiar únicamente la pieza fabricada, nunca a un paciente ni documentos clínicos.

---

## El archivo `Makers-por-Colombia-datos.xlsx`

Quedó como **respaldo y referencia**, no como parte del flujo: el Apps Script ya construye `Registro` y `Resumen` directamente en la nube. Sirve si algún día quieres trabajar los datos en Excel sin conexión, o para consultar el diccionario de columnas.
