# 🚀 Mioveni Quantum OS (v6.8) - ESP32 Smart Display & Weather Station

Un sistem operativ minimalist și futurist (Quantum OS v6.8) rulat pe un **ESP32** și afișat pe un ecran **TFT LCD ST7735 (1.8")**. Proiectul include telemetrie meteo live de la Open-Meteo, radar termic FLIR simulat pentru zona Mioveni, animații fluide, conexiune Wi-Fi și un modul dedicat de **Ceas & Dată Exactă NTP** sincronizat în timp real.

---

## 📱 Prezentare Ecrane (Pagini Interactive)
Navigarea se face prin 2 butoane externe (`BTN_NEXT` și `BTN_PREV`):
1. **Dashboard Principal:** Temperatură live cu tranziție numerică lină + temperatură resimțită & umiditate.
2. **Telemetrie Meteo:** Presiune atmosferică (hPa), Index UV și vizibilitate.
3. **Radar Termic Live (Mioveni FLIR Map):** Matrice dinamică cu grade termice animate în timp real.
4. **Dinamica Vântului:** Viteza vântului (km/h) și direcția în grade.
5. **System Core:** Informații despre procesorul ESP32, timpul de execuție al ciclului (în microsecunde) și pachetele de date transferate.
6. **Ceas & Dată Exactă NTP:** Ziua săptămânii în limba română (ex: *Marti*), data completă (*25 Aug 2026*) și ora exactă cu **secunde în timp real** (*11:06:52*).

---

## 🛠️ Componente Hardware Necesare
* **Placă de dezvoltare ESP32** (NodeMCU / DevKit 30 pini)
* **Ecran TFT LCD ST7735** (1.8 inch, 128x160 pixeli)
* **2x Push-butoane** (pentru navigarea prin pagini)
* **Fire de legătură (Jumper wires)** și breadboard

---

## 🔌 Diagrama de Conexiuni Complete (Pinout)

### 1. Conexiuni Display TFT ST7735 ➔ ESP32
| Pin Display | Pin ESP32 | Descriere / Funcție |
| :--- | :--- | :--- |
| **GND** | **GND** | Masă comună |
| **VCC / VDD** | **3.3V** | Alimentare (Atenție: folosește 3.3V, nu 5V!) |
| **SCL / SCK** | **GPIO 18** | Magistratura SPI Clock |
| **SDA / MOSI** | **GPIO 23** | Magistratura SPI MOSI (Date) |
| **RES / RST** | **GPIO 4** | Reset Display (`TFT_RST`) |
| **DC / RS** | **GPIO 2** | Data / Command (`TFT_DC`) |
| **CS** | **GPIO 15** | Chip Select (`TFT_CS`) |
| **BLK / LED** | **3.3V** | Iluminare fundal (Backlight) |

### 2. Conexiuni Butoane de Navigare ➔ ESP32
*(Notă: Pinii folosesc `INPUT_PULLUP` intern, deci nu ai nevoie de rezistențe externe. Celălalt pin al butonului se leagă direct la **GND**).*
* **BTN_NEXT (Următorul):** Conectat la **GPIO 13** ➡️ celălalt pol la **GND**
* **BTN_PREV (Anteriorul):** Conectat la **GPIO 12** ➡️ celălalt pol la **GND**

---

## 📚 Biblioteci Obligatorii (Arduino IDE)
Instalează următoarele biblioteci din **Library Manager** (`Tools -> Manage Libraries`):
1. **Adafruit GFX Library** (de Adafruit)
2. **Adafruit ST7735 and ST7789 Library** (de Adafruit)
3. **ArduinoJson** (de Benoit Blanchon - versiunea 6.x sau 7.x)

---

## ⚙️ Ghid de Instalare & Configurare
1. Clonează sau descarcă repository-ul.
2. Deschide fișierul `MioveniQuantumOS_v6.8.ino` în Arduino IDE.
3. Introdu datele rețelei tale Wi-Fi în secțiunea dedicată din cod:
   ```cpp
   const char* ssid     = "NUMELE_TAU_DE_WIFI";
   const char* password = "PAROLA_TA_DE_WIFI";
