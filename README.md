# SDSS Pemodelan Bahaya & Dampak Asap
# Provinsi Kalimantan Barat

**Spatial Decision Support System (SDSS)** berbasis WebGIS untuk pemantauan kejadian kebakaran hutan dan lahan (karhutla), pemodelan dispersi polutan PM<sub>2.5</sub> (HYSPLIT), dinamika meteorologi angin & curah hujan, serta analisis risiko dan paparan terhadap penduduk maupun fasilitas vital di Provinsi Kalimantan Barat (periode kajian **1 Agustus – 31 Oktober 2026**, dengan slot *Forecast* **1 – 3 November 2026**).

Dikembangkan oleh **Kelompok 5 — Mata Kuliah GD4103 Sistem Informasi Geografis (ITB)**.

🌐 **Live Demo:** [https://cyberimg05.github.io/webgis-karhutla-kalbar/](https://cyberimg05.github.io/webgis-karhutla-kalbar/)

---

## Fitur Utama

1. **Integrasi Data Spasial & Meteorologi Multi-Sumber**
   - **Sebaran PM<sub>2.5</sub> Harian (HYSPLIT):** Poligon konsentrasi PM<sub>2.5</sub> harian (`1 Agt – 31 Okt 2026`) yang diklasifikasikan berdasarkan kategori ISPU (`Baik`, `Sedang`, `Tidak Sehat`, `Sangat Tidak Sehat`, `Berbahaya`) lengkap dengan nilai rata-rata, maksimum, dan luas zona (`km²`).
   - **Medan Angin Reanalisis ERA5 (Darat + Laut + Buffer):** Grid `0,25°` (`106,0°–117,0° BT`, `-5,5°–4,5° LS`, `1 Agt – 3 Nov 2026`) dalam format terindeks (`ERA5_Wind_UV_Kalbar_Buffer_2026_Indexed.json`) dengan animasi *streamlines* kanvas, *outline* batas domain ERA5, serta telemetri arah dan kecepatan rata-rata khusus daratan Kalimantan Barat (`km/jam` & `m/s`).
   - **Curah Hujan Harian Gabungan (CHIRPS + ERA5-Land):** Data curah hujan harian `1 Agt – 30 Sep 2026` dari **UCSB CHIRPS Daily** (`0,05°`) yang dilanjutkan `1 Okt – 3 Nov 2026` menggunakan **ECMWF ERA5-Land** (`0,1°`), tersaji dalam format JSON terindeks ringan (`Curah_Hujan_Kalbar_2026_Indexed.json`) dengan agregasi otomatis per Kabupaten/Kota dan dukungan *fallback* CSV.
   - **Titik Api & FRP (VIIRS 375 m):** Gabungan deteksi sensor NOAA-20, NOAA-21, dan Suomi-NPP (`1 Agt – 30 Okt 2026`) yang tersaring otomatis mengikuti tanggal aktif pada *time-slider* (`acq_date`).
   - **Lintasan Partikel HYSPLIT Mingguan:** Trajektori NOAA HYSPLIT pada tiga ketinggian (`20 m`, `500 m`, dan `1.000 m AMSL`) dari klaster FRP tertinggi (`trajektori_hysplit_mingguan.geojson`), dengan *fallback* estimasi vektor angin ERA5 pada mode simulasi manual atau *forecast*.
   - **Area Terbakar (*Burned Area*):** Poligon bekas area terbakar dari produk NASA MODIS MCD64A1 v061 periode **Agustus – September 2026**.
   - **Lahan Gambut (KHG) & Batas Administrasi BPS:** Poligon Kesatuan Hidrologis Gambut (KHG) Kalimantan Barat serta batas administrasi 14 Kabupaten/Kota lengkap dengan data kepadatan (`KEPADATAN`) dan jumlah penduduk (`JML_PDDK`) BPS.
   - **Fasilitas & Objek Vital (HOT OSM):** Pemetaan terpisah untuk **Fasilitas Kesehatan**, **Fasilitas Pendidikan**, serta **Bandara & Helipad** (titik, poligon area, dan garis landasan pacu).
   - **Data Pembanding Satelit & Reanalisis:** Layer pembanding `CAMS PM2.5 (Agt–Okt)`, seri mingguan `MERRA-2 PM2.5 (Mingguan)`, dan `MODIS AOD (Mingguan)`.

2. **Filter Wilayah Administrasi Terpadu & *ROI Spotlight Mask***
   - Pemilihan per Kabupaten/Kota (14 wilayah) otomatis mengarahkan tampilan peta (*fly-to bounds*), menyorot batas administrasi terpilih, mengaktifkan *ROI Spotlight Mask* (penggelapan area di luar fokus), serta menyaring seluruh layer, telemetri curah hujan, dan statistik secara *real-time*.

3. **Kontrol Layer Terstruktur, Legenda Dinamis & Mode Ringan**
   - Pengelompokan *dropdown accordion* (*Fasilitas & Objek Vital*, *Gambut, Trajektori & Batas*, dan *Data Pembanding Satelit*) dengan penghitung layer aktif serta **Legenda Peta Dinamis** yang menyesuaikan layer yang sedang ditampilkan.
   - Startup ringan dengan *lazy rendering* serta tombol kontrol aktif/jeda pada fitur berat (*Kalkulator Paparan*, *Top 5 Wilayah Terdampak*, dan *Indeks Risiko Bencana*) yang otomatis terjeda saat *time-slider* digeser/diputar agar navigasi tanggal tetap lancar.
   - Dilengkapi **Welcome Modal**, **Panduan Singkat & Kamus Istilah**, **Loading Overlay**, serta tombol **Fokus Peta** pada header untuk menyembunyikan panel samping saat presentasi.

4. **Time-Slider Temporal Dua Tingkat**
   - **Mode Harian (`1 Agt – 3 Nov`):** Memantau dinamika musiman hingga fase proyeksi `1–3 November 2026`, dilengkapi tombol langkah harian (`‹` / `›`) dan animasi *Play/Pause*.
   - **Mode Episode Puncak (`26 Agt – 3 Sep`):** Fokus harian pada episode puncak kabut asap akhir Agustus – awal September 2026.

5. **Kalkulator Paparan *On-The-Fly* & Top 5 Wilayah Terdampak (Turf.js)**
   - Menghitung luas zona yang melampaui ambang batas bahaya PM<sub>2.5</sub> (default `55 µg/m³`), estimasi populasi terpapar berbasis irisan spasial kepadatan penduduk BPS per Kab/Kota, jumlah sekolah, faskes, dan bandara/helipad terdampak, grafik sebaran luas per kategori ISPU, serta peringkat otomatis **Top 5 Wilayah Terdampak**.

6. **Indeks Risiko Bencana (BNPB / IPCC) & Skenario Mitigasi (*What-If*)**
   - Menghitung skor risiko ternormalisasi (`0,00 – 1,00`) dari perkalian komponen **Bahaya (*H*)** (konsentrasi PM<sub>2.5</sub> & durasi paparan `> 55,4 µg/m³` sejak 1 Agustus) dengan **Kerentanan & Keterpaparan (*V&E*)** (jumlah poligon gambut KHG, fasilitas kesehatan/pendidikan, dan kepadatan penduduk tertimbang).
   - Simulasi *what-if* reduksi emisi hotspot (`0% – 80%`) serta *override* arah dan kecepatan angin manual.

7. **Validasi Kuantitatif Model, Instrumen Aksi BPBD/Dinkes & Ekspor Laporan**
   - **Validasi Kuantitatif Model:** Menghitung metrik *N*, Korelasi Pearson (*r*), R², *Bias* (ME), dan RMSE antara keluaran model HYSPLIT terhadap data pembanding MERRA-2, MODIS AOD, dan CAMS.
   - **Instrumen Aksi BPBD & Dinkes Dinamis:** Menyusun rekomendasi penanganan otomatis sesuai tingkat bahaya wilayah aktif disertai tombol **Salin Briefing Cepat** ke *clipboard*.
   - **Panel Statistik, Ekspor CSV & Cetak Laporan A4 Portrait:** Menyajikan 3 grafik Chart.js (termasuk tren harian gabungan PM<sub>2.5</sub> Maks, Titik Api VIIRS, dan Curah Hujan), 3 tabel ringkasan, unduh **CSV** lengkap, serta cetak laporan **A4 Portrait** dengan *snapshot* peta & legenda aktif.

---

## Teknologi yang Digunakan

- **Arsitektur:** *Single-file* WebGIS (HTML5, CSS3, Vanilla JavaScript ES6+)
- **Peta Interaktif:** [Leaflet.js v1.9.4](https://leafletjs.com/) (`preferCanvas: true` + *custom Canvas wind streamlines*)
- **Analisis Geospasial Client-Side:** [Turf.js v6](https://turfjs.org/) (indeks grid spasial `0,25°`, irisan poligon BPS, *exposure duration grid* `0,05°`)
- **Visualisasi Grafik:** [Chart.js v4.4.1](https://www.chartjs.org/)

---

## Struktur Repositori

```text
webgis-karhutla-kalbar/
├── index.html                                         # Aplikasi utama WebGIS (single-file HTML/CSS/JS)
├── README.md                                          # Dokumentasi proyek
├── Batas_KabKota_KalimantanBarat.geojson              # Batas administrasi 14 Kab/Kota Kalbar & data BPS
├── CAMS_PM25.geojson                                  # Data pembanding konsentrasi PM2.5 CAMS (Agt–Okt)
└── data_pjbl/
    ├── asap_pm25_harian_ispu.geojson                  # Poligon sebaran PM2.5 harian model HYSPLIT
    ├── burned_area_modis_mcd64a1.geojson              # Poligon area terbakar MODIS MCD64A1 (Agt–Sep 2026)
    ├── khg_gambut_kalbar.geojson                      # Poligon Kesatuan Hidrologis Gambut (KHG)
    ├── ERA5_Wind_UV_Kalbar_Buffer_2026_Indexed.json   # Grid angin ERA5 darat+laut+buffer terindeks (95 hari)
    ├── Curah_Hujan_Kalbar_2026_Indexed.json           # Curah hujan harian terindeks (CHIRPS + ERA5-Land)
    ├── CHIRPS_Curah_Hujan_Kalbar_2026_WebGIS.csv      # Dataset CSV curah hujan harian (fallback)
    ├── trajektori_hysplit_mingguan.geojson            # Lintasan partikel NOAA HYSPLIT mingguan
    ├── hotspot/                                       # Data titik api VIIRS 375 m (1 Agt – 30 Okt 2026)
    │   ├── hotspot_viirs_noaa20.geojson
    │   ├── hotspot_viirs_noaa21.geojson
    │   └── hotspot_viirs_snpp.geojson
    ├── layer_dampak/                                  # Objek vital (HOT OSM)
    │   ├── airport_point.geojson
    │   ├── airport_polygon.geojson
    │   ├── airport_polyline.geojson
    │   ├── education_point.geojson
    │   ├── education_polygon.geojson
    │   ├── health_point.geojson
    │   └── health_polygon.geojson
    ├── merra2_mingguan/                               # Seri mingguan NASA MERRA-2 PM2.5
    └── MODIS_mingguan/                                # Seri mingguan NASA MODIS AOD
```
