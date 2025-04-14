# OpenBook

Vasilica Danțiș – 332CD

## Diagrama bloc
![image](https://github.com/user-attachments/assets/3b14aadc-2e50-4f4a-9420-7902c60ad398)

## BOM

| Componenta                                      | Link                                                                                                                         |
| ------------------------------------------------| -----------------------------------------------------------------------------------------------------------------------------|
| led                                             | [Link](https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/view-part/?company=Politehnica+University+of+Buch&welcome=home&ref=search&t=LED+0603) |
| Button_customv1                                 | [Link](https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k)                         |
| Eagle_ltspice_c                                 | [Link](https://componentsearchengine.com/part-view/0402WGF3001TCE/UNI-ROYAL(Uniroyal%20Elec))                                 |
| ESP32_WROVER_AVX—SD0805S020S1R0                 | [Link](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D)                  |
| ESP32_WROVER_BME680_BME680                      | [Link](https://www.snapeda.com/parts/BME680/Bosch/view-part/?welcome=home)                                                  |
| ESP32_WROVER_EAGLE-LTSPICE_R                    | [Link](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)                         |
| RCL_CPOL-EU                                     | [Link](https://www.snapeda.com/parts/TAJB475K025RNJ/AVX/view-part/?t=capacitor%203528&con_ref=None)                         |
| SJ                                              | [Link](https://grabcad.com/library/solder-jumpers-1)                                                                          |
| R-URI                                           | [Link](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)                         |
| ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH   | [Link](https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated)                                         |
| ESP32_WROVER_SPARKFUN-IC-POWER_MCP73831         | [Link](https://eu.mouser.com/ProductDetail/Microchip-Technology/MCP73831T-2ACI-OT?qs=yUQqVecv4qvbBQBGbHx0Mw%3D%3D)       |
| TP                                              | Facut Manual (un cilindru)                                                                                                                |
| FH34SRJ-24S-0.5SH_99_                           | [Link](https://componentsearchengine.com/part-view/FH34SRJ-24S-0.5SH(99)/Hirose)                                             |
| MAX17048G+T10                                   | [Link](https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/)                                                |
| SAMACSYS_PARTS_USB4110-GF-A                     | [Link](https://componentsearchengine.com/part-view/USB4110-GF-A/GCT%20(GLOBAL%20CONNECTOR%20TECHNOLOGY))                      |
| QWIIC_CONNECTOR                                 | [Link](https://www.snapeda.com/parts/PRT-14417/SparkFun%20Electronics/view-part/?t=QWIIC_CONNECTORJS-1MM)                     |
| 112A-TAAR-R03_ATTEND                             | [Link](https://componentsearchengine.com/part-view/112A-TAAR-R03%20ATTEND/ATTEND)                                             |
| 744043680IND_4828-WE-TPC_WRE                     | [Link](https://componentsearchengine.com/part-view/744043680/W%C3%BCrth%20Elektronik)                                          |
| BD5229G-TR                                      | [Link](https://componentsearchengine.com/part-view/BD5229G-TR/ROHM%20Semiconductor)                                          |
| CPH3225A                                        | [Link](https://componentsearchengine.com/part-view/CPH3225A/Seiko%20Semiconductors)                                          |
| DS3231SN#                                       | [Link](https://componentsearchengine.com/part-view/DS3231SN%23/Analog%20Devices)                                             |
| ESP32-C6-WROOM-1-N8                             | [Link](https://componentsearchengine.com/part-view/ESP32-C6-WROOM-1-N8/Espressif%20Systems)                                  |
| MBR0530                                         | [Link](https://componentsearchengine.com/part-view/MBR0530/onsemi)                                                           |
| SI1308EDL-T1-GE3                                | [Link](https://componentsearchengine.com/part-view/SI1308EDL-T1-GE3/Vishay)                                                  |
| USBLC6-2SC6Y                                    | [Link](https://componentsearchengine.com/part-view/USBLC6-2SC6Y/STMicroelectronics)                                          |
| W25Q512JVEIQ                                    | [Link](https://componentsearchengine.com/part-view/W25Q512JVEIQ/Winbond)                                                     |
| XC6220A331MR-G                                  | [Link](https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex)                                                     |


## Descriere detaliată a funcționalității hardware

1. **Microcontroller (ESP32-C6)**
   - **Rol:** Asigură controlul central al dispozitivului, conectivitatea Wi-Fi, logica de afișare pe E-Ink și interfața cu utilizatorul (butoane).
   - **Caracteristici:**
     - Integrează un nucleu RISC-V și un subsistem Wi-Fi 6 (802.11ax).
     - Consum redus în modurile de *deep-sleep*, esențial pentru un e-book reader.

2. **E-Ink Display**
   - **Tip:** (ex.) 2.9" EPD (monocrom), cu driver intern sau driver separat.
   - **Interfață cu ESP32-C6:** SPI (poate fi 4-wire SPI cu linii de comandă suplimentare: DC, CS, RST, BUSY).
   - **Motiv:** E-Ink-ul are consum redus de energie, menținând imaginea chiar și fără alimentare (refresh scăzut).

3. **Senzor BME688**
   - **Rol:** Permite ajustarea luminozității (dacă există LED) sau stocarea datelor de mediu.
   - **Interfață:** I2C (implicit) / SPI (opțional).
   - **Consum:** Relativ mic (în jur de câțiva µA în mod de stand-by, dar poate crește la câteva mA în mod de funcționare continuă).

4. **DS3231 RTC**
   - **Rol:** Asigură un ceas de timp real foarte precis, cu consum scăzut.
   - **Interfață:** I2C, cu eventual pin de interrupt (INT/SQW) pentru semnal periodic sau alarmă.
   - **Consum:** Aproximativ 1-2 µA în modul de menținere a ceasului (alimentat direct din baterie).

5. **Memorie externă NOR Flash (W25Q512)**
   - **Rol:** Oferă stocare suplimentară (ex. 64Mbit) pentru fișiere, resurse, cărți electronice etc.
   - **Interfață:** SPI la viteze ridicate (până la 40-80MHz, dacă e specificat).
   - **Consum:** Câțiva mA în scriere/citire și µA în mod standby.

6. **Sistem de alimentare și managementul bateriei**
   - **USB-C Connector:** Permite alimentare la 5V și date (pentru programare/debug).
   - **Battery Charger (MCP73831):** Încarcă Li-Po la 4.2V cu un curent setat prin rezistență PROG (ex. 500mA).
   - **LDO / DC-DC:** Convertește tensiunea bateriei (3.7V nominal) în 3.3V stabil pentru ESP32-C6, E-Ink și restul circuitelor. Dacă se dorește extragerea tensiunii de 5V, se poate folosi un boost converter (DC-DC step-up).
   - **Calcul consum (approx.):**
     - **ESP32-C6:** ~80-240 mA în mod Tx Wi-Fi, <1 mA în modem-sleep, câțiva µA în deep-sleep.
     - **E-Ink:** Consum ridicat doar la refresh (~tens of mA), inactiv aproape 0.
     - **Senzor BME688:** <1 mA tipic (pe I2C) în mod standard, <1 µA în stand-by.
     - **RTC DS3231:** 1-2 µA pentru menținerea ceasului.

7. **Interfața utilizator (Butoane)**
   - 3 butoane SMD (ex. Boot, Change, Reset) conectate la pinii GPIO ai ESP32-C6, cu rezistențe de pull-up/pull-down și debounce minimal (sau software).

8. **Alte considerații**
   - Protecție ESD pe USB, liniile SPI, conectori externi.
   - Test pad-uri: Semnalele principale (MISO, MOSI, RX, GND) expuse pentru programare / debugging.

## Detalii despre pinii ESP32-C6
![image](https://github.com/user-attachments/assets/90c5aaaf-b80e-4499-9e53-c3db14ae61c5)
![image](https://github.com/user-attachments/assets/014122e7-4830-46b4-ba82-856d29b7ae15)

## Considerații de design PCB

### Rutarea traseelor de alimentare
- Lățime de minimum **0.3 mm** pentru liniile de putere (3V3, 5V, VBAT).
- Lățime de minimum **0.15 mm** pentru liniile de date (SPI, I2C, UART etc.).
- Grosime PCB de maximum **1 mm** pentru a încăpea în carcasă.

### Decuplare
- Condensatoare de **100 nF (0402)** lângă fiecare pin de alimentare al circuitelor integrate (ESP32, BME688, DS3231, Flash).
- Condensatoare mai mari (ex. **4.7 µF ~ 10 µF**) pentru stabilizarea surselor locale.

### Antenă ESP32-C6
- Zona antenei trebuie eliberată de planul de masă și semnale, cu decupaj PCB sub antenă.

### DRC și ERC
- Verificarea regulilor de design: evitarea unghiurilor de 90°; utilizarea via stitching pe planul GND; respectarea reglementărilor de clearance etc.

### Placement
- Componentele SMD sunt plasate exclusiv pe **Top Layer** (conform specificațiilor proiectului).
- Butoanele sunt poziționate ergonomic pentru utilizator.
- Conectorul USB-C este accesibil pe marginea plăcii.

### Via Stitching
- Implementat în jurul ESP32-C6 și al planului de masă pentru reducerea zgomotului EMI.

### Test pad-uri
- Semnalele MISO, MOSI, SCK, GND, 3V3, TX, RX etc. sunt accesibile pentru programare și debugging.

