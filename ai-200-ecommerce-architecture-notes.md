# Rancangan Aplikasi E-Commerce AI-Native Berbasis Azure dan AI-200

## 1. Arah yang sedang dituju Microsoft melalui AI-200

Menurut saya, Microsoft sedang mengarahkan developer menuju peran baru:

> **Cloud developer yang mampu membangun sistem bisnis berbasis AI secara production-grade, bukan sekadar developer yang bisa memanggil API model.**

Ini terlihat dari komposisi AI-200. Porsi terbesar justru berada pada container, data untuk AI, messaging, serverless, keamanan, monitoring, dan troubleshooting. Materinya mencakup Container Apps/AKS, Cosmos DB, PostgreSQL dengan `pgvector`, Redis vector search, Service Bus, Event Grid, Functions, Key Vault, OpenTelemetry, dan KQL.

### Bukan “prompt engineer certification”

AI-200 tidak terlalu menempatkan model AI sebagai pusat alam semesta. Model hanya salah satu komponen dalam sistem yang lebih besar.

Arah pemikirannya kira-kira:

```text
Model AI
   ↓
AI service / orchestration
   ↓
Data + vector database
   ↓
Business services
   ↓
Messaging dan event processing
   ↓
Security, monitoring, deployment
```

Artinya, developer harus memahami apa yang terjadi sebelum dan sesudah model dipanggil:

- Dari mana konteks dan embedding diperoleh?
- Bagaimana proses tetap berjalan saat model lambat atau gagal?
- Bagaimana workload diskalakan?
- Bagaimana data diamankan?
- Bagaimana biaya token dan latency dipantau?
- Bagaimana output AI dievaluasi dan dikendalikan?
- Bagaimana AI berkomunikasi dengan sistem bisnis tanpa merusak konsistensi transaksi?

Microsoft sendiri mendeskripsikan pemegang sertifikasi ini sebagai developer yang ikut dalam seluruh lifecycle, mulai dari requirement, desain, development, deployment, security, sampai monitoring, dengan penekanan pada backend dan scalable architecture.

### AI menjadi fitur standar aplikasi cloud

Dulu arsitektur aplikasi biasanya:

```text
Web → API → Database
```

Arah barunya menjadi:

```text
Web → API → Business Services → Data
               ↓
          AI capabilities
               ↓
      Events, embeddings, agents,
      retrieval, evaluation, monitoring
```

AI tidak lagi berdiri sebagai eksperimen terpisah. Ia masuk ke aliran bisnis utama, tetapi tidak boleh menjadi sumber kebenaran untuk transaksi penting.

### Arsitektur event-driven menjadi semakin penting

Banyak aktivitas AI tidak cocok dijalankan secara sinkron:

- membuat embedding ribuan produk,
- mengklasifikasikan ulasan,
- memperbarui rekomendasi,
- meringkas percakapan,
- menganalisis gambar produk,
- mendeteksi anomali,
- membuat deskripsi produk,
- memproses dokumen pemasok.

Karena itu AI-200 menekankan Service Bus, Event Grid, Functions, retry, dead-letter queue, dan KEDA.

### Data aplikasi menjadi “AI-ready”

AI-200 secara eksplisit menguji:

- relational data,
- document data,
- caching,
- embeddings,
- vector indexing,
- vector similarity search,
- metadata filtering,
- RAG,
- change feed.

Jadi Microsoft tampaknya ingin developer berhenti melihat database hanya sebagai tempat CRUD. Database sekarang juga menjadi mesin retrieval untuk AI.

### Python dan C# akan hidup berdampingan

Saya membaca pilihan Python dalam AI-200 sebagai sinyal bahwa Microsoft menginginkan developer Azure mampu masuk ke ekosistem AI yang lebih luas.

Namun, untuk aplikasi enterprise, saya tidak akan mengganti semua C# dengan Python.

Pembagiannya lebih masuk akal seperti ini:

| Area | Bahasa utama |
|---|---|
| Ordering, payment, inventory, basket | C#/.NET |
| Web API, BFF, business rules | C#/.NET |
| Embedding pipeline | Python |
| AI orchestration dan evaluation | Python |
| Recommendation dan experimentation | Python |
| Background AI workers | Python atau C# |
| Infrastructure orchestration lokal | .NET Aspire |
| Automation dan IaC | Bicep/Terraform + scripting |

**C# menjadi tulang punggung bisnis. Python menjadi laboratorium dan mesin AI.**

---

# 2. Rancangan e-commerce berbasis AI

Saya tidak akan membuat ulang eShop dengan menempelkan chatbot di sudut kanan bawah. Itu hanya memberi mesin tua sebuah topi futuristik.

Saya akan mengambil bounded context dan pola layanan dari eShop, lalu membangunnya sebagai **AI-native commerce platform**.

Repository eShop menggunakan services-based architecture dengan .NET Aspire. AppHost-nya mengorkestrasi Identity, Basket, Catalog, Ordering, order processor, payment processor, webhooks, mobile BFF, web application, PostgreSQL, Redis, RabbitMQ, dan integrasi OpenAI opsional.

Saya akan mempertahankan kerangka tersebut, tetapi menyesuaikannya untuk Azure dan AI-200.

## 3. Gambaran arsitektur

```text
┌─────────────────────────────────────────────────────────┐
│                     CLIENT CHANNELS                     │
│ Web App | Mobile App | Admin Portal | Partner API       │
└──────────────────────────┬──────────────────────────────┘
                           │
                 Azure Front Door + WAF
                           │
                  Azure API Management
                           │
        ┌──────────────────┴──────────────────┐
        │                                     │
  Web / Mobile BFF                      AI Gateway
      .NET/C#                          Python/FastAPI
        │                                     │
┌───────┴─────────────────┐        ┌──────────┴───────────┐
│ DOMAIN SERVICES         │        │ AI CAPABILITIES      │
│                         │        │                      │
│ Identity                │        │ Semantic search      │
│ Catalog                 │        │ Recommendations      │
│ Basket                  │        │ Shopping assistant   │
│ Ordering                │        │ Product enrichment   │
│ Inventory               │        │ Review intelligence  │
│ Payment                 │        │ Customer support     │
│ Promotion               │        │ Fraud risk scoring   │
│ Notification            │        │ AI evaluation        │
└───────────┬─────────────┘        └──────────┬───────────┘
            │                                 │
            ├──────── Azure Service Bus ──────┤
            │          Topics / Queues        │
            │          Retry / DLQ            │
            │                                 │
            ├──────── Azure Event Grid ───────┤
            │                                 │
┌───────────┴─────────────────────────────────┴───────────┐
│                       DATA LAYER                        │
│                                                       │
│ PostgreSQL + pgvector  : transaksi, katalog, embedding │
│ Azure Managed Redis    : basket, cache, hot features   │
│ Cosmos DB              : conversation, profile, events │
│ Blob Storage           : gambar, dokumen, raw dataset  │
└───────────────────────────────────────────────────────┘
                           │
┌──────────────────────────┴──────────────────────────────┐
│                 AI PLATFORM AND MODELS                  │
│ Microsoft Foundry | Azure OpenAI | Model endpoints      │
│ Prompt/version registry | Evaluation | Content safety   │
└─────────────────────────────────────────────────────────┘

Platform:
Azure Container Apps | Functions | ACR | Key Vault
App Configuration | Managed Identity | Azure Monitor
Application Insights | OpenTelemetry | Log Analytics
```

---

# 4. Domain services

## Identity Service

Tanggung jawab:

- registrasi dan login customer,
- role customer, merchant, admin, dan support,
- profil dasar pengguna,
- consent dan preferensi personalisasi,
- token dan authorization.

Saya akan memisahkan:

- customer identity,
- merchant identity,
- internal employee identity.

AI service tidak boleh membaca seluruh profil pengguna. Ia hanya menerima data minimum yang dibutuhkan, misalnya:

```json
{
  "customerSegment": "returning-customer",
  "preferredCategories": ["electronics", "books"],
  "locale": "id-ID"
}
```

Bukan seluruh record customer.

## Catalog Service

Catalog tetap menjadi pemilik:

- produk,
- SKU,
- kategori,
- brand,
- atribut,
- harga dasar,
- status produk,
- metadata gambar.

Catalog juga menyimpan embedding produk di PostgreSQL `pgvector`.

Repository eShop sendiri telah menunjukkan pola semantic catalog search, yaitu membuat embedding dari teks pencarian lalu mengurutkan produk berdasarkan cosine distance pada kolom vector.

Contoh:

```text
Query:
“sepatu lari ringan untuk jalan basah”

Keyword search:
Mungkin hanya menemukan produk dengan kata “lari”.

Semantic search:
Memahami ringan, grip, waterproof, jogging, dan running.
```

Embedding tidak dibuat ketika pengguna mencari. Embedding produk dibuat sebelumnya melalui asynchronous pipeline.

```text
ProductCreated / ProductUpdated
              ↓
       Service Bus Topic
              ↓
      Embedding Worker
              ↓
 Microsoft Foundry / model
              ↓
 PostgreSQL pgvector
```

## Basket Service

Basket saya pertahankan di Azure Managed Redis karena:

- membutuhkan akses sangat cepat,
- bersifat sementara,
- mendukung expiration,
- mudah digunakan untuk distributed session,
- cocok untuk menyimpan hasil recommendation sementara.

Basket service tidak meminta AI setiap kali halaman berubah. Recommendation dicache berdasarkan:

```text
customer + basket fingerprint + model version
```

Contoh key:

```text
recommendation:
customer-123:
basket-hash-a7f91:
model-v3
```

## Ordering Service

Ordering merupakan wilayah deterministik.

AI tidak boleh:

- menentukan bahwa pembayaran sukses,
- mengubah jumlah order,
- menentukan stok akhir,
- membatalkan pesanan sendiri,
- mengubah harga transaksi,
- membuat refund tanpa policy engine.

AI hanya boleh memberi sinyal:

```json
{
  "orderId": "ORD-10029",
  "riskScore": 0.82,
  "reasons": [
    "unusual-order-value",
    "new-device",
    "address-pattern-anomaly"
  ]
}
```

Keputusan akhir tetap dibuat oleh rule engine atau petugas fraud.

## Inventory Service

Inventory menjadi service tersendiri, tidak ditempelkan ke Catalog.

Catalog menjawab:

> Produk ini apa?

Inventory menjawab:

> Produk ini tersedia berapa?

Saat checkout:

```text
OrderSubmitted
      ↓
ReserveInventory
      ↓
InventoryReserved
      ↓
ProcessPayment
      ↓
OrderConfirmed
```

Jika payment gagal:

```text
PaymentFailed
      ↓
ReleaseInventory
```

Ini saya implementasikan sebagai saga atau process manager, bukan distributed transaction lintas database.

## Payment Service

Payment service hanya menyimpan:

- payment transaction ID,
- provider,
- status,
- amount,
- currency,
- idempotency key,
- response metadata yang aman.

Data kartu tidak masuk ke platform.

Model AI tidak menerima detail sensitif pembayaran.

---

# 5. AI capabilities

## A. Semantic product search

Ini menjadi kemampuan AI pertama karena:

- manfaatnya mudah diukur,
- risiko bisnis relatif rendah,
- cocok dengan `pgvector`,
- dapat memiliki fallback ke keyword search,
- sudah memiliki embrio implementasi di eShop.

Pipeline:

```text
User query
   ↓
Query normalization
   ↓
Embedding generation
   ↓
Vector similarity + metadata filters
   ↓
Business filtering
   ↓
Ranking
   ↓
Search results
```

Metadata filter tetap penting:

```text
semantic relevance
AND category = shoes
AND stock > 0
AND price BETWEEN 500000 AND 1500000
AND merchant_status = active
```

Vector search mencari relevansi. SQL tetap menjaga kenyataan.

## B. Recommendation engine

Saya akan memulainya secara sederhana:

```text
Recommendation score =
    semantic similarity
  + category affinity
  + basket compatibility
  + popularity
  + inventory availability
  + business campaign weight
```

Tahap pertama tidak memerlukan machine learning kompleks.

Sumber sinyal:

- product viewed,
- product added to basket,
- purchase completed,
- search performed,
- recommendation clicked,
- recommendation ignored.

Semua aktivitas dikirim sebagai events.

```text
ProductViewed
ProductSearched
BasketItemAdded
OrderCompleted
RecommendationClicked
```

Event tersebut diproses menjadi customer feature atau product feature, bukan dibaca langsung dari database transaksi setiap kali rekomendasi diminta.

## C. Shopping assistant

Shopping assistant bukan chatbot yang bebas berimajinasi. Ia adalah interface percakapan di atas business tools.

Tools yang boleh dipanggil:

```text
search_products
get_product_details
compare_products
check_inventory
get_shipping_estimate
get_active_promotions
add_item_to_basket
get_order_status
```

Alurnya:

```text
User:
“Saya butuh laptop untuk coding,
berat di bawah 1,5 kg,
budget maksimal 18 juta.”

Assistant:
1. Mengekstrak constraint.
2. Memanggil semantic product search.
3. Memfilter harga, berat, dan stok.
4. Membandingkan kandidat.
5. Menjelaskan alasan rekomendasi.
```

LLM tidak mengarang harga atau stok. Nilai tersebut selalu berasal dari tool.

Setiap jawaban menyertakan grounding:

```json
{
  "answer": "...",
  "productIds": [101, 208, 445],
  "dataTimestamp": "2026-07-21T02:15:00Z",
  "modelVersion": "shopping-assistant-v2"
}
```

## D. Product enrichment

Ketika merchant menambahkan produk:

```text
ProductSubmitted
      ↓
Content Extraction Worker
      ↓
AI menghasilkan usulan:
- judul yang lebih rapi
- kategori
- atribut
- deskripsi
- keyword
- image alt text
- potensi policy violation
      ↓
Merchant review
      ↓
Publish
```

AI menghasilkan draft, bukan langsung memublikasikan.

## E. Review intelligence

Review pipeline:

```text
ReviewSubmitted
      ↓
Content moderation
      ↓
Spam detection
      ↓
Sentiment and topic extraction
      ↓
Store review
      ↓
Update product summary
```

Contoh topik yang diekstrak:

```json
{
  "sentiment": "mixed",
  "topics": {
    "battery": "positive",
    "delivery": "negative",
    "packaging": "negative"
  }
}
```

Pengguna kemudian bisa melihat:

> “Pembeli menyukai daya tahan baterainya, tetapi beberapa melaporkan kemasan kurang aman.”

Tetap harus tersedia tautan menuju review asli.

## F. Customer-support assistant

Support assistant menggunakan RAG terhadap:

- kebijakan retur,
- warranty,
- FAQ,
- status order,
- shipment tracking,
- merchant policy.

Namun tindakan seperti refund tetap membutuhkan:

- policy validation,
- authorization,
- audit trail,
- human approval untuk nominal tertentu.

---

# 6. Data strategy

Saya tidak akan memakai semua database hanya karena semuanya muncul dalam AI-200.

## PostgreSQL + pgvector

Menjadi default untuk:

- Catalog,
- Ordering,
- Inventory,
- Payment metadata,
- Promotion,
- product embeddings.

Keunggulan rancangan ini adalah transaksi dan vector search masih dapat hidup berdekatan.

Contoh tabel sederhana:

```sql
catalog_item
------------
id
name
description
price
brand_id
category_id
attributes jsonb
embedding vector
embedding_model
embedding_updated_at
```

Embeddings harus menyimpan versi model. Jika model embedding diganti, sistem dapat melakukan re-embedding secara bertahap.

## Azure Managed Redis

Digunakan untuk:

- basket,
- distributed cache,
- rate limiting,
- session,
- query-result cache,
- short-lived recommendation,
- semantic result cache.

Redis bukan source of truth untuk order atau payment.

## Cosmos DB

Saya baru menggunakannya ketika ada kebutuhan nyata, misalnya:

- conversation threads,
- agent state,
- high-volume customer interaction events,
- denormalized customer AI profile,
- rapidly evolving JSON documents.

Change feed dapat memicu pembentukan ulang profile atau summary saat dokumen diperbarui.

## Blob Storage

Digunakan untuk:

- gambar produk,
- merchant documents,
- raw AI datasets,
- moderation evidence,
- evaluation datasets,
- generated reports.

---

# 7. Messaging strategy

## Azure Service Bus

Saya gunakan untuk workflow bisnis yang membutuhkan:

- delivery guarantee,
- ordering tertentu,
- retry,
- dead-letter queue,
- competing consumers,
- topics dan subscriptions.

Contoh topics:

```text
catalog-events
order-events
payment-events
customer-events
ai-jobs
notification-events
```

Contoh subscriptions pada `catalog-events`:

```text
embedding-generator
search-index-updater
recommendation-feature-builder
merchant-notification
analytics-exporter
```

## Azure Event Grid

Saya gunakan untuk event yang lebih bersifat pemberitahuan atau integrasi platform:

- blob uploaded,
- product image added,
- deployment event,
- webhook event,
- external system notification.

## Azure Functions

Functions cocok untuk handler kecil dan tajam:

- memproses upload gambar,
- membuat thumbnail,
- menerima webhook,
- mengirim email,
- membersihkan data sementara,
- menjalankan event transformation.

Saya tidak akan memindahkan seluruh domain service ke Functions. Kalau terlalu banyak business logic hidup di sana, arsitekturnya berubah menjadi sekawanan fungsi liar yang berlarian membawa state.

---

# 8. Hosting strategy

## Development

Untuk local development:

- .NET Aspire AppHost,
- Docker containers,
- PostgreSQL + pgvector,
- Redis,
- local event broker,
- local model atau Azure model,
- Aspire dashboard,
- OpenTelemetry.

Dengan demikian, developer dapat menjalankan seluruh sistem melalui satu entry point seperti eShop saat ini.

## Production awal

Saya akan memilih **Azure Container Apps**, bukan langsung AKS.

Services:

```text
web-bff
identity-api
catalog-api
basket-api
ordering-api
inventory-api
payment-api
ai-gateway
embedding-worker
recommendation-worker
notification-worker
```

Alasannya:

- deployment container tetap sederhana,
- revision dan traffic splitting,
- scale-to-zero untuk worker tertentu,
- KEDA untuk scaling berdasarkan queue,
- operational burden lebih rendah daripada AKS.

AKS baru dipilih apabila:

- jumlah service sangat besar,
- membutuhkan custom networking kompleks,
- memakai specialized GPU scheduling,
- memiliki platform engineering team,
- membutuhkan service mesh atau custom operators,
- Container Apps sudah menjadi batas teknis nyata.

---

# 9. Security dan observability

## Security baseline

Setiap service menggunakan:

- managed identity,
- Key Vault untuk secrets,
- App Configuration untuk configuration dan feature flags,
- private endpoints untuk layanan data sensitif,
- least-privilege access,
- separate identity per service,
- encryption in transit dan at rest,
- API authorization berdasarkan scope.

Tidak ada API key model yang ditaruh di source code atau environment file production.

## AI-specific security

Tambahan pengamanan:

- prompt-injection filtering,
- tool allowlist,
- parameter validation sebelum tool invocation,
- PII redaction,
- content moderation,
- token dan request limits,
- conversation retention policy,
- audit log untuk tool calls,
- pemisahan trusted instructions dan user input.

## Observability

Setiap request membawa correlation ID:

```text
Browser
  → BFF
  → Catalog
  → AI Gateway
  → Model endpoint
  → PostgreSQL
  → Service Bus
  → Worker
```

Yang saya ukur:

| Area | Metrik |
|---|---|
| API | latency, error rate, throughput |
| Database | query latency, connections, locks |
| Messaging | queue depth, retry, DLQ |
| AI | token usage, model latency, failure rate |
| Search | zero-result rate, click-through rate |
| Recommendation | conversion uplift, acceptance rate |
| Assistant | tool-call success, grounded-answer rate |
| Cost | cost per search, chat, order, dan customer |

Distributed tracing menggunakan OpenTelemetry, sedangkan log dan metrics dianalisis melalui Azure Monitor, Application Insights, Log Analytics, dan KQL.

---

# 10. Struktur repository

Saya akan menggunakan monorepo pada tahap awal:

```text
src/
├── AppHost/
├── ServiceDefaults/
│
├── WebApp/
├── WebBff/
├── MobileBff/
│
├── Services/
│   ├── Identity/
│   ├── Catalog/
│   ├── Basket/
│   ├── Ordering/
│   ├── Inventory/
│   ├── Payment/
│   ├── Promotion/
│   └── Notification/
│
├── AI/
│   ├── Gateway/
│   ├── SemanticSearch/
│   ├── Recommendation/
│   ├── ShoppingAssistant/
│   ├── ProductEnrichment/
│   ├── Evaluation/
│   └── Shared/
│
├── Workers/
│   ├── EmbeddingWorker/
│   ├── RecommendationWorker/
│   ├── ReviewWorker/
│   └── NotificationWorker/
│
├── BuildingBlocks/
│   ├── EventBus/
│   ├── Observability/
│   ├── Security/
│   ├── Idempotency/
│   └── Resilience/
│
└── Contracts/
    ├── Events/
    ├── APIs/
    └── Schemas/

infra/
├── bicep/
│   ├── modules/
│   └── environments/
├── container-apps/
├── monitoring/
└── dashboards/

tests/
├── UnitTests/
├── IntegrationTests/
├── ContractTests/
├── FunctionalTests/
├── LoadTests/
├── AIQualityTests/
└── E2ETests/
```

AI evaluation diperlakukan sebagai testing sungguhan:

```text
Input dataset
     ↓
Expected constraints
     ↓
Prompt/model execution
     ↓
Groundedness check
Safety check
Tool-call correctness
Latency check
Cost check
     ↓
Deployment gate
```

---

# 11. Tahapan implementasi

## Fase 1, Commerce foundation

Bangun:

- Identity,
- Catalog,
- Basket,
- Ordering,
- Inventory,
- Payment abstraction,
- Service Bus,
- PostgreSQL,
- Redis,
- observability,
- CI/CD.

Belum ada agent.

## Fase 2, Search intelligence

Tambahkan:

- embedding pipeline,
- `pgvector`,
- semantic search,
- fallback keyword search,
- query analytics,
- evaluation dataset.

Ini adalah AI MVP yang paling sehat.

## Fase 3, Recommendation

Tambahkan:

- interaction events,
- recommendation worker,
- recommendation API,
- caching,
- A/B testing,
- conversion measurement.

## Fase 4, Shopping assistant

Tambahkan:

- AI Gateway,
- tool calling,
- product comparison,
- basket integration,
- grounded responses,
- prompt-injection protection.

## Fase 5, Merchant dan support AI

Tambahkan:

- product enrichment,
- review summarization,
- support assistant,
- document retrieval,
- human approval workflows.

## Fase 6, Advanced intelligence

Baru kemudian mempertimbangkan:

- multimodal product search,
- demand forecasting,
- dynamic merchandising,
- anomaly detection,
- fraud scoring,
- personalized storefront,
- multi-agent workflows.

---

# Kesimpulan

Arah Microsoft melalui AI-200 menurut saya adalah:

> **Mengubah Azure developer menjadi AI cloud application developer yang memahami container, data, vector retrieval, messaging, serverless, security, dan observability sebagai satu kesatuan.**

Untuk e-commerce, saya akan menggunakan:

- **.NET/C# sebagai transactional commerce core**,
- **Python sebagai AI execution dan experimentation layer**,
- **PostgreSQL + pgvector sebagai fondasi data dan semantic retrieval**,
- **Redis untuk basket dan high-speed cache**,
- **Service Bus dan Event Grid sebagai sistem saraf**,
- **Container Apps sebagai runtime awal**,
- **Microsoft Foundry/Azure OpenAI sebagai model platform**,
- **OpenTelemetry dan Azure Monitor sebagai kotak hitam pesawatnya**.

Prinsip terpentingnya:

> **AI boleh memberi saran, mencari, merangkum, mengklasifikasikan, dan mengorkestrasi. Tetapi harga, stok, pembayaran, order, refund, dan authorization harus tetap dikendalikan oleh layanan bisnis yang deterministik.**

Dengan pendekatan tersebut, hasilnya bukan sekadar “eShop plus chatbot”, melainkan **commerce platform yang sejak awal dirancang agar AI dapat masuk dengan aman, terukur, dapat diganti, dan tidak mengambil alih kunci kasir.**
