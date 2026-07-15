# AI-200 Study Repository — Developing AI Cloud Solutions on Azure

> Exam: **AI-200: Developing AI Cloud Solutions on Azure**
> Sertifikasi: **Microsoft Certified: Azure AI Cloud Developer Associate**
> Lifecycle status exam per audit terakhir: **Transitional/Unresolved** — ini status siklus hidup (beta vs GA), **bukan** indikasi exam tidak tersedia; ketersediaan operasional dicatat terpisah (lihat [Audit Terkini](#0-audit-terkini))
> Tanggal audit: **2026-07-15** (revisi pasca review eksternal: 2026-07-15)
> Bahasa repositori: narasi dalam Bahasa Indonesia; istilah teknis, nama layanan, dan judul domain dipertahankan dalam English sesuai terminologi Microsoft.

Repositori ini adalah kurikulum belajar mandiri untuk exam AI-200. Semua klaim faktual penting merujuk ke **source ID** pada [Source Ledger](#9-source-ledger). Bagian yang berupa interpretasi teknis, rekomendasi belajar, atau inferensi diberi label eksplisit.

**Catatan metodologi verifikasi (penting).** Audit ini dijalankan dari environment yang aksesnya ke `learn.microsoft.com` via HTTP langsung diblokir oleh kebijakan jaringan, sehingga verifikasi dilakukan melalui Microsoft Learn MCP tools resmi (konversi markdown). Konsekuensinya: (1) `<title>` browser, tanggal "Last updated" yang dirender visual, dan banner yang diinjeksi client-side pada beberapa halaman **tidak dapat diperiksa**; (2) bagian halaman sertifikasi yang dirender client-side (daftar exam, bahasa, durasi, harga, tombol jadwal) **tidak dapat diverifikasi** dan dicatat sebagai `Needs Review`; (3) `techcommunity.microsoft.com` tidak dapat diakses sama sekali dari environment ini (HTTP 403). Keterbatasan ini dicatat jujur di setiap baris audit dan ledger — "Not shown" berarti *tidak dapat diambil oleh tool*, bukan *terbukti tidak ada*.

**Catatan revisi 2026-07-15 (review eksternal).** Sebuah review eksternal (non-Microsoft) melaporkan bahwa halaman resmi kini menampilkan beberapa nilai pada bagian yang dirender client-side: bahasa exam **English**, assessment time **120 minutes**, scheduling tersedia melalui Pearson VUE, dan study guide **Last updated: May 5, 2026**. Sesuai kebijakan sumber (Microsoft only, halaman harus dibuka), nilai-nilai ini **tidak diadopsi sebagai fakta terverifikasi** sampai dapat dikonfirmasi langsung dari halaman resmi — baris audit terkait mencantumkannya sebagai *laporan eksternal, belum terverifikasi*. Perbaikan struktural dari review yang sama (pemisahan lifecycle vs operational availability, penajaman narasi Practice Assessment, guardrail Service Bus, prinsip security/observability lintas-modul, kolom Source readiness) **sudah diterapkan**.

---

## 0. Audit Terkini

Semua pemeriksaan dilakukan **2026-07-15** dengan membuka halaman (bukan snippet mesin pencari), sesuai protokol verifikasi.

| Item | Hasil terbaru | Bukti utama | Bukti pendukung/konflik | Confidence | Tanggal cek | Source ID | Perubahan dari baseline |
|---|---|---|---|---|---|---|---|
| Lifecycle status exam (beta/live/GA) | **Transitional/Unresolved** — status siklus hidup, bukan indikasi ketersediaan operasional | Tidak ditemukan pernyataan resmi eksplisit bertanggal bahwa AI-200 sudah "gone live"/GA; halaman sertifikasi memuat frasa "…within 8 weeks of the exam being out of beta and generally available" pada catatan Practice Assessment | Metadata indeks pencarian Learn masih memiliki varian judul halaman "…(beta)"; bagian detail exam di halaman sertifikasi dirender client-side sehingga ada/tidaknya sufiks "(beta)" pada nama exam tidak dapat diperiksa; blog pengumuman resmi tidak dapat diakses dari environment ini | Medium | 2026-07-15 | SRC-001, SRC-020, SRC-021 | Baseline mengantisipasi transisi; hasil audit mengonfirmasi belum ada bukti resolusi biner |
| Practice Assessment AI-200 | Tidak tersedia; AI-200 **tidak terdaftar** pada daftar resmi Practice Assessments (46 entri) | Halaman sertifikasi: "The Practice Assessment for this exam is not currently available." | Daftar Practice Assessments tidak memuat AI-200 (AZ-204 masih terdaftar). Sesuai protokol: **sinyal pendukung, bukan penentu status** | High | 2026-07-15 | SRC-001, SRC-015 | Sesuai baseline |
| Scheduling via Pearson VUE (operational availability) | Surface scheduling resmi (`schedule-through-pearson-vue?examUid=exam.AI-200`) ada, tetapi kontennya dinamis + sign-in gated sehingga schedulability AI-200 **tidak dapat diverifikasi langsung dari environment ini**. Review eksternal (non-Microsoft) melaporkan exam **dapat dijadwalkan** melalui Pearson VUE — *belum terverifikasi dari halaman resmi yang dibuka* | Halaman scheduling tidak mengembalikan konten statis; halaman "Register and schedule an exam" mendeskripsikan surface ini dan Pearson VUE sebagai provider | Sesuai protokol: scheduling bukan bukti GA | Low | 2026-07-15 | SRC-016, SRC-017 | Baseline tidak dapat dikonfirmasi ulang secara langsung; laporan eksternal menunggu konfirmasi |
| Bahasa exam | **BELUM DAPAT DIVERIFIKASI DARI SUMBER RESMI MICROSOFT** oleh environment ini (bagian bahasa pada halaman exam dirender client-side). Review eksternal melaporkan **English** — konsisten dengan baseline, *belum terverifikasi dari halaman resmi yang dibuka* | Halaman sertifikasi tidak menampilkan bagian bahasa pada konten yang dapat diambil | Study guide hanya memuat pernyataan generik tentang lokalisasi exam dan tambahan 30 menit bila exam tidak tersedia dalam bahasa pilihan | Low | 2026-07-15 | SRC-001, SRC-002 | Baseline "English" tidak terkonfirmasi ulang → `Needs Review`; laporan eksternal menunggu konfirmasi |
| Assessment time AI-200 | **BELUM DAPAT DIVERIFIKASI** pada halaman AI-200 oleh environment ini (dinamis). Kebijakan umum: associate role-based tanpa lab = 100 menit exam / 120 menit seat; yang dapat memuat lab = 120 / 140. Review eksternal melaporkan **120 minutes** — konsisten dengan baseline, *belum terverifikasi dari halaman resmi yang dibuka* | Tabel "Exam duration and exam experience" | Baseline menyebut "120 minutes" pada halaman AI-200 — tidak dapat dikonfirmasi ulang. Catatan interpretatif: 120 menit pada tabel kebijakan berkorespondensi dengan kategori "may contain labs" — jangan disimpulkan lebih jauh tanpa konfirmasi halaman | Low (untuk angka AI-200 spesifik); High (untuk tabel kebijakan umum) | 2026-07-15 | SRC-007 | `Needs Review`; laporan eksternal menunggu konfirmasi |
| Delivery & proctoring | Exam Microsoft role-based dijadwalkan melalui **Pearson VUE**; tersedia online proctored (webcam + microphone, room scan, ID) atau test center | FAQ online proctored exams; halaman register-schedule-exam | — | High (kebijakan umum); penerapan spesifik AI-200 adalah **interpretasi wajar** (AI-200 adalah role-based exam) | 2026-07-15 | SRC-012, SRC-017 | Sesuai baseline |
| Interactive components/lab | **Tidak diklaim.** Kebijakan resmi: Microsoft tidak menerbitkan daftar exam yang memiliki lab; lab "can be removed at any time" | Halaman exam duration: footnote lab | Wording spesifik AI-200 tidak dapat diperiksa (dinamis) | High (untuk kebijakan); N/A untuk AI-200 spesifik | 2026-07-15 | SRC-007 | Sesuai baseline (tidak mengklaim lab) |
| Passing score | **Scaled score 700 atau lebih pada skala 1–1.000**; secara eksplisit BUKAN persentase jawaban benar ("it may not equal 70% of the points") | Halaman exam scoring | Study guide AI-200: "A score of 700 or greater is required to pass." | High | 2026-07-15 | SRC-008, SRC-002 | Sesuai baseline |
| Score availability | Live exam: hasil "within minutes", masuk Learn profile ≤24 jam (lab +~30 menit). Beta: skor TIDAK langsung — keluar ~10 hari setelah exam "goes live" (10–12 minggu setelah beta mulai; bisa sampai 14 minggu) | Halaman exam scoring; halaman about beta exams | — | High | 2026-07-15 | SRC-008, SRC-010 | Sesuai baseline |
| Retake policy | Umum: gagal pertama → tunggu 24 jam; berikutnya 14 hari; maksimum 5 attempt per 12 bulan. **Beta: hanya boleh 1× selama periode beta**; retake setelah exam live | Halaman retake policy | "This policy supersedes the general retake policy" (aturan beta) | High | 2026-07-15 | SRC-009 | Sesuai baseline |
| Study guide: domain & bobot | **Cocok dengan baseline** — 4 domain, bobot sama (lihat [Peta Domain](#4-peta-domain-dan-modul)) | Study guide AI-200 (dibuka penuh) | Variasi minor judul Domain 4: "Skills at a glance" menulis "Secure, monitor, troubleshoot…", heading rinci menulis "Secure, monitor, and troubleshoot…" | High | 2026-07-15 | SRC-002 | Tidak ada perubahan |
| Study guide: last updated | **Not shown** — tidak ada tanggal/change log pada konten yang dapat diambil oleh environment ini. Review eksternal melaporkan **May 5, 2026** — *belum terverifikasi dari halaman resmi yang dibuka* | Study guide AI-200 | Study guide AZ-204 (pembanding) menampilkan "Skills measured as of January 14, 2026" | Medium | 2026-07-15 | SRC-002, SRC-005 | `Needs Review`; laporan eksternal menunggu konfirmasi |
| AI-200 sebagai replacement path AZ-204 | **BELUM DAPAT DIVERIFIKASI DARI SUMBER RESMI MICROSOFT yang dapat diakses.** Halaman AZ-204 TIDAK menyebut AI-200/Azure AI Cloud Developer Associate sebagai pengganti; banner retirement hanya menaut ke blog Tech Community yang tidak dapat diakses dari environment ini | Halaman Azure Developer Associate (banner + "Learn more" → blog 4494128) | Kaitan tidak langsung: study guide AI-200 menaut ke halaman exam AZ-204 pada baris "Get trained" | Low | 2026-07-15 | SRC-004, SRC-021, SRC-002 | Baseline tidak terkonfirmasi ulang → `Needs Review` |
| Status AZ-204 | **Masih aktif; retire 31 Juli 2026.** Banner (exact): "This certification, related exam, and renewal assessments will retire on July 31, 2026." Study guide AZ-204: retire "July 31, 2026, at 11:59 PM Central Standard Time" | Halaman Azure Developer Associate (Last Updated 01/14/2026); daftar exam retirement (baris "AZ-204 … July 31, 2026") | Tanggal eksekusi (2026-07-15) < tanggal retirement → AZ-204 masih dapat diambil | High | 2026-07-15 | SRC-004, SRC-005, SRC-006 | Sesuai baseline; kini ~2 minggu sebelum retirement |
| AI-200 pada daftar retirement | AI-200 **tidak terdaftar** pada halaman exam retirement (baik scheduled maupun recently retired) | Halaman exam retirement | Catatan: AI-102 (exam berbeda) tercatat retired 30 Juni 2026 | High | 2026-07-15 | SRC-006 | Informasi baru (konteks) |
| Renewal | Kebijakan umum terverifikasi: sertifikasi associate diperpanjang **gratis** via online assessment (unproctored, open book) di Microsoft Learn; jendela eligibility **6 bulan** sebelum expiry; perpanjangan +1 tahun | Halaman renewal | Baris "Renewal Frequency" pada halaman AI-200 tidak tampak pada konten yang dapat diambil (dinamis) → penerapan spesifik AI-200 `Needs Review` | High (kebijakan umum); Low (tampilan di halaman AI-200) | 2026-07-15 | SRC-014, SRC-001 | Sesuai baseline |
| Akses Microsoft Learn saat exam | Terverifikasi untuk role-based exams: "You can access Microsoft Learn as you complete your associate or expert exam" — kecuali Q&A, Practice Assessments, dan profil; timer terus berjalan | Halaman exam duration & experience | Penerapan ke AI-200 = **interpretasi wajar** (AI-200 role-based associate), bukan pernyataan spesifik per-exam | High (kebijakan); Medium (penerapan AI-200) | 2026-07-15 | SRC-007 | Sesuai baseline |
| Course AI-200T00-A | Terverifikasi: "Course AI-200T00-A: Develop AI cloud solutions on Azure", 5 hari, Intermediate, 12 bahasa **termasuk Indonesian** | Halaman course AI-200T00 | Bahasa course ≠ bahasa exam (jangan disamakan) | High | 2026-07-15 | SRC-003 | Sesuai baseline |
| Blog pengumuman Tech Community | **Tidak dapat diakses dari environment ini** (HTTP 403 pada semua tool). Isi kedua post tidak dapat diverifikasi | — | Halaman resmi Learn menjadikan post 4494128 sebagai target "Learn more" pada banner retirement AZ-204 — membuktikan post itu pengumuman resmi yang ditunjuk Microsoft, tanpa bisa membaca isinya | Low | 2026-07-15 | SRC-020, SRC-021 | `Needs Review` |
| Exam sandbox | fwlink 2226877 → destinasi **`https://mscertdemo.starttest.com/`** ("Microsoft Sandbox - English"); halaman "Prepare for an exam" menyebut URL destinasi yang sama secara eksplisit | Halaman prepare-exam; resolusi fwlink | Destinasi adalah **operational destination pihak ketiga**, bukan sumber bukti | High | 2026-07-15 | SRC-018, SRC-019 | Sesuai baseline |

### Ringkasan status exam

Status dipisah menjadi dua atribut agar `Transitional/Unresolved` tidak disalahartikan sebagai "exam tidak tersedia":

| Atribut | Nilai per 2026-07-15 |
|---|---|
| **Operational availability** (bisakah exam diambil?) | Surface scheduling resmi Pearson VUE untuk `exam.AI-200` ada (SRC-016); review eksternal melaporkan exam dapat dijadwalkan — belum terverifikasi dari halaman resmi yang dibuka oleh environment ini. Tidak ada indikasi resmi bahwa exam TIDAK tersedia |
| **Lifecycle status** (beta atau sudah GA?) | **Transitional/Unresolved** — belum ditemukan pernyataan resmi eksplisit bertanggal yang memastikan beta ataupun GA. Ketiadaan Practice Assessment diperlakukan sebagai **sinyal pendukung saja** dan tidak menentukan status: bisa berarti masih beta, atau sudah keluar beta tetapi masih dalam jendela ±8 minggu sebelum Practice Assessment terbit |

| Kesimpulan status | Bukti yang mendukung | Bukti yang melemahkan/ambigu | Confidence |
|---|---|---|---|
| **Transitional/Unresolved** | (a) Tidak ada pernyataan resmi Microsoft eksplisit & bertanggal — pada halaman mana pun yang dapat dibuka per 2026-07-15 — bahwa AI-200 telah "gone live"/"generally available"/"out of beta" (SRC-001…SRC-021); (b) catatan Practice Assessment di halaman sertifikasi berbunyi "…usually available within 8 weeks of the exam being out of beta and generally available" dan Practice Assessment "not currently available" (SRC-001) — *teks generik; sinyal pendukung saja, kompatibel dengan "masih beta" maupun "baru saja GA"*; (c) AI-200 absen dari daftar Practice Assessments (SRC-015) — *sinyal pendukung saja*; (d) metadata indeks pencarian Learn masih memuat varian judul halaman sertifikasi dengan sufiks "(beta)" — *sinyal metadata, belum terkonfirmasi on-page* | (a) Bagian halaman sertifikasi tempat sufiks "(beta)", bahasa, durasi, dan tombol jadwal seharusnya tampil **dirender client-side dan tidak dapat diperiksa** oleh tool yang tersedia; (b) blog pengumuman resmi (satu-satunya kandidat pernyataan bertanggal) tidak dapat diakses dari environment ini; (c) ketiadaan pengumuman GA bukan bukti bahwa GA belum terjadi — exam dapat saja go live tanpa halaman yang terjangkau tool ini; (d) konten komunitas di `learn.microsoft.com/answers` membahas status beta AI-200 dan proyeksi GA Juli 2026, tetapi sesuai kebijakan sumber prompt, konten Q&A **sengaja tidak digunakan sebagai bukti** | **Medium** untuk karakterisasi "Transitional/Unresolved" (kondisi transisi didukung banyak sinyal konsisten); **Low** untuk penentuan biner beta-vs-GA — karena itu penentuan biner tidak dipaksakan |

**Implikasi praktis (rekomendasi belajar, bukan fakta):** perlakukan AI-200 sebagai exam yang berada pada jendela transisi beta→live. Sebelum menjadwalkan, buka halaman sertifikasi langsung di browser dan periksa apakah nama exam masih menampilkan "(beta)"; jika masih beta, ingat aturan beta: skor tidak langsung keluar (SRC-010) dan beta hanya boleh diambil 1× selama periode beta (SRC-009).

---

## 1. Ringkasan Exam

| Atribut | Nilai terbaru | Source ID |
|---|---|---|
| Exam code dan nama | Exam AI-200: Developing AI Cloud Solutions on Azure | SRC-002 |
| Certification | Microsoft Certified: Azure AI Cloud Developer Associate | SRC-001 |
| Status | **Transitional/Unresolved** — *lifecycle status* (tidak ada bukti resmi eksplisit yang menyelesaikan beta vs GA per tanggal cek); bukan indikasi ketersediaan operasional — surface scheduling Pearson VUE ada | SRC-001, SRC-015, SRC-016, SRC-020, SRC-021 |
| Confidence dan ringkasan bukti | Medium untuk karakterisasi transisi; Low untuk penentuan biner. Bukti: catatan Practice Assessment ("…out of beta…"), absennya AI-200 dari daftar Practice Assessments, varian judul "(beta)" di metadata indeks; konten exam-details client-side tidak terperiksa | SRC-001, SRC-015 |
| Tanggal status diperiksa | 2026-07-15 | — |
| Level | Intermediate | SRC-001 |
| Role | Developer | SRC-001 |
| Subject | Application development; Artificial intelligence | SRC-001 |
| Bahasa exam | **BELUM DAPAT DIVERIFIKASI DARI SUMBER RESMI MICROSOFT** oleh environment ini (client-side). Review eksternal melaporkan **English** (konsisten baseline) — menunggu konfirmasi dari halaman resmi. Study guide: bila exam tidak tersedia dalam bahasa pilihan, dapat meminta tambahan 30 menit | SRC-001, SRC-002 |
| Assessment time | Untuk AI-200 spesifik: **BELUM DAPAT DIVERIFIKASI** oleh environment ini (dinamis). Review eksternal melaporkan **120 minutes** (konsisten baseline) — menunggu konfirmasi. Kebijakan umum associate role-based: 100 menit (tanpa lab) atau 120 menit (dapat memuat lab) | SRC-007 |
| Seat time jika dapat diverifikasi | Kebijakan umum: 120 menit (tanpa lab) / 140 menit (dapat memuat lab); angka spesifik AI-200 belum terverifikasi | SRC-007 |
| Passing score | **Scaled score 700 atau lebih** pada skala 1–1.000; bukan "70% jawaban benar" ("As this is a scaled score, it may not equal 70% of the points") | SRC-008, SRC-002 |
| Score availability/timing | Live: hasil dalam hitungan menit; Learn profile ≤24 jam; exam ber-lab ~30 menit ekstra. Beta: skor keluar ~10 hari setelah exam goes live (10–12 minggu setelah beta dimulai; bisa hingga 14 minggu) | SRC-008, SRC-010 |
| Retake policy | Umum: 24 jam setelah gagal pertama; 14 hari antar-attempt berikutnya; maksimum 5 attempt per 12 bulan. Beta: hanya 1× selama periode beta; jika gagal, retake setelah live | SRC-009, SRC-010 |
| Delivery/proctoring | Pearson VUE (test center atau online proctored: secure browser, webcam+microphone monitoring, room scan, government ID) | SRC-012, SRC-017 |
| Interactive components/lab | Tidak diklaim. Kebijakan resmi: Microsoft tidak menerbitkan daftar exam ber-lab; lab dapat dihapus sewaktu-waktu; informasi diberikan saat registrasi/launch exam | SRC-007 |
| Practice Assessment | Tidak tersedia untuk AI-200; tidak terdaftar pada daftar resmi (biasanya tersedia ±8 minggu setelah exam out of beta dan GA) | SRC-001, SRC-015 |
| Scheduling | Surface resmi `schedule-through-pearson-vue?examUid=exam.AI-200` ada (dinamis, sign-in gated); review eksternal melaporkan **dapat dijadwalkan melalui Pearson VUE** — belum terverifikasi langsung dari environment audit | SRC-016, SRC-017 |
| Renewal | Kebijakan umum associate: expire tahunan; renewal gratis via online assessment (unproctored, open book) di Microsoft Learn; jendela 6 bulan; +1 tahun setelah lulus. Baris renewal spesifik AI-200 belum tampak (`Needs Review`) | SRC-014, SRC-001 |
| Relationship dengan AZ-204 | AZ-204/Azure Developer Associate retire **31 Juli 2026** (terverifikasi). Penunjukan resmi AI-200 sebagai replacement path: **BELUM DAPAT DIVERIFIKASI** dari halaman yang dapat diakses (banner AZ-204 hanya menaut blog yang tidak terjangkau). AI-200 **bukan** rename/salinan AZ-204 — cakupan skills measured berbeda (perbandingan SRC-002 vs SRC-005) | SRC-004, SRC-005, SRC-006, SRC-021 |

---

## 2. Profil Kandidat

Parafrase dari audience profile resmi (SRC-001, SRC-002):

Kandidat AI-200 adalah developer yang **berkontribusi pada semua fase implementasi AI solutions di Azure**, dengan penekanan pada **back-end services dan komponennya** — bukan hanya menulis kode, tetapi juga terlibat dalam **requirements gathering, design, development, deployment, security, dan monitoring**.

Kandidat diharapkan cakap dalam:

- **Azure SDKs dan third-party SDKs** yang dipakai di Azure — memilih, mengautentikasi, dan memakai client library dengan benar;
- **Azure data management services** — Cosmos DB for NoSQL, Azure Database for PostgreSQL, Azure Managed Redis;
- **Monitoring dan troubleshooting** — logs, metrics, traces, dan analisisnya;
- **Messaging dan eventing** — Service Bus, Event Grid, pola event-driven;
- **Vector databases** — menyimpan embedding dan menjalankan similarity search untuk skenario semantic retrieval/RAG;
- **Python** — bahasa utama contoh dan praktik pada kurikulum ini;
- **Containerized applications** — build, ship, run di ACR, App Service, Container Apps, dan AKS.

**Interpretasi teknis:** dibandingkan AZ-204 (yang retire 31 Juli 2026, SRC-004), profil AI-200 menggeser fokus dari "breadth of Azure compute + storage" ke **backend AI workloads**: data layer untuk vector/RAG, messaging untuk arsitektur event-driven, dan observability modern (OpenTelemetry + KQL). Ini interpretasi dari perbandingan skills measured kedua study guide (SRC-002, SRC-005), bukan pernyataan resmi.

---

## 3. Strategi Belajar

Seluruh bagian ini adalah **rekomendasi belajar** (bukan fakta resmi), disusun dari struktur skills measured (SRC-002).

### Urutan domain yang disarankan

1. **Domain 1 — Develop containerized solutions (20–25%)** terlebih dahulu: semua praktik lain butuh aplikasi yang berjalan; container + ACR menjadi fondasi deployment untuk seluruh skenario end-to-end.
2. **Domain 2 — AI solutions dengan data management services (25–30%)**: bobot terbesar; kerjakan segera setelah punya fondasi deploy. Cosmos DB → PostgreSQL/pgvector → Azure Managed Redis, karena pola vector search berulang di ketiganya dan saling memperkuat.
3. **Domain 3 — Connect and consume Azure services (20–25%)**: messaging/eventing menghubungkan komponen yang sudah dibuat di Domain 1–2 menjadi arsitektur asinkron.
4. **Domain 4 — Secure, monitor, and troubleshoot (20–25%)** terakhir sebagai lapisan lintas-layanan: Key Vault/App Configuration mengamankan semua modul sebelumnya; OpenTelemetry + KQL mengobservasi seluruh alur.

**Alasan urutan:** mengikuti alur dependency nyata sebuah solusi (deploy → data → integrasi → secure/observe), sehingga setiap modul memakai hasil modul sebelumnya, bukan urutan hafalan.

### Prinsip lintas-modul: security & observability sejak lab pertama

Pelajari Domain 4 secara formal setelah Domain 1–3, tetapi **terapkan security dan observability minimum pada setiap lab sejak awal**. Domain 4 berfungsi sebagai konsolidasi dan pendalaman, bukan perkenalan pertama terhadap security dan telemetry. Penerapan minimum per modul (rekomendasi):

- **d1-01 ACR:** authentication dan RBAC sejak lab pertama;
- **d1-02 App Service:** managed identity + secret reference, bukan connection string hardcoded;
- **d1-03 Container Apps:** managed identity, secrets, logs, dan pemahaman revisions;
- **d1-04 AKS:** identity, RBAC, probes, logs, events;
- **d2-x data services:** Microsoft Entra ID / data-plane authorization bila didukung layanannya;
- **d3-01 Service Bus:** passwordless authentication dan least privilege;
- **seluruh compute:** logs, metrics, dan tracing dasar diaktifkan sejak deploy pertama.

Setiap file detail memiliki section Security (template §6) yang mengoperasionalkan prinsip ini — bukan menundanya ke d4-01/d4-03.

### Hubungan antarlayanan

Satu skenario mengikat semuanya: aplikasi Python dikemas sebagai container (ACR), dijalankan (App Service/Container Apps/AKS), menerima pekerjaan lewat messaging (Service Bus/Event Grid/Functions), membaca-menulis data & vector (Cosmos DB/PostgreSQL/Redis), mengambil rahasia & konfigurasi (Key Vault/App Configuration), dan mengirim telemetry (OpenTelemetry → Azure Monitor → KQL). Lihat [Roadmap Hands-on](#6-roadmap-hands-on).

### Proporsi waktu yang disarankan

- **Theory/dokumentasi: ±30%** — mental model, decision guide, batasan layanan.
- **Hands-on: ±45%** — Portal + CLI + Python SDK untuk setiap bullet yang praktikal.
- **Review & troubleshooting drill: ±15%** — playbook gejala→penyebab→solusi.
- **Mock scenarios/self-assessment: ±10%** — pertanyaan skenario orisinal di tiap modul.

### Menggunakan Microsoft Learn saat exam — tanpa bergantung padanya

**Fakta (SRC-007):** pada associate/expert role-based exams, kandidat dapat mengakses Microsoft Learn selama exam — seluruh domain learn.microsoft.com **kecuali** Q&A, Practice Assessments, dan profil — **tanpa waktu tambahan**, dan timer terus berjalan. **Catatan:** konfirmasi spesifik untuk AI-200 belum dapat diperiksa (halaman exam dinamis); penerapan ke AI-200 adalah interpretasi wajar karena AI-200 adalah role-based exam.

**Rekomendasi:** latih *navigasi terarah*: hafal struktur hub docs tiap layanan (mis. di mana indexing policy Cosmos DB atau KEDA scale rules berada), sehingga Learn dipakai untuk konfirmasi cepat (satu-dua menit), bukan membaca dari nol. Jangan merencanakan menjawab soal dengan riset penuh — waktu tidak cukup.

### Prioritas domain berbobot terbesar

Domain 2 (25–30%) mendapat porsi file terbanyak (3 file, 15 bullet praktik) dan sebaiknya mendapat porsi review terbesar. Vector search muncul di **tiga layanan berbeda** (Cosmos DB, PostgreSQL/pgvector, Azure Managed Redis) — pahami perbedaan model, indexing, dan trade-off-nya karena pemilihan layanan adalah tipikal keputusan desain yang diuji (inferensi pola soal, bukan klaim soal nyata).

---

## 4. Peta Domain dan Modul

Judul domain, bobot, dan subheading di bawah ini dikutip dari study guide resmi (SRC-002), diakses 2026-07-15.

### Domain 1 — Develop containerized solutions on Azure (20–25%)

| Subheading resmi | Layanan | File |
|---|---|---|
| Implement container application hosting | Azure Container Registry (+ACR Tasks), Azure App Service | [d1-01-azure-container-registry.md](d1-01-azure-container-registry.md), [d1-02-azure-app-service-container.md](d1-02-azure-app-service-container.md) |
| Implement container-orchestrated solutions | Azure Container Apps (+KEDA), Azure Kubernetes Service | [d1-03-azure-container-apps-keda.md](d1-03-azure-container-apps-keda.md), [d1-04-azure-kubernetes-service.md](d1-04-azure-kubernetes-service.md) |

### Domain 2 — Develop AI solutions by using Azure data management services (25–30%)

| Subheading resmi | Layanan | File |
|---|---|---|
| Develop AI solutions by using Azure Cosmos DB for NoSQL | Azure Cosmos DB for NoSQL | [d2-01-cosmos-db-nosql.md](d2-01-cosmos-db-nosql.md) |
| Develop AI solutions by using Azure Database for PostgreSQL | Azure Database for PostgreSQL, pgvector | [d2-02-azure-database-postgresql.md](d2-02-azure-database-postgresql.md) |
| Integrate Azure Managed Redis in AI solutions | Azure Managed Redis | [d2-03-azure-managed-redis.md](d2-03-azure-managed-redis.md) |

### Domain 3 — Connect to and consume Azure services (20–25%)

| Subheading resmi | Layanan | File |
|---|---|---|
| Develop event- and message-based AI solutions | Azure Service Bus, Azure Event Grid | [d3-01-azure-service-bus.md](d3-01-azure-service-bus.md), [d3-02-azure-event-grid.md](d3-02-azure-event-grid.md) |
| Develop and implement Azure Functions | Azure Functions | [d3-03-azure-functions.md](d3-03-azure-functions.md) |

### Domain 4 — Secure, monitor, and troubleshoot Azure solutions (20–25%)

| Subheading resmi | Layanan | File |
|---|---|---|
| Implement secure Azure solutions | Azure Key Vault, Azure App Configuration | [d4-01-azure-key-vault.md](d4-01-azure-key-vault.md), [d4-02-azure-app-configuration.md](d4-02-azure-app-configuration.md) |
| Monitor and troubleshoot Azure solutions | OpenTelemetry, Azure Monitor, Log Analytics, KQL | [d4-03-observability-opentelemetry-kql.md](d4-03-observability-opentelemetry-kql.md) |

> Catatan: pada "Skills at a glance" study guide, Domain 4 ditulis "Secure, monitor, troubleshoot Azure solutions"; pada heading rinci ditulis "Secure, monitor, and troubleshoot Azure solutions". Repositori ini memakai bentuk heading rinci. (SRC-002)

**Catatan produk yang dijaga di seluruh repositori:**

- Skills measured menyebut **Azure Managed Redis** — produk berbeda dari **Azure Cache for Redis** (hub docs terpisah: `/azure/redis/` vs `/azure/azure-cache-for-redis/`; SRC-029). Perhatikan: tabel "Find documentation" pada study guide masih menaut ke Azure Cache for Redis — kurikulum ini mengikuti **skills measured** (Azure Managed Redis), dan tabel Find-documentation generik tidak dijadikan acuan cakupan (SRC-002, SRC-029).
- Cosmos DB difokuskan pada **Azure Cosmos DB for NoSQL** sesuai skills measured, bukan seluruh API (SRC-002, SRC-027).
- Container Instances, Blob Storage, Event Hubs, API Management, Queue Storage muncul di tabel Find-documentation study guide tetapi **tidak ada** pada bullet skills measured → hanya akan disinggung sebagai pembanding dan ditandai **out of primary exam scope**.
- Fitur Preview tidak otomatis keluar cakupan: "Most questions cover features that are general availability (GA). The exam may contain questions on Preview features if those features are commonly used." (SRC-002)

---

## 5. Coverage Matrix

Setiap bullet resmi skills measured (SRC-002) dipetakan ke minimal satu file. `Coverage`: `Planned` / `Draft` / `Complete` / `Needs Review`.

`Source readiness` membedakan kelengkapan sumber dari status penulisan (sehingga `Planned` tidak memberi kesan sumber implementasi sudah lengkap): `Hub only` = baru hub docs yang terverifikasi; `Specific docs identified` = artikel spesifik sudah ditemukan & dibuka; `Implementation sources verified` = seluruh artikel yang dipakai modul sudah diverifikasi (dicapai saat modul ditulis).

| # | Domain | Official skill heading | Skill (parafrase) | Layanan/fitur | File tujuan | Praktik wajib | Source ID | Source readiness | Coverage |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 1 | Implement container application hosting | Build, store, version, dan manage container image di registry privat | Azure Container Registry | d1-01 | Build/tag/push/pull image; versioning dan manajemen repository | SRC-002, SRC-022, SRC-040, SRC-042–SRC-046, SRC-048, SRC-049 | Implementation sources verified | Draft |
| 2 | 1 | Implement container application hosting | Build dan run image menggunakan ACR Tasks | ACR Tasks | d1-01 | `az acr build`, `az acr run`, task otomatis | SRC-002, SRC-022, SRC-041, SRC-047 | Implementation sources verified | Draft |
| 3 | 1 | Implement container application hosting | Deploy container ke App Service, termasuk environment variables dan secrets | Azure App Service (custom container) | d1-02 | Deploy image dari ACR (managed identity); app settings → env vars; Key Vault references | SRC-002, SRC-023, SRC-050–SRC-054 | Implementation sources verified | Draft |
| 4 | 1 | Implement container-orchestrated solutions | Deploy aplikasi ke Container Apps, termasuk konfigurasi environment dan revision management | Azure Container Apps | d1-03 | Buat environment; deploy; kelola revisions/traffic split/labels | SRC-002, SRC-024, SRC-055–SRC-057 | Implementation sources verified | Draft |
| 5 | 1 | Implement container-orchestrated solutions | Terapkan event-driven scaling dengan KEDA di Container Apps | Container Apps + KEDA | d1-03 | Scale rule HTTP + custom `azure-servicebus` (auth secret/managed identity); validasi end-to-end bersama d3-01 | SRC-002, SRC-025 | Implementation sources verified | Draft |
| 6 | 1 | Implement container-orchestrated solutions | Deploy dan kelola aplikasi di AKS menggunakan manifest files | Azure Kubernetes Service | d1-04 | Cluster + node pools; `kubectl apply` manifest (Deployment/Service, probes, nodeSelector); attach ACR | SRC-002, SRC-026, SRC-060, SRC-061 | Implementation sources verified | Draft |
| 7 | 1 | Implement container-orchestrated solutions | Monitor dan troubleshoot solusi di AKS dan Container Apps: logs, events, konektivitas end-to-end | AKS, Container Apps | d1-03 (Container Apps) + d1-04 (AKS) — cross-link dua arah | Inspeksi logs/events/probes; uji konektivitas eksternal (LoadBalancer+curl) & internal (nc -zv); az aks check-acr | SRC-002, SRC-024, SRC-026, SRC-058, SRC-059, SRC-062, SRC-063 | Implementation sources verified | Draft |
| 8 | 2 | Develop AI solutions by using Azure Cosmos DB for NoSQL | Connect ke Cosmos DB for NoSQL via SDK dan jalankan query | Cosmos DB for NoSQL, Python SDK | d2-01 | CRUD, point read, query berparameter via `azure-cosmos` + DefaultAzureCredential | SRC-002, SRC-027, SRC-064 | Implementation sources verified | Draft |
| 9 | 2 | Develop AI solutions by using Azure Cosmos DB for NoSQL | Optimasi performa query dan konsumsi RU via indexing policies dan consistency levels | Indexing policy, consistency, RU | d2-01 | Include/exclude paths, composite index, ukur RU header, uji 5 consistency levels | SRC-002, SRC-027, SRC-065, SRC-066, SRC-069 | Implementation sources verified | Draft |
| 10 | 2 | Develop AI solutions by using Azure Cosmos DB for NoSQL | Simpan/ambil embeddings dan jalankan vector similarity search untuk semantic retrieval | Vector search di Cosmos DB for NoSQL | d2-01 | Vector policy + index (flat/quantizedFlat/diskANN); query `VectorDistance` TOP N via Python | SRC-002, SRC-027, SRC-067, SRC-070 | Implementation sources verified | Draft |
| 11 | 2 | Develop AI solutions by using Azure Cosmos DB for NoSQL | Implement change feed processor untuk mendeteksi item baru/berubah | Change feed | d2-01 | Pull model Python (`query_items_change_feed`) + continuation token; konsep processor vs pull | SRC-002, SRC-027, SRC-068 | Implementation sources verified | Draft |
| 12 | 2 | Develop AI solutions by using Azure Database for PostgreSQL | Connect dan query Azure Database for PostgreSQL via SDK | Azure Database for PostgreSQL | d2-02 | Koneksi + query dari Python | SRC-002, SRC-028 | Hub only | Planned |
| 13 | 2 | Develop AI solutions by using Azure Database for PostgreSQL | Modelkan schema dan strategi indexing: desain tabel dan pemilihan data type | Schema/index design | d2-02 | DDL tabel; pilih tipe data | SRC-002, SRC-028 | Hub only | Planned |
| 14 | 2 | Develop AI solutions by using Azure Database for PostgreSQL | Strategi indexing: optimasi latency query dan pengurangan overhead compute pgvector | pgvector indexing | d2-02 | Bandingkan tipe index vector; ukur latency | SRC-002, SRC-028 | Hub only | Planned |
| 15 | 2 | Develop AI solutions by using Azure Database for PostgreSQL | Konfigurasi compute, memory, dan storage untuk vector workloads | Sizing Flexible Server | d2-02 | Pilih SKU/konfigurasi untuk beban vector | SRC-002, SRC-028 | Hub only | Planned |
| 16 | 2 | Develop AI solutions by using Azure Database for PostgreSQL | Vector similarity search: simpan embedding, semantic retrieval, pola RAG dengan metadata filter | pgvector + RAG | d2-02 | Similarity search + filter metadata (RAG) | SRC-002, SRC-028 | Hub only | Planned |
| 17 | 2 | Develop AI solutions by using Azure Database for PostgreSQL | Optimasi koneksi untuk throughput dan latency | Connection pooling/optimization | d2-02 | Uji pooling; bandingkan latency | SRC-002, SRC-028 | Hub only | Planned |
| 18 | 2 | Integrate Azure Managed Redis in AI solutions | Operasi data Azure Managed Redis: caching, expiration, invalidation | Azure Managed Redis | d2-03 | Cache-aside; TTL; invalidasi | SRC-002, SRC-029 | Hub only | Planned |
| 19 | 2 | Integrate Azure Managed Redis in AI solutions | Vector indexing untuk similarity search | Vector search di Redis | d2-03 | Index vector + query kemiripan | SRC-002, SRC-029 | Hub only | Planned |
| 20 | 3 | Develop event- and message-based AI solutions | Queue & proses operasi back-end via Service Bus: messages, topics, subscriptions, dead-letter handling | Azure Service Bus | d3-01 | Kirim/terima; topic+subscription; DLQ handling | SRC-002, SRC-030, SRC-039 | Specific docs identified | Planned |
| 21 | 3 | Develop event- and message-based AI solutions | Event-driven workflows via Event Grid: filters, custom events, retries | Azure Event Grid | d3-02 | Custom topic + event; filter; amati retry | SRC-002, SRC-031 | Hub only | Planned |
| 22 | 3 | Develop and implement Azure Functions | Bangun serverless APIs: triggers dan bindings | Azure Functions | d3-03 | HTTP/queue trigger + binding | SRC-002, SRC-032 | Hub only | Planned |
| 23 | 3 | Develop and implement Azure Functions | Konfigurasi dan deploy function apps | Azure Functions | d3-03 | Deploy + app settings | SRC-002, SRC-032 | Hub only | Planned |
| 24 | 4 | Implement secure Azure solutions | Amankan secrets via Key Vault, termasuk rotation dan retrieval | Azure Key Vault | d4-01 | Simpan/ambil/rotasi secret via SDK | SRC-002, SRC-033 | Hub only | Planned |
| 25 | 4 | Implement secure Azure solutions | Simpan dan ambil app configuration via App Configuration | Azure App Configuration | d4-02 | Key-value config + baca dari Python | SRC-002, SRC-034 | Hub only | Planned |
| 26 | 4 | Monitor and troubleshoot Azure solutions | Trace distributed systems dengan OpenTelemetry SDKs | OpenTelemetry → Azure Monitor | d4-03 | Instrument traces/metrics/logs; kirim ke Application Insights | SRC-002, SRC-035 | Hub only | Planned |
| 27 | 4 | Monitor and troubleshoot Azure solutions | Tulis KQL query untuk analisis logs dan metrics | KQL / Log Analytics | d4-03 | Filtering, aggregation, correlation, latency/error/dependency analysis | SRC-002, SRC-036, SRC-037 | Specific docs identified | Planned |

**Alasan penggabungan (pedagogis):** ACR + ACR Tasks satu file (satu resource, dua cara build); Container Apps + KEDA satu file (KEDA adalah mekanisme scaling internal Container Apps, SRC-025); bullet #7 dibagi dua file sesuai platform dengan cross-link; OpenTelemetry + Azure Monitor + KQL satu file karena membentuk satu alur telemetry-to-query.

**Kesesuaian struktur:** study guide terbaru tidak menambah/menghapus/memindahkan skill dibanding baseline → **struktur starter 13 file dipertahankan tanpa perubahan**, dan seluruh 27 bullet memiliki tempat belajar.

**Aturan sumber untuk modul detail:** hub docs cukup untuk tahap perencanaan ini, tetapi setiap file detail **wajib memakai artikel dokumentasi spesifik** untuk tiap klaim implementasi (contoh yang akan ditambahkan ke ledger saat modulnya ditulis: Cosmos DB vector search, Cosmos DB change feed processor, PostgreSQL `pgvector`, Azure Managed Redis vector search, Service Bus dead-letter queues — sudah terverifikasi sebagai SRC-039, Event Grid retry/delivery, Key Vault secret rotation, Azure Monitor OpenTelemetry, KQL operator reference). Sebuah modul baru boleh `Complete` bila `Source readiness` = `Implementation sources verified`.

---

## 6. Roadmap Hands-on

### Skenario end-to-end (kerangka integrasi)

```text
Python API / worker
  → container image
  → Azure Container Registry            (d1-01)
  → App Service / Container Apps / AKS  (d1-02, d1-03, d1-04)
  → Service Bus / Event Grid / Functions (d3-01, d3-02, d3-03)
  → Cosmos DB / PostgreSQL pgvector / Azure Managed Redis (d2-01, d2-02, d2-03)
  → Key Vault / App Configuration       (d4-01, d4-02)
  → OpenTelemetry / Azure Monitor / KQL (d4-03)
```

**Ini kerangka integrasi, bukan satu deployment tunggal.** Rekomendasi & interpretasi teknis (bukan fakta resmi):

- **Compute:** tidak perlu menjalankan App Service + Container Apps + AKS bersamaan. Urutan belajar yang efisien: App Service (paling sederhana untuk single container) → Container Apps (revisions + KEDA; pilihan utama skenario event-driven) → AKS (kontrol penuh manifest-level; paling kompleks). Skenario integrasi utama cukup memakai **Container Apps**; App Service dan AKS dilatih pada lab terpisah yang lebih kecil.
- **Data:** ketiga data service dilatih pada dataset embedding yang sama agar perbandingan vector search apple-to-apple; hanya satu yang perlu hidup pada satu waktu.
- **Messaging:** Service Bus untuk command/work-queue (dengan DLQ), Event Grid untuk notifikasi event; Functions menjadi konsumen ringan. Trade-off dibahas di masing-masing decision guide.
- **Urutan lab lintas-modul:** (1) bangun image & push ke ACR → (2) deploy ke satu compute target → (3) tambahkan queue/event → (4) sambungkan data layer → (5) pindahkan secret/config ke Key Vault/App Configuration + managed identity → (6) instrument OpenTelemetry dan analisis dengan KQL.

### Lab Environment Manifest

Semua nilai adalah **asumsi kerja** yang akan diverifikasi ulang terhadap dokumentasi resmi saat setiap modul ditulis (kolom verifikasi diisi per modul; tidak ada versi yang diklaim tanpa sumber).

| Komponen | Versi/asumsi | Tanggal verifikasi | Source ID |
|---|---|---|---|
| Operating system / shell | Linux atau macOS dengan bash/zsh; Windows via WSL2 (rekomendasi, bukan syarat resmi) | Needs Review — diverifikasi per modul | — |
| Python | 3.10+ (minimum tested version ditetapkan per modul sesuai dukungan SDK di dokumentasi resmi) | Needs Review — diverifikasi per modul | — |
| Azure CLI | 2.x terbaru (versi minimum dicatat per modul; cek `az version`) | Needs Review — diverifikasi per modul | — |
| Azure CLI extensions | `containerapp` (untuk d1-03); lainnya dicatat per modul | Needs Review — diverifikasi per modul | — |
| Python SDK packages | Ditetapkan per modul via `requirements.txt` (mis. `azure-cosmos`, `azure-servicebus`, `azure-keyvault-secrets`, `azure-appconfiguration`, `azure-identity`, `redis`, `psycopg`, OpenTelemetry packages) — nama & versi final diverifikasi ke dokumentasi resmi sebelum dipakai | Needs Review — diverifikasi per modul | — |

Prinsip yang berlaku di semua lab: placeholder jelas (`<RESOURCE_GROUP>`, `<LOCATION>`, `<ACR_NAME>`), tanpa secret/tenant/subscription nyata, autentikasi **Microsoft Entra ID + managed identity** diprioritaskan bila didukung, command idempotent atau diberi catatan perilaku saat diulang.

---

## 7. Cost and Cleanup Guardrails

**Prinsip umum (berlaku untuk semua modul):**

- Kurikulum ini **tidak membuat resource apa pun secara otomatis**. Semua lab dieksekusi manual oleh pembelajar.
- **Jangan menulis/mengasumsikan nominal biaya** — harga berubah; cek halaman Azure Pricing resmi saat eksekusi lab.
- Satu resource group per modul (`rg-ai200-<modul>`), sehingga cleanup = satu perintah: `az group delete --name <RESOURCE_GROUP> --yes --no-wait`.
- **Verifikasi cleanup** selalu dijalankan: `az group exists --name <RESOURCE_GROUP>` harus mengembalikan `false` (atau `az group show` mengembalikan not-found).
- Pemilihan tier hemat di bawah ini adalah **rekomendasi** yang harus dicek ulang ke halaman pricing/tier resmi saat modul ditulis.

| Modul | Resource berpotensi berbayar | Arah tier hemat (rekomendasi, verifikasi saat eksekusi) | Risiko "lupa matikan" |
|---|---|---|---|
| d1-01 | Container Registry | Tier terendah yang tersedia (cek halaman SKU ACR) | Rendah, tetapi storage image tetap ditagih |
| d1-02 | App Service plan | Tier dev/test terkecil; hapus plan (bukan hanya app) saat selesai | **Tinggi** — App Service plan menagih walau app berhenti |
| d1-03 | Container Apps environment + Log Analytics | Consumption-based; scale-to-zero bila mungkin | Sedang — Log Analytics workspace ikut dibuat |
| d1-04 | AKS cluster (node VM, disk, IP) | Node count minimum; hapus cluster segera setelah lab | **Sangat tinggi** — node VM menagih terus; jangan biarkan cluster hidup |
| d2-01 | Cosmos DB account | Evaluasi opsi free tier/serverless pada dokumentasi resmi saat eksekusi | Sedang |
| d2-02 | Azure Database for PostgreSQL | SKU burstable terkecil; stop server saat tidak dipakai bila didukung | **Tinggi** — compute DB menagih saat idle |
| d2-03 | Azure Managed Redis | Tier terkecil yang tersedia (cek halaman tier resmi) | **Tinggi** — cache menagih saat idle |
| d3-01 | Service Bus namespace | Gunakan tier terendah yang mendukung seluruh lab. Queue dan dead-letter handling dapat dilatih pada queue — DLQ adalah **subqueue bawaan** pada setiap queue dan topic subscription, bukan fitur tier (SRC-039). Topics/subscriptions memerlukan tier yang mendukung publish/subscribe; verifikasi feature matrix tier sebelum provisioning | Rendah–sedang |
| d3-02 | Event Grid custom topic | Bayar per operasi; volume lab kecil | Rendah |
| d3-03 | Function app + storage account | Consumption plan | Rendah–sedang (storage account tersisa) |
| d4-01 | Key Vault | Bayar per operasi; volume lab kecil | Rendah |
| d4-02 | App Configuration | Evaluasi tier free/standard pada dokumentasi resmi | Rendah |
| d4-03 | Log Analytics workspace + Application Insights | Perhatikan ingestion & retention; batasi volume telemetry lab | Sedang — ingestion telemetry berkelanjutan |

**Resource yang tidak boleh dibiarkan aktif tanpa sengaja:** AKS cluster, PostgreSQL server, Azure Managed Redis, App Service plan. Setiap modul akan memuat langkah cleanup + verifikasi cleanup spesifik.

---

## 8. Status Pengerjaan

| Domain | Topik | File | Status | Coverage | Last reviewed |
|---|---|---|---|---|---|
| — | Induk: audit, peta, ledger | README.md | **Direvisi pasca review eksternal — menunggu checkpoint ulang** | — | 2026-07-15 |
| 1 | Azure Container Registry + ACR Tasks | [d1-01-azure-container-registry.md](d1-01-azure-container-registry.md) | **Draft — menunggu review** | Draft | 2026-07-15 |
| 1 | App Service custom container | [d1-02-azure-app-service-container.md](d1-02-azure-app-service-container.md) | **Draft — menunggu review** | Draft | 2026-07-15 |
| 1 | Container Apps + KEDA | [d1-03-azure-container-apps-keda.md](d1-03-azure-container-apps-keda.md) | **Draft — menunggu review** | Draft | 2026-07-15 |
| 1 | Azure Kubernetes Service | [d1-04-azure-kubernetes-service.md](d1-04-azure-kubernetes-service.md) | **Draft — menunggu review** | Draft | 2026-07-15 |
| 2 | Cosmos DB for NoSQL | [d2-01-cosmos-db-nosql.md](d2-01-cosmos-db-nosql.md) | **Draft — review di akhir** | Draft | 2026-07-15 |
| 2 | Azure Database for PostgreSQL + pgvector | d2-02-azure-database-postgresql.md | Belum dibuat | Planned | — |
| 2 | Azure Managed Redis | d2-03-azure-managed-redis.md | Belum dibuat | Planned | — |
| 3 | Azure Service Bus | d3-01-azure-service-bus.md | Belum dibuat | Planned | — |
| 3 | Azure Event Grid | d3-02-azure-event-grid.md | Belum dibuat | Planned | — |
| 3 | Azure Functions | d3-03-azure-functions.md | Belum dibuat | Planned | — |
| 4 | Azure Key Vault | d4-01-azure-key-vault.md | Belum dibuat | Planned | — |
| 4 | Azure App Configuration | d4-02-azure-app-configuration.md | Belum dibuat | Planned | — |
| 4 | Observability: OpenTelemetry + Azure Monitor + KQL | d4-03-observability-opentelemetry-kql.md | Belum dibuat | Planned | — |

---

## 9. Source Ledger

Semua URL **dibuka dan dibaca** pada 2026-07-15 melalui Microsoft Learn MCP tools resmi (bukan snippet), kecuali dicatat lain. `Last updated` = tanggal yang terlihat pada konten yang dapat diambil; `Not shown` = tidak ditampilkan/tidak dapat diambil oleh tool (bukan berarti tidak ada di halaman rendered). Kekuatan bukti: `Primary` / `Supporting` / `Historical`.

| ID | Sumber Microsoft | Jenis | Klaim/topik yang didukung | Last updated | Diakses | Kekuatan bukti | Operational destination | Status |
|---|---|---|---|---|---|---|---|---|
| SRC-001 | <https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-cloud-developer-associate/> | Halaman sertifikasi | Identitas certification; level/role/subject; audience profile; catatan Practice Assessment; sinyal status | Not shown | 2026-07-15 | Primary | — | **Needs Review** (bagian exam-details client-side tidak terperiksa) |
| SRC-002 | <https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200> | Study guide | Domain, bobot, seluruh 27 bullet skills measured; audience profile; catatan GA/Preview; skor 700; catatan lokalisasi +30 menit | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-003 | <https://learn.microsoft.com/en-us/training/courses/ai-200t00> | Halaman course | Course AI-200T00-A: judul, 5 hari, Intermediate, 12 bahasa termasuk Indonesian | Not shown | 2026-07-15 | Supporting | — | OK |
| SRC-004 | <https://learn.microsoft.com/en-us/credentials/certifications/azure-developer/> | Halaman sertifikasi (AZ-204) | Banner retirement AZ-204: 31 Juli 2026; tidak menyebut pengganti; Renewal Frequency 12 months | 01/14/2026 (tampil di halaman) | 2026-07-15 | Primary | — | OK |
| SRC-005 | <https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-204> | Study guide (AZ-204) | Warning retirement "July 31, 2026, at 11:59 PM Central Standard Time"; link "Learn more" → blog 4494128; pembanding cakupan AZ-204 (5 domain) vs AI-200 (4 domain) | "Skills measured as of January 14, 2026" | 2026-07-15 | Supporting | — | OK |
| SRC-006 | <https://learn.microsoft.com/en-us/credentials/support/retired-certification-exams> | Halaman kebijakan | Baris "AZ-204 … July 31, 2026" pada Exams scheduled to retire; AI-200 tidak terdaftar; AI-102 retired 30 Juni 2026 | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-007 | <https://learn.microsoft.com/en-us/credentials/support/exam-duration-exam-experience> | Halaman kebijakan | Tabel durasi (associate: 100/120 atau 120/140 menit); kebijakan lab tidak dipublikasikan per-exam; akses Microsoft Learn saat role-based exam (kecuali Q&A/Practice/profil, timer jalan); unscheduled breaks | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-008 | <https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports> | Halaman kebijakan | Scaled score 1–1.000, lulus ≥700; "may not equal 70% of the points"; timing hasil live & catatan beta | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-009 | <https://learn.microsoft.com/en-us/credentials/support/retake-policy> | Halaman kebijakan | Retake 24 jam/14 hari/maks 5 per 12 bulan; "Beta exams may be taken only once during the beta period" | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-010 | <https://learn.microsoft.com/en-us/credentials/support/about-beta-exams> | Halaman kebijakan | Proses beta; skor ~10 hari setelah go-live (10–12 minggu setelah beta mulai, hingga 14 minggu); diskon 80% + 25%; lulus beta dihitung untuk certification; larangan lokasi tertentu | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-011 | <https://learn.microsoft.com/en-us/credentials/support/reschedule-and-cancellation-policy> | Halaman kebijakan | Reschedule/cancel ≥24 jam sebelum jadwal atau fee hangus; proses via Learn profile | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-012 | <https://learn.microsoft.com/en-us/credentials/support/frequently-asked-questions-about-online-proctored-exams> | Halaman kebijakan | Online proctoring via Pearson VUE; webcam/microphone monitoring; room scan + ID; maksimal 2 exam terjadwal | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-013 | <https://learn.microsoft.com/en-us/credentials/certifications/accommodations> | Halaman kebijakan | Proses accommodation (via Pearson VUE, ±10 hari kerja); extra time bila exam tak tersedia dalam bahasa native (form ESL); angka 30 menit TIDAK ada di halaman ini (ada di study guide) | Not shown | 2026-07-15 | Primary | Form ESL Pearson VUE (dari halaman Microsoft) | OK |
| SRC-014 | <https://learn.microsoft.com/en-us/credentials/certifications/renew-your-microsoft-certification> | Halaman kebijakan | Renewal gratis, unproctored, open book, via Microsoft Learn; jendela 6 bulan; +1 tahun; fundamentals tidak expire | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-015 | <https://learn.microsoft.com/en-us/credentials/certifications/practice-assessments-for-microsoft-certifications> | Halaman kebijakan/daftar | Daftar 46 Practice Assessments: AI-200 absen; AZ-204 masih terdaftar; gratis & boleh diulang | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-016 | <https://learn.microsoft.com/en-us/credentials/certifications/schedule-through-pearson-vue?examUid=exam.AI-200&examUrl=https%3A%2F%2Flearn.microsoft.com%2Fcredentials%2F> | Surface scheduling | Keberadaan surface scheduling AI-200 (konten dinamis, sign-in gated — tidak dapat diambil) | Not shown | 2026-07-15 | Supporting | Pearson VUE (setelah sign-in) | **Needs Review** (dinamis) |
| SRC-017 | <https://learn.microsoft.com/en-us/credentials/certifications/register-schedule-exam> | Halaman kebijakan | Alur scheduling; "Most exams show only Pearson VUE as the exam provider" | Not shown | 2026-07-15 | Supporting | Pearson VUE | OK |
| SRC-018 | <https://go.microsoft.com/fwlink/?linkid=2226877> | Short link resmi | Exam sandbox; resolusi menghasilkan "Microsoft Sandbox - English" | Not shown | 2026-07-15 | Supporting | → <https://mscertdemo.starttest.com/> (platform demo pihak ketiga; bukan sumber bukti) | OK |
| SRC-019 | <https://learn.microsoft.com/en-us/credentials/certifications/prepare-exam> | Halaman kebijakan | Menyebut eksplisit URL sandbox English = mscertdemo.starttest.com; deskripsi fungsi sandbox | Not shown | 2026-07-15 | Supporting | <https://mscertdemo.starttest.com/> | OK |
| SRC-020 | <https://techcommunity.microsoft.com/blog/skills-hub-blog/new-microsoft-certified-azure-ai-cloud-developer-associate-certification/4494116> | Blog resmi (pengumuman) | (Dituju sebagai pengumuman sertifikasi baru) — isi TIDAK dapat diverifikasi: HTTP 403 dari environment audit | Not shown | 2026-07-15 (gagal akses) | Historical | — | **Needs Review** (tidak dapat diakses) |
| SRC-021 | <https://techcommunity.microsoft.com/blog/skills-hub-blog/the-ai-job-boom-is-here-are-you-ready-to-showcase-your-skills/4494128> | Blog resmi (pengumuman) | Target link "Learn more" pada banner retirement AZ-204 (fakta penautannya terverifikasi di SRC-004/SRC-005) — isi post TIDAK dapat diverifikasi (HTTP 403) | Not shown | 2026-07-15 (gagal akses) | Historical | — | **Needs Review** (tidak dapat diakses) |
| SRC-022 | <https://learn.microsoft.com/en-us/azure/container-registry/> | Docs hub | Hub ACR ("build, store, and manage container images and artifacts in a private registry"); ada seksi ACR Tasks | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-023 | <https://learn.microsoft.com/en-us/azure/app-service/> | Docs hub | Hub App Service; quickstart Custom container | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-024 | <https://learn.microsoft.com/en-us/azure/container-apps/> | Docs hub | Hub Container Apps ("run containerized applications without worrying about orchestration or infrastructure") | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-025 | <https://learn.microsoft.com/en-us/azure/container-apps/scale-app> | Docs artikel | KEDA; limits default 0/10 (maks 1.000); rule HTTP/TCP/custom + auth (secret/managed identity); scale behavior: polling 30 dtk, cooldown 300 dtk, `ceil(metric/target)`, step 1→4→8→16; peringatan ingress-off + min 0 | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-026 | <https://learn.microsoft.com/en-us/azure/aks/> | Docs hub | Hub AKS (H1: "Azure Kubernetes Service (AKS)") | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-027 | <https://learn.microsoft.com/en-us/azure/cosmos-db/> | Docs hub | Hub Cosmos DB; API NoSQL; link "Vector search in Azure Cosmos DB for NoSQL" | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-028 | <https://learn.microsoft.com/en-us/azure/postgresql/> | Docs hub | Hub Azure Database for PostgreSQL; Flexible Server sebagai deployment utama | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-029 | <https://learn.microsoft.com/en-us/azure/redis/> | Docs hub | H1: "Azure Managed Redis Documentation" — hub khusus Azure Managed Redis, terpisah dari Azure Cache for Redis (`/azure/azure-cache-for-redis/`) | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-030 | <https://learn.microsoft.com/en-us/azure/service-bus-messaging/> | Docs hub | Hub Service Bus Messaging (queues, topics & subscriptions) | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-031 | <https://learn.microsoft.com/en-us/azure/event-grid/> | Docs hub | Hub Event Grid | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-032 | <https://learn.microsoft.com/en-us/azure/azure-functions/> | Docs hub | Hub Azure Functions; "Azure Functions triggers and bindings concepts" | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-033 | <https://learn.microsoft.com/en-us/azure/key-vault/> | Docs hub | Hub Key Vault (H1: "Azure Key Vault"); seksi Secrets | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-034 | <https://learn.microsoft.com/en-us/azure/azure-app-configuration/> | Docs hub | Hub App Configuration | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-035 | <https://learn.microsoft.com/en-us/azure/azure-monitor/> | Docs hub | Hub Azure Monitor; link "Enable OpenTelemetry" (Application Insights) | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-036 | <https://learn.microsoft.com/en-us/azure/azure-monitor/logs/get-started-queries> | Docs artikel | Get started log queries (Log Analytics/KQL): take, sort, where, ago, project/extend, summarize/bin | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-037 | <https://learn.microsoft.com/en-us/kusto/query/?view=microsoft-fabric> | Docs referensi | "Kusto Query Language overview"; Applies to: Fabric, Azure Data Explorer, Azure Monitor, Sentinel | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-038 | <https://learn.microsoft.com/en-us/credentials/certifications/online-exams> | Halaman kebijakan | "Microsoft partners with Pearson VUE to deliver online exams"; syarat government ID; link sandbox = fwlink 2226877 | Not shown | 2026-07-15 | Supporting | Pearson VUE | OK |
| SRC-039 | <https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-dead-letter-queues> | Docs artikel | "Azure Service Bus queues and topic subscriptions provide a secondary subqueue, called a dead-letter queue (DLQ)… doesn't need to be explicitly created" — DLQ bukan fitur tier; alasan dead-letter (TTLExpiredException, MaxDeliveryCountExceeded, dll.); transfer DLQ | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-040 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-image-tag-version> | Docs artikel | Stable tags (base images) vs unique tags (deployments); lock `write-enabled=false`; untagged manifests & purge/retention | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-041 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview> | Docs artikel | ACR Tasks: quick/triggered/multi-step; trigger commit, base image update, timer; context; platform; task logs; catatan free credits & diagnostic tracing | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-042 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-authentication> | Docs artikel | Metode autentikasi ACR (individual, SP, managed identity, admin, token); token `az acr login` 3 jam; `--expose-token`; admin account default disabled | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-043 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-rbac-built-in-roles-overview> | Docs artikel | Role built-in per skenario; mode "RBAC Registry + ABAC Repository Permissions" vs "RBAC Registry Permissions"; Repository Reader/Writer/Contributor/Catalog Lister vs AcrPull/AcrPush/AcrDelete; syarat melakukan role assignment | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-044 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-skus> | Docs artikel | Tabel fitur/limit Basic/Standard/Premium; rate limits + HTTP 429 + `Retry-After`; zone redundancy; `az acr show-usage`; ganti SKU tanpa downtime | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-045 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-get-started-azure-cli> | Docs quickstart | `az acr create` (nama 5–50 lowercase alnum, DNL scope, `--role-assignment-mode`); login server + hash; docker tag/push; `az acr repository list`/`show-tags`; cleanup `az group delete` | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-046 | <https://learn.microsoft.com/en-us/python/api/overview/azure/containerregistry-readme> | Docs SDK Python | `azure-containerregistry` 1.2.0; `ContainerRegistryClient` + `DefaultAzureCredential` + `audience`; list repositories/tags; `update_manifest_properties`; `delete_manifest`; Python ≥ 3.7 | Not shown (versi paket 1.2.0 tercantum) | 2026-07-15 | Primary | — | OK |
| SRC-047 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-quickstart-task-cli> | Docs quickstart | `az acr build` & `az acr run` (quick task tanpa Docker lokal); contoh output; flag `--source-acr-auth-id [caller]` untuk registry ABAC | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-048 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-get-started-portal> | Docs quickstart | Langkah pembuatan registry di Portal (DNL scope, permissions mode); `az acr login` pakai nama resource, bukan login server | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-049 | <https://learn.microsoft.com/en-us/azure/container-registry/container-registry-check-health> | Docs artikel | `az acr check-health` (CLI ≥ 2.0.67); `--ignore-errors --yes`; contoh output sehat; rujukan error reference | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-050 | <https://learn.microsoft.com/en-us/azure/app-service/configure-custom-container> | Docs artikel | Managed identity pull dari ACR (4 langkah); `WEBSITES_PORT`; env vars & reserved `DOCKER_REGISTRY_SERVER_*`; persistent storage `/home`; TLS terminate di front end; container logs; Docker Compose retire 2027-03-31; robots933456 | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-051 | <https://learn.microsoft.com/en-us/azure/app-service/configure-common> | Docs artikel | App settings → env vars (injeksi via `--env`, restart saat berubah, encrypted at rest); `:` → `__` di Linux; connection strings & prefix; Always On; izin portal | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-052 | <https://learn.microsoft.com/en-us/azure/app-service/app-service-key-vault-references> | Docs artikel | Format `@Microsoft.KeyVault(...)`; syarat managed identity + role Key Vault Secrets User/permission Get; rotasi & cache 24 jam; `keyVaultReferenceIdentity`; perilaku gagal-resolve & detector | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-053 | <https://learn.microsoft.com/en-us/azure/app-service/quickstart-custom-container> | Docs quickstart | Alur Portal (Publish=Container, OS=Linux, Image Source=ACR); opsi tier F1; pull ulang saat restart | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-054 | <https://learn.microsoft.com/en-us/azure/app-service/tutorial-custom-container> | Docs tutorial | Alur CLI Linux penuh: `az appservice plan create --is-linux` (default B1), `az webapp create --deployment-container-image-name`, user-assigned identity + AcrPull + `acrUseManagedIdentityCreds`, CD webhook ACR, log config/tail, SSH; x86-64 only (ARM64 tidak didukung); sampel docker-django-webapp-linux | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-055 | <https://learn.microsoft.com/en-us/azure/container-apps/revisions> | Docs artikel | Revisi immutable (≤100 inactive); lifecycle status (ErrImagePull dsb. di running state); mode Single/Multiple/Labels; traffic splitting; zero-downtime; revision- vs application-scope changes; revision suffix | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-056 | <https://learn.microsoft.com/en-us/azure/container-apps/environment> | Docs artikel | Environment = secure boundary (VNet + Log Analytics bersama); tipe Workload profiles (default) vs Consumption only; kebijakan auto-delete 90 hari idle | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-057 | <https://learn.microsoft.com/en-us/azure/container-apps/get-started-existing-container-image> | Docs quickstart | Extension `containerapp` + register provider; `az containerapp env create`; `az containerapp create` (publik/registry privat + Key Vault untuk password registry); verifikasi via query `ContainerAppConsoleLogs_CL` | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-058 | <https://learn.microsoft.com/en-us/azure/container-apps/logging> | Docs artikel | Tiga kategori log (console/system/HTTP opt-in); daftar pesan system logs termasuk `Error provisioning revision. ErrorCode: ErrImagePull|Timeout|ContainerCrashing` | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-059 | <https://learn.microsoft.com/en-us/azure/container-apps/log-streaming> | Docs artikel | `az containerapp logs show` (`--type system|console`, `--tail` 0–300, `--follow`, `--revision/--replica/--container`); `az containerapp env logs show`; `az containerapp revision list` / `replica list` | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-060 | <https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli> | Docs quickstart | `az aks create` (default 3 node; system-assigned identity), nodepool add `--mode User`, `get-credentials`, manifest lengkap (probes startup/readiness/liveness, initContainer `nc -zv`, nodeSelector, requests/limits), `kubectl apply`, uji LoadBalancer IP + curl, dua resource group | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-061 | <https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration> | Docs artikel | `--attach-acr`/`--detach-acr` → AcrPull ke kubelet identity; **caveat ABAC: tidak didukung — pakai Container Registry Repository Reader manual**; image pull secret utk registry eksternal; `az acr import`; `az aks check-acr`; cleanup termasuk RG `MC_*`; CLI ≥ 2.7.0 | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-062 | <https://learn.microsoft.com/en-us/azure/aks/events> | Docs artikel | Kubernetes events: **retensi hanya 1 jam** (Container insights utk lebih lama); Warning vs Normal (FailedScheduling/CrashLoopBackoff); `kubectl get events` + filter namespace; `kubectl describe pod`; Portal Events | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-063 | <https://learn.microsoft.com/en-us/azure/aks/monitor-aks> | Docs artikel | Container insights (stdout/stderr + events → Log Analytics; live data = `kubectl logs -c`/`top pods`; log di `/var/log/containers`); control plane logs via diagnostic settings (tabel AKSAudit/AKSAuditAdmin/AKSControlPlane); peringatan biaya `kube-audit` + rekomendasi kube-audit-admin/Basic logs; baseline AKS Automatic | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-064 | <https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/quickstart-python> | Docs quickstart | Python SDK `azure-cosmos`: CosmosClient + DefaultAzureCredential; object model; upsert/read_item (point read)/query_items berparameter; provisioning via `azd` template; Python 3.12 | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-065 | <https://learn.microsoft.com/en-us/azure/cosmos-db/index-policy> | Docs artikel | Indexing mode consistent/none; include/exclude paths + presedensi; partition key wajib diindeks; composite indexes (ORDER BY/filter, equality dulu-range terakhir); transformasi online & RU; vector indexes | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-066 | <https://learn.microsoft.com/en-us/azure/cosmos-db/consistency-levels> | Docs artikel | 5 consistency levels + semantik; session token; **RU read 2× untuk Strong/Bounded staleness**; latency write Strong multi-region; RPO per level; override default = read-only + recreate SDK instance | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-067 | <https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/vector-search> | Docs artikel | Enable `EnableNoSQLVectorSearch`; container vector policy; index flat (≤505 dim)/quantizedFlat/diskANN (≤4096 dim, **≥1.000 vektor**); `VectorDistance` + kewajiban `TOP N`; limitasi (container baru, immutable, no shared throughput) | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-068 | <https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/change-feed-pull-model> | Docs artikel | Processor vs pull model (lease vs continuation token; filter partition key hanya pull); Python `query_items_change_feed`; token via `last_response_headers['etag']`; HTTP 304 vs 200-kosong; AllVersionsAndDeletes ≥4.9.1b1 | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-069 | <https://learn.microsoft.com/en-us/azure/cosmos-db/request-units> | Docs artikel | RU = mata uang performa; point read 1 KB ≈ 1 RU; faktor biaya (indexed properties, konsistensi 2×, point read < query, kompleksitas query); mode provisioned/serverless/autoscale; RU × region | Not shown | 2026-07-15 | Primary | — | OK |
| SRC-070 | <https://learn.microsoft.com/en-us/azure/cosmos-db/how-to-python-vector-index-query> | Docs artikel | Python vector: `vector_embedding_policy`, indexing policy dengan **exclude path vector** (peringatan RU insert), `create_container_if_not_exists(..., vector_embedding_policy=...)`, query `VectorDistance` berparameter | Not shown | 2026-07-15 | Primary | — | OK |

**Sumber yang sengaja TIDAK digunakan:** konten Microsoft Q&A (`learn.microsoft.com/answers/...`) yang membahas status beta AI-200 ditemukan selama audit, tetapi dikecualikan dari bukti sesuai kebijakan sumber prompt (bukan konten editorial resmi Microsoft). Tidak ada exam dump, blog pribadi, forum, atau sumber pihak ketiga yang digunakan.

---

## 10. Change Log

| Tanggal | Perubahan | Alasan | Source ID |
|---|---|---|---|
| 2026-07-15 | Repositori dibuat; README induk disusun (audit, peta domain, coverage matrix 27 bullet, ledger 38 sumber) | Eksekusi TAHAP 1–3 prompt kurikulum | SRC-001…SRC-038 |
| 2026-07-15 | Status exam ditetapkan **Transitional/Unresolved** — bukan mewarisi baseline; hasil triangulasi: tidak ada pernyataan GA eksplisit; catatan/absennya Practice Assessment diperlakukan sebagai **sinyal pendukung saja** (kompatibel dengan "masih beta" maupun "baru keluar beta"); bagian exam-details tidak dapat diperiksa (client-side) | Protokol status beta/live/GA (triangulasi, tanpa memaksa kesimpulan biner; tanpa sinyal tunggal) | SRC-001, SRC-015, SRC-020, SRC-021 |
| 2026-07-15 | Baseline "bahasa exam English" dan "assessment time 120 minutes" diturunkan menjadi **Needs Review** — tidak dapat dikonfirmasi ulang karena bagian tersebut dirender client-side | Protokol verifikasi #11 (konten dinamis → Needs Review); larangan mewarisi baseline tanpa validasi | SRC-001, SRC-007 |
| 2026-07-15 | Baseline "AI-200 = replacement path Azure Developer Associate" diturunkan menjadi **BELUM DAPAT DIVERIFIKASI** dari halaman yang dapat diakses — halaman AZ-204 tidak menyebut pengganti; blog rujukan tidak dapat diakses (403) | Halaman dibuka langsung; klaim tidak ditemukan pada konten yang dapat diambil | SRC-004, SRC-021 |
| 2026-07-15 | Konfirmasi ulang: AZ-204 retire 31 Juli 2026 (masih aktif per tanggal audit); domain & bobot AI-200 tidak berubah dari baseline; struktur starter 13 file dipertahankan | Validasi baseline terhadap sumber terbaru | SRC-002, SRC-004, SRC-005, SRC-006 |
| 2026-07-15 | Dicatat: study guide "Find documentation" masih menaut Azure Cache for Redis, sementara skills measured menyebut Azure Managed Redis; kurikulum mengikuti skills measured dan hub `/azure/redis/` | Menjaga pemisahan produk Azure Managed Redis vs Azure Cache for Redis | SRC-002, SRC-029 |
| 2026-07-15 | Revisi pasca review eksternal: (1) status dipisah menjadi **Lifecycle status** vs **Operational availability**; (2) narasi Practice Assessment dipertegas sebagai sinyal pendukung yang kompatibel dua arah; (3) guardrail Service Bus diperbaiki — DLQ adalah subqueue bawaan queue/subscription, bukan fitur tier; (4) prinsip "security & observability sejak lab pertama" ditambahkan ke Strategi Belajar; (5) kolom **Source readiness** ditambahkan ke coverage matrix; (6) aturan artikel-spesifik untuk modul detail dieksplisitkan | Review eksternal 2026-07-15; poin diverifikasi ulang ke sumber resmi sebelum diadopsi | SRC-039 (baru), SRC-002, SRC-016 |
| 2026-07-15 | Klaim faktual review eksternal (bahasa **English**, assessment time **120 minutes**, scheduling tersedia, study guide last updated **May 5, 2026**) **TIDAK diadopsi sebagai fakta** — dicatat sebagai "laporan eksternal, menunggu konfirmasi" karena tetap tidak dapat diverifikasi dari halaman resmi yang dibuka oleh environment ini | Kebijakan sumber Microsoft-only; larangan mengadopsi klaim tanpa membuka halaman resmi | SRC-001, SRC-002, SRC-007, SRC-016 |
| 2026-07-15 | Modul pertama dibuat: **d1-01-azure-container-registry.md** (Draft, menunggu review). 10 artikel spesifik ACR diverifikasi dan ditambahkan ke ledger (SRC-040–SRC-049); coverage matrix baris #1–2 → `Draft` dengan `Implementation sources verified` | Eksekusi TAHAP 5 iterasi pertama setelah README disetujui | SRC-040–SRC-049 |
| 2026-07-15 | Modul kelima dibuat: **d2-01-cosmos-db-nosql.md** (Draft; sesuai arahan user, review menyeluruh dilakukan di akhir). 7 artikel baru diverifikasi (SRC-064–SRC-070); coverage matrix #8–#11 → `Draft`/`Implementation sources verified`. Catatan verifikasi penting: vector policy hanya untuk container baru & immutable; quantizedFlat/diskANN butuh ≥1.000 vektor; change feed processor = .NET/Java — Python resmi memakai pull model (`query_items_change_feed`) | Eksekusi TAHAP 5 iterasi kelima — mulai Domain 2 | SRC-064–SRC-070 |
| 2026-07-15 | Modul keempat dibuat: **d1-04-azure-kubernetes-service.md** (Draft, menunggu review; d1-03 disetujui user). 4 artikel baru diverifikasi (SRC-060–SRC-063); coverage matrix #6 → `Draft`/`Implementation sources verified`; **#7 kini lengkap dua sisi (Container Apps + AKS)** → `Implementation sources verified`. Catatan verifikasi penting: `--attach-acr` tidak didukung registry ABAC-enabled (wajib role Container Registry Repository Reader manual); retensi Kubernetes events hanya 1 jam | Eksekusi TAHAP 5 iterasi keempat — Domain 1 selesai draft | SRC-060–SRC-063 |
| 2026-07-15 | Modul ketiga dibuat: **d1-03-azure-container-apps-keda.md** (Draft, menunggu review; d1-02 disetujui user). 5 artikel baru diverifikasi (SRC-055–SRC-059) + SRC-025 diperkaya; coverage matrix #4–#5 → `Draft`/`Implementation sources verified`; #7 → `Draft` sebagian (bagian Container Apps; bagian AKS menyusul di d1-04). Validasi end-to-end KEDA `azure-servicebus` dijadwalkan bersama lab d3-01 | Eksekusi TAHAP 5 iterasi ketiga | SRC-025, SRC-055–SRC-059 |
| 2026-07-15 | Modul kedua dibuat: **d1-02-azure-app-service-container.md** (Draft, menunggu review; d1-01 disetujui user). 5 artikel spesifik App Service diverifikasi (SRC-050–SRC-054); coverage matrix baris #3 → `Draft` + `Implementation sources verified`. Catatan verifikasi: container Linux App Service wajib x86-64; Docker Compose multi-container retire 2027-03-31 (sidecar sebagai pengganti) | Eksekusi TAHAP 5 iterasi kedua | SRC-050–SRC-054 |
