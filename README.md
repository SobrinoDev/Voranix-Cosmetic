# Voranix Cosmetic

Catálogo de capas de la comunidad **Voranix**. Cada jugador con Voranix Client elige su capa en el
**menú de capas** (tecla **K**, o el botón **Capas** del menú de pausa). En servidores con
**Voranix Server** todos ven la capa de todos; en otros servidores solo uno mismo ve la suya.
Quien no tenga Voranix no ve las capas.

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

## Cuándo se ven los cambios

- El catálogo se relee cada 5 minutos (GitHub además puede tardar unos minutos en actualizar).
- Si **cambias la imagen** de una capa que ya existe, se verá al reiniciar el juego. Para que se vea
  antes, súbela con otro nombre (por ejemplo `dragon2.png`) y actualiza `capas.json`.
