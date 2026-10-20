# Data Card: Evaluarea Derivei Senzorilor Low-Cost de Calitate a Aerului
**Cod Unitate:** U12 (senzor × zi)  
**Autor:** Gușe Ovidiu-Marius  
**Interval analizat:** 12 Octombrie 2025 – 12 Octombrie 2026 (366 zile)  
**Locație:** București, România  

---

## 1. Sursa 1: Stația Oficială de Referință RNMCA B-1 (Cercul Militar)
* **Proveniență & Acces:** Rețeaua Națională de Monitorizare a Calității Aerului (RNMCA), Ministerul Mediului. Date descărcate prin portalul public [calitateaer.ro](https://www.calitateaer.ro) (Fișier: `Raport_20261013210828.xls`).
* **Tip instrument:** Analizor automat certificat de referință (TEOM 1405 - Tapered Element Oscillating Microbalance) și stație meteo automată colocalizată (MTX).
* **Perioadă și frecvență:** 12.10.2025 00:00 – 12.10.2026 23:00 (rezoluție orară brută: 8.781 observații).
* **Rezoluție spațială:** Punct fix de trafic urban central (București - Cercul Militar / Calea Victoriei, Lat 44.4353°, Long 26.0969°).
* **Rezoluție temporală țintă:** Medie zilnică (24h) per indicator.
* **Variabile extrase:**
  * `PM25_Ref` (µg/m³) – Concentrație masică PM2.5 (analizor TEOM).
  * `PM10_Ref` (µg/m³) – Concentrație masică PM10 (analizor TEOM).
  * `Temp_Ref` (°C) – Temperatura aerului la sol.
  * `RH_Ref` (%) – Umiditatea relativă a aerului.
  * `Wind_Ref` (m/s) – Viteza vântului la sol.
* **Calitatea datelor & Goluri:** Peste 99.5% disponibilitate a datelor (8.746 ore valide). Golurile orare scurte (<3 ore consecutive datorate autocalibrării zilnice) au fost tratate prin interpolare liniară locală. Pe rezoluția zilnică există 366/366 zile acoperite complet (0% zile lipsă).
* **Licență:** Publică (Open Data guvernamental pentru cercetare și informare publică).

---

## 2. Sursa 2: Senzorul Low-Cost PurpleAir (Bd. Dacia)
* **Proveniență & Acces:** Rețeaua globală civică PurpleAir. Date descărcate prin platforma oficială [map.purpleair.com](https://map.purpleair.com) (Fișier: `raw-pm25-gm.csv`).
* **Tip senzor:** Dispozitiv optic bazat pe difuzia luminii laser (Light Scattering), echipat intern cu două module Plantower PMS5003 independente (Canal A și Canal B).
* **Perioadă și frecvență:** 12.10.2025 – 12.10.2026 (rezoluție zilnică directă: 366 observații).
* **Rezoluție spațială:** Punct fix urban colocalizat în București (Bd. Dacia, la o distanță de ~1.5 km de stația oficială RNMCA B-1).
* **Variabile extrase:**
  * `PM25_PA_A` (µg/m³) – Concentrație PM2.5 înregistrată de canalul laser optic A.
  * `PM25_PA_B` (µg/m³) – Concentrație PM2.5 înregistrată de canalul laser optic B.
  * `PM25_PA_Mean` (µg/m³) – Media canalelor interne A și B.
  * `Diff_AB` (µg/m³) – Diferența absolută |A - B| dintre canale (indicator intern de integritate optică).
* **Calitatea datelor & Goluri:** 366 zile valide din 366 (100% acoperire continuă, 0 zile lipsă). Coerența internă între canalele duale este ridicată ($R^2 = 0.941$).
* **Licență:** Open Data / Creative Commons Attribution (PurpleAir Community).

---

## 3. Raport de Aliniere și Structura Matricei X
* **Cheie comună de aliniere:** `Data` calendaristică normalizată (`YYYY-MM-DD`).
* **Dimensiunea matricei X:** $N = 366$ observații (zile) $\times$ $d = 9$ trăsături numerice.
* **Rata de retenție (Acoperire comună):** 100% (toate cele 366 de zile se regăsesc în ambele surse de date).
* **Offset sistematic identificat:** Valoarea medie raportată de PurpleAir este mai mică cu $11.48\ \mu\text{g/m}^3$ față de instrumentul TEOM de referință, evidențiind subestimarea clasică a senzorilor optici la particule grosiere/umiditate necorectată.
* **Protocol de split:** Split strict temporal — Primele 183 de zile pentru calibrare/antrenare (12 Oct 2025 – 12 Apr 2026), următoarele 183 de zile pentru testare și detectarea derivei optice (13 Apr 2026 – 12 Oct 2026).