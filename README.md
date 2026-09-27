# Voranix Cosmetic

Capas de la comunidad **Voranix**. Todos los jugadores con Voranix Client descargan este repositorio
y ven las capas de todos, en cualquier servidor. Quien no tenga Voranix no las ve.

## Cómo darle una capa a un jugador

Edita `capas.json` y agrega el nombre del jugador en `jugadores`, con el nombre de la capa:

```json
{
  "jugadores": {
    "SobrinoDev": "nyan",
    "OtroJugador": "dragon"
  },
  "capas": {
    "nyan": { "nombre": "Nyan Cat", "velocidad": 100 },
    "dragon": { "nombre": "Dragón Voranix" }
  }
}
```

- El nombre del jugador es su nombre de Minecraft (no importan mayúsculas/minúsculas).
- Cada jugador tiene una sola capa. Para quitársela, borra su línea.
- Cuidado con las comas: la última línea de cada bloque **no** lleva coma. Si el JSON queda mal,
  los jugadores siguen viendo la última lista que funcionó.

## Cómo agregar una capa nueva

1. Sube la imagen a la carpeta `capas/` con un nombre en minúsculas, sin espacios ni acentos
   (solo letras, números, `-` y `_`). Por ejemplo `capas/dragon.png`.
2. Ese nombre (sin `.png`) es el que se usa en `jugadores`.
3. Opcional: agrégala en `capas` con su `nombre` y `velocidad`.

### Formato de la imagen

- **Capa fija:** PNG con proporción 2:1, con el mismo diseño que una capa de Minecraft
  (64x32, o más grande manteniendo la proporción: 128x64, 384x192, 1024x512...).
- **Capa animada:** los cuadros van **uno debajo del otro**, cada uno 2:1.
  Ejemplo: `nyan.png` mide 384x1728 = 9 cuadros de 384x192.
- `velocidad`: milisegundos por cuadro (por defecto 100; mínimo 20).
- Tamaño máximo: 16 MB por imagen.

## Cuándo se ven los cambios

- La lista se relee cada 5 minutos (GitHub además puede tardar unos minutos en actualizar).
- Si **cambias la imagen** de una capa que ya existe, se verá al reiniciar el juego. Para que se vea
  antes, súbela con otro nombre (por ejemplo `dragon2.png`) y cambia el nombre en `capas.json`.
