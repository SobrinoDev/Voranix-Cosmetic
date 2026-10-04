# Voranix Cosmetic

Catálogo de cosméticos de la comunidad **Voranix**: capas, alas, sombreros y mascotas. Cada jugador con
Voranix Client arma su outfit en el **menú de cosméticos** (tecla **J**, o el botón **Cosméticos** del menú
de pausa). En servidores con **Voranix Server** todos ven los cosméticos de todos; en otros servidores solo
uno mismo ve los suyos. Quien no tenga Voranix no los ve.

## Cómo está organizado

| Categoría | Sección en `capas.json` | Archivos |
|---|---|---|
| Capas | `capas` | `capas/<id>.png` |
| Alas | `alas` | `alas/<id>.json` + `alas/<id>.png` |
| Sombreros | `sombreros` | `sombreros/<id>.json` + `sombreros/<id>.png` |
| Mascotas | `mascotas` | `mascotas/<id>.json` + `mascotas/<id>.png` |

`<id>` es el nombre del cosmético: minúsculas, sin espacios ni acentos (solo letras, números, `-` y `_`).
En cada sección, `nombre` es lo que se ve en el menú y el orden del archivo es el orden del menú.

## Cómo agregar una capa nueva

1. Sube la imagen a la carpeta `capas/` con un nombre en minúsculas, sin espacios ni acentos
   (solo letras, números, `-` y `_`). Por ejemplo `capas/dragon.png`.
2. Agrégala en `capas.json` con ese mismo nombre (sin `.png`):

```json
{
  "capas": {
    "nyan": { "nombre": "Nyan Cat", "velocidad": 100 },
    "dragon": { "nombre": "Dragón Voranix" }
  }
}
```

- `nombre`: lo que se ve en el menú.
- `velocidad` (opcional): milisegundos por cuadro en capas animadas (por defecto 100; mínimo 20).
- El orden del archivo es el orden del menú.
- Cuidado con las comas: la última capa **no** lleva coma después de `}`. Si el JSON queda mal,
  los jugadores siguen viendo el último catálogo que funcionó.

Para **quitar** una capa del menú, bórrala de `capas.json` (quien ya la tenga puesta la sigue usando
mientras la imagen exista en `capas/`).

## Formato de la imagen

- **Capa fija:** PNG con proporción 2:1 y el mismo diseño que una capa de Minecraft
  (64x32, o más grande manteniendo la proporción: 128x64, 384x192, 1024x512...).
  El frente de la capa (lo que se ve en el menú) es el rectángulo de 10x16 que empieza en (1, 1)
  en una capa de 64x32.
- **Capa animada:** los cuadros van **uno debajo del otro**, cada uno 2:1.
  Ejemplo: `nyan.png` mide 384x1728 = 9 cuadros de 384x192.
- Tamaño máximo: 16 MB por imagen.

## Élitros

La misma imagen de la capa lleva el diseño de los élitros, en la zona de la derecha
(en una capa de 64x32: de (22,0) a (46,22)). Si esa zona está vacía, las alas se ven transparentes.

- La cara que se ve **desde atrás** del jugador es el rectángulo de 10x20 que empieza en (36, 2).
- La cara de **adentro** es el de 10x20 que empieza en (24, 2): conviene poner ahí el mismo diseño en espejo,
  para que el ala se vea desde los dos lados.
- Las partes transparentes recortan la forma del ala (por ejemplo, plumas).

## Alas, sombreros y mascotas (modelos 3D)

Se hacen en **Blockbench** (gratis, blockbench.net):

1. *Archivo → Nuevo → Bedrock Entity* (o abre uno de los ejemplos de este repositorio).
2. Modela con el jugador **parado en el origen**, como en la plantilla de jugador de Bedrock:
   los pies en Y=0, el cuerpo de Y=12 a Y=24, la cabeza de Y=24 a Y=32, el frente mirando al **norte**.
   - **Sombreros**: sobre la cabeza (desde Y≈32). Siguen los movimientos de la cabeza.
   - **Alas**: en la espalda (Z≈2). Siguen al cuerpo; no se ven con élitros puestos.
   - **Mascotas**: sobre un hombro (el derecho del jugador está en X entre -8 y -4, arriba en Y=24). Siguen al cuerpo.
3. Pinta la textura (UV de caja o por cara, las dos funcionan). Las partes transparentes se recortan.
4. *Archivo → Exportar → Exportar Bedrock Geometry* → guárdalo como `<id>.json`, y la textura como `<id>.png`,
   en la carpeta de su categoría.
5. Agrégalo en `capas.json` en la sección de su categoría.

Ejemplos: `sombreros/mago`, `alas/neon` y `mascotas/slime`.

Soporta huesos (con padre, pivote y rotación) y cubos con rotación, inflate y mirror. Las animaciones de
Blockbench todavía no se usan: los modelos se ven quietos.

## Cuándo se ven los cambios

- El catálogo se relee cada 5 minutos (GitHub además puede tardar unos minutos en actualizar).
- Si **cambias la imagen o el modelo** de un cosmético que ya existe, se verá al reiniciar el juego. Para que
  se vea antes, súbelo con otro nombre (por ejemplo `dragon2`) y actualiza `capas.json`.
