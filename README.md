# Kerepetas 2026 – matavimo sistema

Matavimo sistema su PoE kamera, Raspberry Pi 5, STM32 valdikliu ir 5G ryšiu, maitinama iš 48 V LiFePO4 16S baterijos.

## Dokumentai

| Dokumentas | Failas |
| --- | --- |
| Blokinė schema (PDF) | [docs/blokine_schema.pdf](docs/blokine_schema.pdf) |
| Komponentų sąrašas (PDF) | [docs/komponentai.pdf](docs/komponentai.pdf) |

## Blokinė schema

![Blokinė schema](docs/blokine_schema.png)

## Pirkimo nuorodos

| Žymuo | Komponentas | Parduotuvė |
| --- | --- | --- |
| F1 | Hager L501PV saugiklio laikiklis | [aio.lv](https://aio.lv/en/product--hager-l501pv--7691240) |
| U1 | Mean Well DDR-120C-48 | [Lemona](https://www.lemona.lt/en/120w-dc-dc-converter-33-6-67-2v-48v-2-5a-on-the-din-mean-well.html) · [TME](https://www.tme.eu/gb/details/DDR-120C-48/) |
| A1 | Teltonika TSW100 | [Lemona](https://lemona.lt/teltonika-tsw100-poe-switch-5x-rj45-1000mb-s-4x-poe-60w-teltonika.html) |
| A2 | Teltonika RUTC50 | [Lemona](https://www.lemona-electronics.eu/router-teltonika-lte-rutc50.html) |
| A3 | Raspberry Pi 5 4 GB | [Lemona](https://www.lemona.lt/en/single-board-computer-raspberry-pi-5-b-4gb-ram.html) |
| A3 HAT | Waveshare PoE HAT (H) | [Waveshare](https://www.waveshare.com/poe-hat-h.htm?sku=30901) |

Jei Lemonos nuoroda neatsidaro, Lemonos paieškoje įvesk prekės kodą (pvz., `DDR-120C-48`).
PDF faile parduotuvių pavadinimai irgi yra nuorodos, bet GitHub peržiūroje jie neveikia – reikia PDF atsisiųsti.

## Svarbiausi parametrai

- **Baterija:** LiFePO4 16S, darbinė įtampa ~51–53 V, pilnai įkrauta iki 58,4 V.
- **48 V linija:** DDR-120C-48 išėjimą nustatyti į **47,0 V**. RUTC50 įėjimo riba yra 50 V (lieka 3 V atsarga), o TSW100 PoE išėjimui reikia ≥44 V. Keitiklis stabilizuotas ir izoliuotas, todėl atskiro TVS diodo nereikia.
- **Suvartojimas:** ~50 W (kamera ~10 W, Pi 5 ~20 W, RUTC50 iki ~18 W), apie 1 A iš baterijos.
- **Raspberry Pi 5:** į `/boot/firmware/config.txt` įrašyti `usb_max_current_enable=1`.
