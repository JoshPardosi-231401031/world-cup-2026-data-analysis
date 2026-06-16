# World Cup 2026 Data Analysis & Tournament Simulation

Repository ini berisi simulasi *end-to-end* turnamen sepak bola menggunakan **PostgreSQL**. Proyek ini dirancang untuk menunjukkan kemampuan manipulasi data (*Data Manipulation*), perancangan logika database (*Schema Evolution*), hingga analisis *pipeline* turnamen yang kompleks secara modular.

---

## 🚀 Tech Stack
* **Database Management:** PostgreSQL (DBeaver)

---

## 📁 Struktur Pipeline SQL
Proyek ini dipecah secara modular menjadi 3 tahap utama agar alur pengerjaan data terlihat jelas:

1. **`01_data_preparation.sql`**
   * Pembuatan skema tabel awal `matches` menggunakan format netral (`team_1`, `team_2`, `score_1`, `score_2`).
   * *Data entry* untuk 12 pertandingan awal yang dibagi secara merata ke dalam Grup A, B, dan C.

2. **`02_group_stage.sql`**
   * Melengkapi data jadwal turnamen (Matchday 3) menggunakan perintah `INSERT INTO` hingga genap 18 pertandingan (6 laga per grup).
   * Perhitungan klasemen grup otomatis menggunakan logika poin sepak bola (Menang = 3, Seri = 1, Kalah = 0).
   * Penyaringan otomatis menggunakan *Window Function* untuk mengambil hanya peringkat 1 dan 2 dari masing-masing grup.

3. **`03_knockout_stage.sql`**
   * Evolusi skema dengan membuat tabel baru `knockout_matches` yang mendukung pencatatan skor adu penalti.
   * Penerapan sistem babak gugur dan penentuan juara utama menggunakan metode liga mini (*Round-Robin*) adil untuk 3 tim terbaik (Juara Akhir: **Netherlands** 🏆).

---

## 💡 Fitur Advanced SQL yang Digunakan
* **Common Table Expressions (CTE):** Menggunakan `WITH ... AS` berlapis untuk membungkus kueri sementara agar logika kode lebih modular dan mudah dibaca.
* **Window Functions:** Memanfaatkan `RANK() OVER (PARTITION BY grup ORDER BY ...)` untuk mereset dan menghitung peringkat tim secara dinamis di dalam grupnya masing-masing.
* **Conditional Logic:** Implementasi `CASE WHEN` untuk kalkulasi poin otomatis berdasarkan perbandingan skor pertandingan.
* **Set Operators:** Menggunakan `UNION ALL` untuk menggabungkan data statistik dari sudut pandang `team_1` dan `team_2` ke dalam satu kolom agregasi yang sama.
* **Data Definition & Manipulation:** Menguasai penggunaan `ALTER TABLE`, `UPDATE`, dan `TRUNCATE TABLE` untuk menjaga integritas data selama proses simulasi.
