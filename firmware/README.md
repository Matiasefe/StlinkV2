# Firmware para Blue Pill / ST-Link clone

Fuente: [mike-pittelko/stlink-v2-repair-and-toolkit](https://github.com/mike-pittelko/stlink-v2-repair-and-toolkit)

## Archivos

| Archivo | Uso |
|---------|-----|
| `stlink-v2/STLinkV2.J16.S4.bin` | Firmware ST-Link V2 (base). Después conviene actualizar con `STLinkUpgrade` (STSW-LINK007). |
| `blackmagic/Blackmagic_dfu-*.bin` | Bootloader DFU Black Magic (offset `0x08000000`) |
| `blackmagic/Blackmagic-*.bin` | Firmware Black Magic Probe (offset `0x08002000`) |

## Opción A — Blue Pill como ST-Link V2

Necesitás **otro** programador SWD (otro ST-Link, J-Link, etc.) conectado a los pines SWD de la Blue Pill (`SWDIO`, `SWCLK`, `GND`, `3V3`).

```bash
# Unlock (si hace falta)
openocd -f interface/stlink-v2.cfg -f target/stm32f1x.cfg \
  -c "init" -c "halt" -c "stm32f1x unlock 0" -c "shutdown"

# Power-cycle de la Blue Pill, después:
st-flash erase

# Flashear imagen base
openocd -f interface/stlink-v2.cfg -f target/stm32f1x.cfg \
  -c "init" -c "halt" \
  -c "flash write_image erase firmware/stlink-v2/STLinkV2.J16.S4.bin 0x8000000" \
  -c "shutdown"
```

Alternativa con `st-flash`:

```bash
st-flash --reset write firmware/stlink-v2/STLinkV2.J16.S4.bin 0x8000000
```

Después:

1. Desconectá el programador auxiliar.
2. Conectá la Blue Pill por USB (conector USB propio).
3. Actualizá con **STLinkUpgrade** / CubeProgrammer (`STSW-LINK007`).

### Pines del firmware ST-Link (hacia el target)

El firmware ST-Link **no** usa el LED PC13 de la Blue Pill ni el header SWD “de fábrica” para programar al target. Usa el mapa del clon:

| Señal al target | Pin MCU Blue Pill |
|-----------------|-------------------|
| RST | PB6 (feedback PB5) |
| SWDIO | PB14 (feedback PB12) |
| SWCLK | PA5 + PB13 |
| SWIM | PB8 + PB11 |
| LED (status) | PA9 |

USB del ST-Link: `PA11` / `PA12`. En muchas Blue Pill el pull-up USB (R10) está mal (10k en vez de 1.5k); si no enumerá, revisá eso.

## Opción B — Blue Pill como Black Magic Probe (recomendado en ese toolkit)

Mejor para Blue Pill: GDB server embebido, open source.

```bash
st-flash write firmware/blackmagic/Blackmagic_dfu-v1.6-rc0-213-gdf7ad91.bin 0x8000000
st-flash --reset write firmware/blackmagic/Blackmagic-v1.6-rc0-213-gdf7ad91.bin 0x8002000
```

Nota: esos `.bin` del toolkit están pensados para **clon ST-Link de 64 KB**. En Blue Pill a veces conviene un build BMP específico para `bluepill` desde [blackmagic](https://github.com/blackmagic-debug/blackmagic).

## SHA256

```
1e7ffb1a6f0d40faa1a1cbebf37e3c4acc6ecc2da7cb961df282103b66e558f0  STLinkV2.J16.S4.bin
fca14791f9ffa2713d089aae7b0a8574e7fa1517171a75538cabdda1e5267203  Blackmagic_dfu-v1.6-rc0-213-gdf7ad91.bin
b20aa52c179705a6d21729473fe7f7fcf2d23908bd192f95c77932a714f9f1b5  Blackmagic-v1.6-rc0-213-gdf7ad91.bin
```

## Aviso

`STLinkV2.J16.S4.bin` es firmware propietario de ST redistribuido en el toolkit de referencia. Uso personal / recuperación. Para algo open source en Blue Pill, preferí Black Magic Probe.
