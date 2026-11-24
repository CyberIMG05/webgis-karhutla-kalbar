# SDSS Mitigasi & Peringatan Dini Karhutla — Provinsi Kalimantan Barat

**Spatial Decision Support System (SDSS)** berbasis WebGIS untuk pemantauan kejadian kebakaran hutan dan lahan (karhutla), simulasi dispersi polutan PM2.5, serta analisis dampak paparan terhadap penduduk dan fasilitas vital di Provinsi Kalimantan Barat (periode kajian Agustus – Oktober 2026).

🌐 **Live Demo:** [https://cyberimg05.github.io/webgis-karhutla-kalbar/](https://cyberimg05.github.io/webgis-karhutla-kalbar/)

---

## Fitur Utama

1. **Manajemen Layer Spasial Multi-Sumber**
   - **Titik Api & FRP (VIIRS 375 m):** Gabungan deteksi sensor NOAA-20, NOAA-21, dan Suomi-NPP yang tersaring otomatis mengikuti tanggal aktif pada *time-slider*.
   - **Area Terbakar (*Burned Area*):** Poligon bekas area terbakar dari produk NASA MODIS MCD64A1 v061.
   - **Sebaran Asap & Lintasan Partikel:** Simulasi dispersi konsentrasi PM2.5 berbasis kategori ISPU, lintasan partikel HYSPLIT (20 m, 500 m, dan 1.000 m AMSL), serta visualisasi aliran angin dinamis (*streamlines*).
   - **Objek Vital Terdampak:** Pemetaan terpisah untuk **Fasilitas Kesehatan**, **Fasilitas Pendidikan**, serta **Bandara & Helipad** (titik, poligon area, dan garis landasan pacu).
   - **Validasi Satelit & Reanalisis:** Layer validasi PM2.5 (CAMS), seri mingguan NASA MERRA-2 PM2.5, dan NASA MODIS AOD.

2. **Time-Slider Temporal Dua Tingkat**
   - **Mode Harian (1 Agustus – 31 Oktober 2026 + Proyeksi Forecast):** Memantau dinamika musiman dan puncak emisi karhutla.
   - **Mode Episode Puncak (72 Jam / Interval 6 Jam):** Simulasi resolusi tinggi pada episode kabut asap kritis (11–14 Oktober 2026).

3. **Kalkulator Paparan *On-The-Fly***
   - Menghitung estimasi populasi terpapar, fasilitas sensitif terdampak, serta grafik perbandingan konsentrasi PM2.5 antar-kabupaten/kota secara *real-time* berdasarkan ambang batas bahaya yang diatur pengguna.

4. **Simulator Skenario Mitigasi (*What-If*) & Pembobotan AHP**
   - Simulasi dampak reduksi emisi hotspot (0%–80%) dan perubahan arah/kecepatan angin manual.
   - Penyesuaian bobot parameter **Analytical Hierarchy Process (AHP)** (Konsentrasi PM2.5, Kepadatan Penduduk, Fasilitas Sensitif, dan Durasi Paparan) secara interaktif.

5. **Ekspor Data & Pelaporan**
   - Unduh rekapitulasi hasil simulasi dalam format **CSV** serta fitur cetak laporan langsung dari peramban.

---

## Struktur Repositori

```text
webgis-karhutla-kalbar/
├── index.html                                  # Aplikasi utama WebGIS (HTML, CSS, JS)
├── Batas_KabKota_KalimantanBarat.geojson       # Batas administrasi Kabupaten/Kota Kalbar
├── CAMS_PM25.geojson                           # Data validasi konsentrasi PM2.5 CAMS
└── data_pjbl/
    ├── burned_area_modis_mcd64a1.geojson       # Poligon area terbakar (MODIS MCD64A1)
    ├── hotspot/                                # Data titik api VIIRS (NOAA-20, NOAA-21, S-NPP)
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
