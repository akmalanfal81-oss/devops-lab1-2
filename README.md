# Laporan Praktikum Modul 1: Kontainerisasi Docker & Orkestrasi Multi-Tier

- **Nama Mahasiswa**: Akmal
- **NIM**: 42430041
- **Kelas / Prodi**: S1 Teknologi Informasi – UNDIKNAS Denpasar
- **Tautan Branch / PR GitHub**: [Isi URL Branch/PR kamu]
- **Nama Rekan Peer-Reviewer**: [Isi Nama & NIM temanmu]

## 1. Tabel Komparasi Eksperimen Individu

| Parameter Pembanding | Tahap 1: Tanpa Docker | Tahap 2: Docker Single-Stage | Tahap 3: Docker Multi-Stage |
| :--- | :--- | :--- | :--- |
| **Kebutuhan Instalasi Go di Host** | Wajib | Tidak wajib | Tidak wajib |
| **Ukuran Image** | *Tidak ada* | ~840 MB | **~16 MB** (Target < 100MB) |
| **Output `container_or_host_id`** | Hostname: `LAPTOP-T4V0501E` | Container ID | Container ID |
| **User Eksekusi Proses (`id`)** | User laptop | `uid=0 (root)` | `uid=10001 (appuser)` |
| **Menjalankan 2 Instansi** | Gagal (port bentrok) | Berhasil (`-p 8081` & `8082`) | Berhasil |

## 2. Bukti Screenshot & Penjelasan Analisis

### A. Tahap 1 – Eksekusi Tanpa Docker
![SC-01](docs/screenshots/sc01-tahap1-tanpa-docker.png)
* **Penjelasan**: [Jelaskan mengapa hostname muncul nama laptop, dan mengapa error `bind: address already in use` terjadi.]

### B. Tahap 2 – Docker Single-Stage
![SC-02](docs/screenshots/sc02-tahap2-single-stage.png)
* **Penjelasan**: [Jelaskan mengapa ukuran image membengkak >800MB, dan bagaimana Docker membuat 2 kontainer bisa jalan bersamaan.]

### C. Tahap 3 – Multi-Stage Build
![SC-03](docs/screenshots/sc03-tahap3-multistage.png)
* **Penjelasan**: [Hitung persentase penurunan ukuran image. Jelaskan fungsi `COPY --from=builder` dan alasan keamanan menggunakan `USER appuser`.]

### D. Tahap 4 – Orkestrasi Multi-Tier & Persistensi
![SC-04](docs/screenshots/sc04-tahap4-compose-persistensi.png)
* **Penjelasan**: [Jelaskan bagaimana Named Volume `pgdata` menjaga data tetap aman walaupun kontainer dihapus, dan bagaimana frontend/backend/db saling terhubung tanpa membuka port 5432 ke publik.]

### E. Tahap 5 – Troubleshooting
![SC-05](docs/screenshots/sc05-tahap5-troubleshooting.png)
* **Penjelasan**: [Jelaskan mengapa `DB_HOST=localhost` menyebabkan error, dan bahaya perintah `docker compose down -v`.]

### F. Tantangan Mandiri
![SC-06](docs/screenshots/sc06-tantangan-mandiri.png)
* **Penjelasan**: [Jelaskan mengapa `ping db` dari frontend gagal (bad address), dan bagaimana file `.env` melindungi password dari GitHub.]

## 3. Bukti Audit Silang (Peer-Review)
- **Tautan Pull Request (PR)**: [URL PR Kamu]
- **Ringkasan Catatan Peer-Reviewer**: [Tulis hasil review dari temanmu]# devops-lab1-2
