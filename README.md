# StlinkV2

Firmware y notas para flashear **ST-Link V2** (y Black Magic Probe) en una **Blue Pill** / clones STM32F103.

Fuente del toolkit: [mike-pittelko/stlink-v2-repair-and-toolkit](https://github.com/mike-pittelko/stlink-v2-repair-and-toolkit)

## Archivos

| Path | Descripción |
|------|-------------|
| `firmware/stlink-v2/STLinkV2.J16.S4.bin` | Firmware ST-Link V2 base (64 KiB). Luego actualizar con STSW-LINK007. |
| `firmware/blackmagic/Blackmagic_dfu-*.bin` | Bootloader DFU Black Magic → `0x08000000` |
| `firmware/blackmagic/Blackmagic-*.bin` | Firmware Black Magic Probe → `0x08002000` |
| `firmware/README.md` | Pasos de flash y mapa de pines |

## Flash rápido (Blue Pill como ST-Link)

Con otro programador SWD:

```bash
st-flash erase
st-flash --reset write firmware/stlink-v2/STLinkV2.J16.S4.bin 0x8000000
```

Después conectá la Blue Pill por USB y actualizá con **STLinkUpgrade** / CubeProgrammer.

### Pines hacia el target (firmware ST-Link)

| Señal | Pin MCU |
|-------|---------|
| SWDIO | PB14 |
| SWCLK | PA5 / PB13 |
| RST | PB6 |
| LED | PA9 |

Detalle completo en [`firmware/README.md`](firmware/README.md).

## Aviso

`STLinkV2.J16.S4.bin` es firmware propietario de ST redistribuido por el toolkit de referencia. Uso personal / recuperación.
