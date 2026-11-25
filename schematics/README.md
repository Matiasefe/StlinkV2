# Esquemáticos ST-Link V2 clon (carcasa aluminio)

Dongle USB-A con header 2×5, tipicamente marcado:

```
RST    SWCLK
SWIM   SWDIO
GND    GND
3.3V   3.3V
5.0V   5.0V
```

(Variante A / ~2020. Otras tandas cruzan SWDIO/SWCLK o mueven los GND.)

## Archivos

| Archivo | Qué es |
|---------|--------|
| `aluminum-clone/cuvoodoo-stlink-v2-aluminum-2014.pdf` | **Reverse principal** del mini ST-Link V2 aluminio (CuVoodoo, 2014-06-22). MCU STM32F101C, AMS1117-3.3, cristal 8 MHz, USB con series ~22 Ω y pull-up ~1.5 kΩ en D+. |
| `aluminum-clone/cuvoodoo-baite-stlink-v2.pdf` | Reverse del clon **Baite** (form factor distinto, JTAG+SWD+SWIM). |
| `aluminum-clone/mike-pittelko-stlink-V2-schematic.jpg` | Esquemático “Chinese clone” del toolkit de recovery. |
| `aluminum-clone/avrki-shemf-st-link-v2.jpg` | Otro reverse circulante (referenciado por juju.nz). |

## Fuentes

- CuVoodoo (fotos + PDF): https://wiki.cuvoodoo.info/doku.php?id=jtag → *mini ST-LINK V2*
- PDF directo: https://wiki.cuvoodoo.info/lib/exe/fetch.php?media=jtag:alu.pdf
- Pinout / variantes: https://chiptron.eu/pinouts/st-link-v2-pinout/
- Mapa de pines MCU (aluminio): https://juju.nz/michaelh/project/st_link_dev/

## Mapa MCU típico (firmware ST-Link clon)

| Función | Pin |
|---------|-----|
| USB DM / DP | PA11 / PA12 |
| LED | PA9 |
| SWDIO (target) | PB14 (sense PB12) |
| SWCLK (target) | PA5 + PB13 |
| RST (target) | PB6 (sense PB5) |
| SWIM | PB8 + PB11 (sense PB7/PB9/PB10) |
| Cristal | 8 MHz en OSC_IN/OUT |

ST no publica esquemático del ST-LINK/V2 oficial; estos son reverse de la comunidad.
