# Gemini-Force

Kumpulan **skill file** untuk AI (Gemini, Claude, ChatGPT, dan model lain yang mendukung custom skill / system instruction) yang memaksa model bekerja dengan disiplin verifikasi ketat: tanpa basa-basi pembuka, tanpa data yang dipotong, tanpa sitasi karangan.

Repo ini punya dua lapis:

| Lapis | Isi | Fungsi |
|---|---|---|
| **Inti** | [`notebook-source-guide-v4.6.md`](notebook-source-guide-v4.6.md) | Mesin riset umum: verifikasi jurnal (Scopus Q1–Q2, SINTA 1–2), first-principles reasoning, three-layer source gating, dan audit metodologis. |
| **Split Force** | [`Gemini-split-force/`](Gemini-split-force) | Tiga modul spesialis yang memecah aturan inti ke domain terpisah, supaya gerbang verifikasi yang dimuat hanya yang relevan dengan tugas. |

---

## Kenapa dipecah (Split Force)?

Aturan akademik yang ketat bagus untuk literature review, tapi jadi friksi kalau dipakai untuk semua hal — misalnya AI diminta mengecek indeksasi SINTA saat kamu sedang memperbaiki bug Python, atau AI malah mencari ke internet padahal kamu ingin mengaudit satu PDF secara tertutup.

Split Force adalah **kotak perkakas bedah**: satu modul, satu tugas, satu gerbang verifikasi.

1. **Mencegah tabrakan aturan antar-domain.** Modul kode mengganti syarat bibliografi akademik dengan audit Big-O, keamanan memori, dan larangan placeholder kode.
2. **Isolasi konteks & hemat kuota token.** Memuat satu modul per sesi membuang instruksi tak relevan, sehingga model mengalokasikan seluruh memori dan token reasoning pada satu mekanisme penalaran.
3. **Pemisahan peran epistemik.** Tiap modul punya sikap berbeda terhadap kebenaran: mengunci diri pada dokumen, mengaudit sistem, atau menyerang argumen.

---

## Isi repo

```
Gemini-Force/
├── notebook-source-guide-v4.6.md          # skill inti (riset & verifikasi)
├── README.md                              # file ini
└── Gemini-split-force/
    ├── 01-closed-notebook-strict.md       # audit korpus tertutup
    ├── 02-code-systems-auditor.md         # audit kode & arsitektur sistem
    └── 03-red-team-demolisher.md          # penghancur argumen / anti-sycophancy
```

---

## Instalasi

### Instal seluruh repo

```
install https://github.com/ErlanggaDev-Studios/Gemini-Force
```

### Instal per skill (disarankan untuk Split Force)

Pasang hanya modul yang kamu butuhkan:

```
install https://github.com/ErlanggaDev-Studios/Gemini-Force/blob/main/Gemini-split-force/01-closed-notebook-strict.md
```

```
install https://github.com/ErlanggaDev-Studios/Gemini-Force/blob/main/Gemini-split-force/02-code-systems-auditor.md
```

```
install https://github.com/ErlanggaDev-Studios/Gemini-Force/blob/main/Gemini-split-force/03-red-team-demolisher.md
```

### Instal skill inti

```
install https://github.com/ErlanggaDev-Studios/Gemini-Force/blob/main/notebook-source-guide-v4.6.md
```

### Manual

Kalau platform AI-mu belum mendukung perintah `install`, cukup:

1. Buka file yang dituju di GitHub, klik **Raw**, lalu salin seluruh isinya.
2. Tempel sebagai system instruction / custom instruction / skill baru di aplikasimu (Gemini Gems, Claude Projects, ChatGPT Custom Instructions, dsb).
3. Simpan dengan nama yang sama seperti nama file agar trigger-nya mudah diingat.

---

## Cara memanggil

Tulis trigger di awal prompt. Semua trigger case-sensitive.

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

### Skill inti (`notebook-source-guide`)

Tidak memakai trigger pendek; aktif sebagai instruksi dasar dan mengenali mode `/Thesis`, `/Deep-think`, serta kombinasinya (`/Deep-think && /Thesis`) untuk sintesis akademik dan audit atribusi.

---

## Kapan pakai yang mana

| Kebutuhan | Skill |
|---|---|
| Riset literatur, verifikasi jurnal, tinjauan pustaka | `notebook-source-guide-v4.6.md` |
| Audit satu/beberapa dokumen tertutup, tanpa akses luar | `01-closed-notebook-strict.md` (`/cns`) |
| Review kode, performa, keamanan, desain sistem | `02-code-systems-auditor.md` (`/csa`) |
| Uji argumen, cari titik lemah tesis/rencana | `03-red-team-demolisher.md` (`/rtd`) |

Modul split bisa digabung dengan skill inti, tapi jangan mengaktifkan dua modul split sekaligus — justru tabrakan aturan yang ingin dihindari.

---

## Versi

- `notebook-source-guide` — v4.6
- `closed-notebook-strict` — v1.0
- `code-systems-auditor` — v1.0
- `red-team-demolisher` — v1.0

Semua skill memakai format frontmatter (`name`, `description`, `version`) agar terbaca oleh loader skill yang mendukung.
