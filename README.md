# Gemini-Force

Kumpulan **skill file** untuk AI (Gemini, Claude, ChatGPT, dan model lain yang mendukung custom skill / system instruction) yang memaksa model bekerja dengan disiplin verifikasi ketat: tanpa basa-basi pembuka, tanpa data yang dipotong, tanpa sitasi karangan.

Repo ini punya dua lapis:

| Lapis | Isi | Fungsi |
|---|---|---|
| **Inti** | [`notebook-source-guide-v4.6.md`](notebook-source-guide-v4.6.md) | Mesin riset umum: verifikasi jurnal (Scopus Q1–Q2, SINTA 1–2), first-principles reasoning, three-layer source gating, dan audit metodologis. |
| **Split Force** | [`Gemini-split-force/`](Gemini-split-force) | Tujuh modul spesialis yang memecah aturan inti ke domain terpisah, supaya gerbang verifikasi yang dimuat hanya yang relevan dengan tugas. |

---

## Kenapa dipecah (Split Force)?

Aturan akademik yang ketat bagus untuk literature review, tapi jadi friksi kalau dipakai untuk semua hal — misalnya AI diminta mengecek indeksasi SINTA saat kamu sedang memperbaiki bug Python, atau AI malah mencari ke internet padahal kamu ingin mengaudit satu PDF secara tertutup.

Split Force adalah **kotak perkakas bedah**: satu modul, satu tugas, satu gerbang verifikasi.

1. **Mencegah tabrakan aturan antar-domain.** Modul kode mengganti syarat bibliografi akademik dengan audit Big-O, keamanan memori, dan larangan placeholder kode.
2. **Isolasi konteks & hemat kuota token.** Memuat satu modul per sesi membuang instruksi tak relevan, sehingga model mengalokasikan seluruh memori dan token reasoning pada satu mekanisme penalaran.
3. **Pemisahan peran epistemik.** Tiap modul punya sikap berbeda terhadap kebenaran: mengunci diri pada dokumen, mengaudit sistem, menyerang argumen, merekonsiliasi angka, atau menulis dari bukti — bukan empat sikap yang sama dengan label berbeda.

---

## Isi repo

```
Gemini-Force/
├── notebook-source-guide-v4.6.md          # skill inti (riset & verifikasi)
├── README.md                              # file ini
└── Gemini-split-force/
    ├── 00-skill-router.md                 # router otomatis: deteksi intensi → modul
    ├── 01-closed-notebook-strict.md       # audit korpus tertutup
    ├── 02-code-systems-auditor.md         # audit kode & arsitektur sistem
    ├── 03-red-team-demolisher.md          # penghancur argumen / anti-sycophancy
    ├── 04-data-statistics-auditor.md      # rekonsiliasi angka & validitas inferensi
    ├── 05-academic-prose-compiler.md      # penulis prosa akademik berbasis bukti
    └── 06-skill-registry.md               # indeks skill terpasang + fungsi singkat
```

---

## Instalasi

Gunakan **link raw**, bukan link halaman GitHub. Kebanyakan AI konvensional tidak bisa membaca halaman `github.com/.../blob/...` (HTML penuh menu dan JavaScript), tapi bisa mengambil file mentah dari `raw.githubusercontent.com` sebagai teks biasa.

### Instal seluruh repo

```
install https://github.com/ErlanggaDev-Studios/Gemini-Force
```

### Instal per skill (disarankan untuk Split Force)

Pasang hanya modul yang kamu butuhkan. Salin link raw sesuai kebutuhan:

| Skill | Link raw yang dipasang |
|---|---|
| Skill inti | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/notebook-source-guide-v4.6.md` |
| 00 Skill Router | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/00-skill-router.md` |
| 01 Closed-Notebook | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/01-closed-notebook-strict.md` |
| 02 Code & Systems | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/02-code-systems-auditor.md` |
| 03 Red-Team | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/03-red-team-demolisher.md` |
| 04 Data & Statistics | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/04-data-statistics-auditor.md` |
| 05 Academic Prose | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/05-academic-prose-compiler.md` |
| 06 Skill Registry | `https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/06-skill-registry.md` |

Perintah pasang siap salin:

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/notebook-source-guide-v4.6.md
```

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/00-skill-router.md
```

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/01-closed-notebook-strict.md
```

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/02-code-systems-auditor.md
```

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/03-red-team-demolisher.md
```

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/04-data-statistics-auditor.md
```

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/05-academic-prose-compiler.md
```

```
install https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/06-skill-registry.md
```

### Semua link raw dalam satu blok

Kalau tidak mau menyalin satu per satu, salin satu blok di bawah ini (satu URL per baris) dan kirim apa adanya:

```
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/notebook-source-guide-v4.6.md
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/00-skill-router.md
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/01-closed-notebook-strict.md
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/02-code-systems-auditor.md
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/03-red-team-demolisher.md
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/04-data-statistics-auditor.md
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/05-academic-prose-compiler.md
https://raw.githubusercontent.com/ErlanggaDev-Studios/Gemini-Force/refs/heads/main/Gemini-split-force/06-skill-registry.md
```

Semua file bisa dipasang sekaligus dengan mengirim kedelapan link raw di atas dalam satu pesan.

### Kalau platform-mu bisa membaca GitHub

Link halaman biasa tetap berfungsi untuk AI yang punya akses browsing:

```
install https://github.com/ErlanggaDev-Studios/Gemini-Force/blob/main/Gemini-split-force/01-closed-notebook-strict.md
```

### Manual

Kalau platform AI-mu belum mendukung perintah `install`, cukup:

1. Buka file yang dituju di GitHub, klik **Raw**, lalu salin seluruh isinya.
2. Tempel sebagai system instruction / custom instruction / skill baru di aplikasimu (Gemini Gems, Claude Projects, ChatGPT Custom Instructions, dsb).
3. Simpan dengan nama yang sama seperti nama file agar trigger-nya mudah diingat.

---

## Cara memanggil

Tulis trigger di awal prompt. **Kapital tidak berpengaruh:** `/extract`, `/Extract`, dan `/EXTRACT` memicu hal yang sama, begitu juga `/c-audit` dan `/C-audit`. Bentuk berkapital di tabel bawah adalah nama tampilan kanonisnya, bukan syarat penulisan.

### 00 — Skill Router (otomatis, tanpa perintah)

**Zero-command:** cukup pasang file ini sekali, tidak ada perintah untuk mengaktifkannya. Setiap pesan yang kamu kirim lewat alur yang sama: `input → AI berpikir → membuka skill 00 → memutuskan perlu modul atau tidak, dan modul apa → proses → output`. Router menilai dulu apakah pertanyaan memang butuh protokol berat: obrolan ringan dan definisi satu kalimat dijawab langsung (Bypass) supaya token tidak habis untuk aturan yang tidak dipakai. Kalau perlu, ia memetakan intensi ke modul yang tepat — dokumen tertutup ke `01`, kode ke `02`, argumen ke `03`, angka ke `04`, catatan jadi prosa ke `05`, tinjauan literatur ke skill inti — dan merangkai dua modul berurutan kalau satu pertanyaan membawa dua intensi (misalnya `04` lalu `05`, atau `02` lalu `03`).

| Perintah | Fungsi |
|---|---|
| _(tanpa perintah)_ | Aktif sejak dipasang; semua pesan dirutekan otomatis ke modul yang tepat |
| `/Matrix` | Cetak tabel ambang batas + pemetaan intensi dan modul yang dipilih, tanpa menjalankannya |
| `/Chain` | Cetak rencana rantai dua modul berurutan, lalu langsung jalankan langkah pertama |

Cocok untuk: dipasang sebagai satu-satunya modul, lalu biarkan ia yang memanggil sisanya. `/route` tidak diperlukan — menuliskannya tidak mengubah apa pun karena router sudah berjalan. Dua mode diagnostik di atas tetap tidak peka kapital: `/matrix` dan `/chain` sama sahnya dengan bentuk berkapital.

### 01 — Closed-Notebook Strict (`/cns`)

AI hanya bicara berdasarkan dokumen yang kamu unggah. Tidak ada internet, tidak ada memori luar. Setiap klaim wajib punya jangkar lokasi (`[Sumber, Bagian, Halaman X, Tabel Y, Catatan Kaki Z]`), dan data yang tidak ada di dokumen dijawab `[NOT IN CORPUS]`.

| Perintah | Fungsi |
|---|---|
| `/cns` | Aktifkan skill; jawaban langsung terikat korpus yang diunggah |
| `/C-audit` | Sintesis multi-dokumen: bandingkan metodologi, temukan kontradiksi antar-file |
| `/Extract` | Ekstraksi penuh tanpa potong: semua tabel, persamaan, definisi, footnote |

Cocok untuk: audit kontrak, naskah sensitif, NotebookLM, telaah PDF tertutup.

### 02 — Code & Systems Auditor (`/csa`)

Mengubah AI menjadi auditor arsitektur perangkat lunak: menolak kode malas/terpotong, menurunkan kompleksitas Big-O secara eksplisit, dan menekan kasus tepi (null, overflow, race condition, deadlock).

| Perintah | Fungsi |
|---|---|
| `/csa` | Aktifkan skill; diagnosis akar masalah + implementasi utuh |
| `/Audit` | Audit baris-per-baris: kerentanan, konkurensi, memori, edge case |
| `/Architect` | Desain sistem dari batasan hardware/jaringan & modus kegagalan, sebelum menulis kode |

Cocok untuk: code review, refactor, desain sistem, analisis performa.

### 03 — Red-Team Demolisher (`/rtd`)

Mematikan sifat bawaan AI yang suka memuji pengguna. Setiap tesis, hipotesis, atau rencana dianggap bersalah sampai lolos pembongkaran formal: premis tersembunyi, titik hancur asimtotik, dan backfire orde kedua (Goodhart's Law).

| Perintah | Fungsi |
|---|---|
| `/rtd` | Aktifkan skill; teardown adversarial empat tahap |
| `/Demolish` | (default) Bongkar total: logika, empiris, konsekuensi orde kedua |
| `/Steelman` | Bangun versi terkuat argumen dulu, baru dibongkar sistematis |

Cocok untuk: uji proposal tesis, validasi strategi, debat, pra-mortem proyek.

### 04 — Data & Statistics Auditor (`/dsta`)

Auditor angka: tidak menilai narasi, hanya menilai koherensi data. Menghitung ulang total, subgroup, dan persentase; memeriksa unit dan tahun dasar; lalu mengaudit validitas inferensinya (pilihan uji, multiple comparisons, effect size vs p-value, Simpson's paradox, power subgroup). Angka yang mustahil diberi verdict eksplisit, bukan diperbaiki diam-diam.

| Perintah | Fungsi |
|---|---|
| `/dsta` | Aktifkan skill; audit aritmetika & konsistensi angka yang dikirim |
| `/Reconcile` | Ledger penuh: total, subtotal, denominator, persentase, baris turunan |
| `/Inference` | Audit validitas inferensi: desain, uji, multiplisitas, effect size, power |

Cocok untuk: tabel hasil regresi, data BPS/survei, grafik laporan, bab hasil tesis.

### 05 — Academic Prose Compiler (`/apc`)

Satu-satunya modul yang **menulis**, bukan mengaudit. Mengubah catatan dan temuan terverifikasi menjadi prosa akademik siap tempel: heading, topic sentence, transisi, terminologi terkunci, dan sitasi yang hanya boleh merujuk entri sumber yang benar-benar kamu berikan. Sitasi yang tidak ada di daftar dijawab `[CITATION NEEDED]`, bukan dikarang.

| Perintah | Fungsi |
|---|---|
| `/apc` | Aktifkan skill; kompilasi paragraf/bagian dari catatan yang ada |
| `/Compile` | Bagian utuh dengan hierarki heading + claim–source map |
| `/Tighten` | Rapikan draft yang sudah ada: register, kohesi, konsistensi istilah — tanpa klaim baru |
| `/Abstract` | Ringkas ke abstrak/intisari dengan batas kata yang dinyatakan |

Cocok untuk: menulis bab tinjauan pustaka, abstrak, diskusi, dan naskah jurnal ID/EN.

### 06 — Skill Registry (`/skills`)

Indeks skill yang terpasang. Mencetak satu baris per skill dalam bentuk `/trigger → fungsi singkat`, dan hanya menyebut skill yang definisinya benar-benar ada di sesi — skill yang cuma terdokumentasi diberi label `[DOCUMENTED]`, yang tidak ditemukan `[UNKNOWN SKILL]`, bukan dikarang dari ingatan.

| Perintah | Fungsi |
|---|---|
| `/skills` | Daftar panah ringkas: trigger + fungsi satu baris per skill |
| `/Map` | Tabel penuh: trigger, full form, file sumber, versi, dan mode tiap skill |
| `/Verify` | Audit saja: skill mana yang termuat, trigger bentrok, dan versi yang tidak sinkron |

Cocok untuk: membuka sesi baru, memastikan modul mana yang sudah aktif, dan mendeteksi trigger yang saling menimpa sebelum dipakai. Pemanggilannya juga tidak peka kapital: `/skills`, `/Skills`, `/map`, dan `/verify` semuanya sah.

### Skill inti (`notebook-source-guide`)

Tidak memakai trigger pendek; aktif sebagai instruksi dasar dan mengenali mode `/Thesis`, `/Deep-think`, serta kombinasinya (`/Deep-think && /Thesis`) untuk sintesis akademik dan audit atribusi.

---

## Kapan pakai yang mana

| Kebutuhan | Skill |
|---|---|
| Tidak mau memilih modul sendiri; ingin dirutekan otomatis tanpa perintah | `00-skill-router.md` (aktif sendiri) |
| Riset literatur, verifikasi jurnal, tinjauan pustaka | `notebook-source-guide-v4.6.md` |
| Audit satu/beberapa dokumen tertutup, tanpa akses luar | `01-closed-notebook-strict.md` (`/cns`) |
| Review kode, performa, keamanan, desain sistem | `02-code-systems-auditor.md` (`/csa`) |
| Uji argumen, cari titik lemah tesis/rencana | `03-red-team-demolisher.md` (`/rtd`) |
| Cek konsistensi tabel/angka, audit statistik & inferensi | `04-data-statistics-auditor.md` (`/dsta`) |
| Menulis bab/abstrak dari catatan yang sudah terverifikasi | `05-academic-prose-compiler.md` (`/apc`) |
| Mencetak daftar skill terpasang beserta fungsi singkatnya | `06-skill-registry.md` (`/skills`) |

Modul split bisa digabung dengan skill inti, tapi jangan mengaktifkan dua modul split sekaligus — berurutan boleh (lihat `/Chain` di `00-skill-router.md`), bersamaan tidak, karena justru tabrakan aturan yang ingin dihindari.

---

## Versi

- `notebook-source-guide` — v4.6
- `skill-router` — v1.1 (zero-command)
- `closed-notebook-strict` — v1.0
- `code-systems-auditor` — v1.0
- `red-team-demolisher` — v1.0
- `data-statistics-auditor` — v1.0
- `academic-prose-compiler` — v1.0
- `skill-registry` — v1.0

Semua skill memakai format frontmatter (`name`, `description`, `version`) agar terbaca oleh loader skill yang mendukung.
