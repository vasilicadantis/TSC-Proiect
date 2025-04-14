# OpenBook

**-TSC-**  
Vasilica Danțiș – 332CD

## Diagrama bloc
![image](https://github.com/user-attachments/assets/3b14aadc-2e50-4f4a-9420-7902c60ad398)

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

