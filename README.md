# SDSS Mitigasi & Peringatan Dini Karhutla — Provinsi Kalimantan Barat

**Spatial Decision Support System (SDSS)** berbasis WebGIS untuk pemantauan kejadian kebakaran hutan dan lahan (karhutla), pemodelan sebaran polutan PM2.5 (HYSPLIT), serta analisis dampak paparan terhadap penduduk dan fasilitas vital di Provinsi Kalimantan Barat (periode kajian Agustus – Oktober 2026).

🌐 **Live Demo:** [https://cyberimg05.github.io/webgis-karhutla-kalbar/](https://cyberimg05.github.io/webgis-karhutla-kalbar/)

---

## Fitur Utama

1. **Integrasi Data Spasial & Pemodelan Multi-Sumber**
   - **Sebaran PM2.5 (HYSPLIT):** Poligon konsentrasi PM2.5 harian hasil pemodelan HYSPLIT yang diklasifikasikan berdasarkan kategori ISPU (`Sedang`, `Tidak Sehat`, `Sangat Tidak Sehat`, `Berbahaya`) lengkap dengan nilai rata-rata, maksimum, dan luas zona ($\text{km}^2$).
   - **Titik Api & FRP (VIIRS 375 m):** Gabungan deteksi sensor NOAA-20, NOAA-21, dan Suomi-NPP yang tersaring otomatis mengikuti tanggal aktif pada *time-slider* (`acq_date`).
   - **Area Terbakar (*Burned Area*):** Poligon bekas area terbakar dari produk NASA MODIS MCD64A1 v061.
   - **Lahan Gambut (KHG) & Batas Administrasi:** 178 poligon Kesatuan Hidrologis Gambut (KHG) Kalimantan Barat serta batas administrasi 14 Kabupaten/Kota.
   - **Fasilitas & Objek Vital:** Pemetaan terpisah untuk **Fasilitas Kesehatan**, **Fasilitas Pendidikan**, serta **Bandara & Helipad** (titik, poligon area, dan garis landasan pacu).
   - **Validasi Satelit & Reanalisis:** Layer pembanding konsentrasi PM2.5 dari CAMS, seri mingguan NASA MERRA-2 PM2.5, dan NASA MODIS AOD.

2. **Filter Wilayah Administrasi Terpadu (14 Kabupaten/Kota)**
   - Pemilihan wilayah per Kabupaten/Kota otomatis mengarahkan tampilan peta (*fly-to bounds*), menyorot batas administrasi terpilih, serta menyaring seluruh layer aktif dan grafik statistik secara *real-time*.

3. **Kontrol Layer Terstruktur & Legenda Dinamis**
   - Panel kontrol layer dilengkapi pengelompokan *dropdown accordion* (*Fasilitas & Objek Vital*, *Gambut, Trajektori & Batas*, dan *Validasi Satelit & Reanalisis*) dengan penghitung layer aktif.
   - **Legenda Peta Dinamis** yang otomatis menyesuaikan simbol dan klasifikasi berdasarkan layer-layer yang sedang diaktifkan pengguna.

4. **Time-Slider Temporal Dua Tingkat**
   - **Mode Harian (1 Agustus – 31 Oktober 2026 + Proyeksi Forecast):** Memantau dinamika musiman dan fase puncak emisi karhutla.
   - **Mode Episode Puncak (72 Jam / Interval 6 Jam):** Simulasi resolusi tinggi pada episode kabut asap kritis (11–14 Oktober 2026).

5. **Kalkulator Paparan *On-The-Fly* (Turf.js)**
   - Menghitung luas area yang melewati ambang batas bahaya PM2.5, estimasi populasi terpapar, serta deteksi tumpang susun spasial (*spatial intersection*) secara langsung terhadap titik/poligon fasilitas pendidikan dan fasilitas kesehatan.

6. **Simulator Skenario Mitigasi (*What-If*) & Pembobotan AHP**
   - Simulasi dampak reduksi emisi hotspot (`0%–80%`) dan perubahan arah/kecepatan angin manual.
   - Penyesuaian bobot kriteria **Analytical Hierarchy Process (AHP)** secara interaktif beserta fitur unduh laporan **CSV** dan cetak laporan.

---

## Struktur Repositori

```text
webgis-karhutla-kalbar/
├── index.html                                  # Aplikasi utama WebGIS (HTML, CSS, JS)
├── README.md                                   # Dokumentasi proyek
├── Batas_KabKota_KalimantanBarat.geojson       # Batas administrasi 14 Kab/Kota Kalbar
├── CAMS_PM25.geojson                           # Data validasi konsentrasi PM2.5 CAMS
└── data_pjbl/
    ├── asap_pm25_harian_ispu.geojson           # Poligon sebaran PM2.5 harian model HYSPLIT
    ├── burned_area_modis_mcd64a1.geojson       # Poligon area terbakar (MODIS MCD64A1)
    ├── khg_gambut_kalbar.geojson               # Poligon Kesatuan Hidrologis Gambut (KHG)
    ├── hotspot/                                # Data titik api VIIRS 375m
    │   ├── hotspot_viirs_noaa20.geojson
    │   ├── hotspot_viirs_noaa21.geojson
    │   └── hotspot_viirs_snpp.geojson
    ├── layer_dampak/                           # Objek vital (Kesehatan, Pendidikan, Bandara)
    │   ├── airport_point.geojson
    │   ├── airport_polygon.geojson
    │   ├── airport_polyline.geojson
    │   ├── education_point.geojson
    │   ├── education_polygon.geojson
    │   ├── health_point.geojson
    │   └── health_polygon.geojson
    ├── merra2_mingguan/                        # Seri mingguan NASA MERRA-2 PM2.5
    └── MODIS_mingguan/                         # Seri mingguan NASA MODIS AOD
