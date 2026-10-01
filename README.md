Berikut gambar Workflownya
<img width="818" height="323" alt="image" src="https://github.com/user-attachments/assets/f3986cbb-5866-4bae-b25b-dc9374b2d764" />

Link Workflownya 
https://bagussujatmiko.app.n8n.cloud/workflow/lFlLnASBQtwn0MyE?projectId=1IzfW1cdEl0LEU2H

# 🤖 ZANBAS - CS & Sales Lead Automation with n8n & Google Gemini AI

Sistem otomatisasi *Customer Service* dan manajemen *leads* penjualan 24/7 untuk produk digital brand **ZANBAS**. Berbasis **n8n**, **Telegram Bot**, **Google Gemini AI Agent**, dan terintegrasi langsung dengan **Google Sheets** serta sistem *Knowledge Base* (RAG Vector Store)[cite: 3].

---

## 📌 Latar Belakang Masalah & Urgensi

* **Kebocoran Leads dari Iklan IG**: Pesan masuk dari *campaign* iklan Instagram sering kali terlambat dibalas di luar jam kerja, menyebabkan potensi pembeli hilang[cite: 3].
* **Pertanyaan Berulang (FAQ)**: Staf CS menghabiskan banyak waktu hanya untuk membalas pertanyaan dasar yang sama (harga, cara bayar, akses), memicu kelelahan (*burnout*)[cite: 3].
* **Pencatatan Data Manual**: Penanganan status prospek secara manual rentan *human error* dan tidak terorganisir[cite: 3].

### 💡 Solusi & Manfaat Bisnis
1. **Respon Instan 24/7**: Balasan akurat dalam hitungan detik tanpa tergantung jam kerja staf[cite: 3].
2. **Penghematan Efisiensi**: Mengurangi beban kerja rutin staf CS hingga 80%[cite: 3].
3. **Pencatatan Real-time**: Mengidentifikasi dan mencatat status minat pembeli (`MAU_BELI`, `BELUM_JAWAB`, `TIDAK_MAU_BELI`) otomatis ke Google Sheets.
4. **Meningkatkan Konversi**: Mengarahkan pembeli potensial langsung ke link pemesanan terpusat[cite: 3].

---

## 🛠️ Teknologi yang Digunakan

* **Workflow Orchestrator**: [n8n](https://n8n.io/)[cite: 3]
* **Messaging Platform**: Telegram Bot API[cite: 3]
* **AI & Machine Learning Engine**: Google Gemini Chat Model (`gemini-3.1-flash`)
* **Embeddings**: Google Gemini Embeddings[cite: 3]
* **Database & Knowledge Base**: Simple Vector Store (RAG) & Google Sheets[cite: 3]

---

## 📐 Arsitektur Workflow n8n

Workflow terdiri dari dua bagian utama:

### 1. Load Data Flow (Knowledge Base Ingestion)
Memuat dokumen FAQ produk ke dalam memori *Vector Store*[cite: 3].
* **`Upload FAQ TXT`** *(Trigger)*: Pintu masuk pengunggahan file dokumen `.txt`.
* **`Default Data Loader - TXT`**: Membaca teks mentah dokumen.
* **`Recursive Character Text Splitter`**: Memecah dokumen menjadi potongan-potongan informasi kecil (*chunks*)[cite: 3].
* **`Embeddings Google Gemini`**: Mengubah teks menjadi format vektor numerik[cite: 3].
* **`Insert FAQ ke Simple Vector Store`**: Menyimpan data vektor ke memori n8n[cite: 3].

### 2. Main AI Conversation Workflow
Berjalan otomatis setiap ada chat masuk dari pelanggan.
* **`Telegram Trigger`** *(Trigger Utama)*: Menangkap pesan masuk di Telegram[cite: 3].
* **`AI Agent`** *(Core Engine)*: Pengendali logika, konteks, dan panggilan *tools*.
* **`Google Gemini Chat Model`**: LLM pemroses percakapan[cite: 3].
* **`Simple Memory`**: Menyimpan riwayat obrolan agar percakapan tetap kontekstual[cite: 3].
* **`Send a text message`**: Mengirim balasan teks & link pemesanan kembali ke Telegram[cite: 3].

### 🛠️ Sub-Nodes (Tools Integration)
* **`Query Data Tool`**: Mengambil jawaban relevan dari *Vector Store* FAQ[cite: 3].
* **`ambil_semua_data_produk`**: Membaca katalog dan promo aktif dari Google Sheets[cite: 3].
* **`catat_status`**: Menambahkan baris data status pelanggan (`nama`, `no_hp`, `produk`, `status`) ke Google Sheets.

---

## 🚀 Alur Kampanye Penjualan (Inbound Lead)

1. **Trigger Instagram Ads**: Calon pembeli mengklik link promo di Instagram[cite: 3].
2. **Pre-filled Message Telegram**:
   > *"Halo Kak! Saya lihat iklan Lisensi Cloud Storage Team (1 Tahun) di Instagram."*[cite: 3]
3. **Eksekusi AI Agent**: AI mengidentifikasi minat produk, mengecek data FAQ/Sheets, mencatat status `MAU_BELI`, dan membalas dengan link Google Form checkout[cite: 3].

