# Kerepetas 2026 – matavimo sistema

Matavimo sistema su PoE kamera, Raspberry Pi 5, STM32 valdikliu ir 5G ryšiu, maitinama iš 48 V LiFePO4 16S baterijos.

## Dokumentai

| Dokumentas | Failas |
| --- | --- |
| Blokinė schema (PDF) | [docs/blokine_schema.pdf](docs/blokine_schema.pdf) |
| Komponentų sąrašas (PDF) | [docs/komponentai.pdf](docs/komponentai.pdf) |

## Blokinė schema

```mermaid
flowchart TD
    G1["G1 Baterija<br/>LiFePO4 16S, 40–58,4 V"] --> F1["F1 Saugiklis-jungiklis<br/>Hager L501PV, gPV 6 A"]
    F1 --> U1["U1 Keitiklis<br/>Mean Well DDR-120C-48<br/>48,0 V, 120 W"]
    U1 -- "48,0 V DC" --> A1["A1 PoE komutatorius<br/>Teltonika TSW100"]
    U1 -- "48,0 V DC" --> F2["F2, VD1 Apsauga<br/>gPV 2 A + TVS SMBJ48A"]
    F2 --> A2["A2 5G maršrutizatorius<br/>Teltonika RUTC50"]
    A1 -- "PoE 1" --> A4["A4 IP PoE kamera"]
    A1 -- "PoE 2" --> A3["A3 Raspberry Pi 5 4 GB<br/>+ PoE HAT (H)"]
    A1 <-- "LAN, 5 prievadas" --> A2
    A2 <-- "4× koaks." --> W1["W1 Išorinė 5G antena<br/>4×4 MIMO"]
    A3 -- "USB: 5 V + UART" --> A5["A5 STM32 valdiklis"]
```

## Svarbiausi parametrai

- **Baterija:** LiFePO4 16S, darbinė įtampa ~51–53 V, pilnai įkrauta iki 58,4 V.
- **48 V linija:** DDR-120C-48 išėjimą nustatyti tiksliai **48,0 V**. RUTC50 įėjimo riba yra 50 V, o TSW100 PoE išėjimui reikia ≥44 V.
- **Suvartojimas:** ~50 W (kamera ~10 W, Pi 5 ~20 W, RUTC50 iki ~18 W), apie 1 A iš baterijos.
- **Raspberry Pi 5:** į `/boot/firmware/config.txt` įrašyti `usb_max_current_enable=1`.
