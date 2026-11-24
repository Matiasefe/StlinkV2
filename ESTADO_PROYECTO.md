# ESTADO_PROYECTO

## Resumen Ejecutivo

Colección de recursos para ST-Link V2 **clones** (esquemáticos y firmware). Incluye el binario `STLinkV2.J16.S4.bin` del toolkit de mike-pittelko para flashear en Blue Pill / clones.

## Avances Recientes

- Agregado `firmware/stlink-v2/STLinkV2.J16.S4.bin` (64 KiB).
- Agregados bins Black Magic Probe del mismo toolkit.
- README con pasos de flash para Blue Pill y mapa de pines ST-Link.

## Siguiente Paso / Tareas Pendientes

- (Opcional) Sumar esquemáticos reverse del dongle aluminio / Baite.
- (Opcional) Build BMP específico `bluepill` más reciente.

## Decisiones Técnicas

- Fuente firmware: https://github.com/mike-pittelko/stlink-v2-repair-and-toolkit
- ST-Link base: `STLinkV2.J16.S4.bin` @ `0x08000000`, luego upgrade con STSW-LINK007.
- Repo Origin: `matias-pompolo/stlink-clones`
- Mirror GitHub: https://github.com/Matiasefe/StlinkV2
