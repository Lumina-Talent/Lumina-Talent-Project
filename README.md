# Lumina Talent

**Lumina Talent** adalah platform talent marketplace yang menghubungkan **freelancer digital Indonesia** dengan **klien global**. Aplikasi ini menampilkan fitur untuk kedua peran utama:
- **Freelancer**: mencari pekerjaan, melamar, mengelola profile, melihat status lamaran, menggunakan CoPilot AI, dan memantau keuangan.
- **Employer**: membuat lowongan, memverifikasi bisnis, melihat pelamar, mengelola escrow, dan berkomunikasi dengan freelancer.

## Fitur Utama

- Pendaftaran dan otentikasi pengguna dasar untuk freelancer dan employer.
- Dashboard khusus per peran:
  - Freelancer: Beranda, Profil, Status Lamaran, Keuangan, Chat, dan CoPilot.
  - Employer: Dashboard, Buat Lowongan, Verifikasi, Pelamar, Pesan, Escrow.
- Sistem escrow dengan alur konfirmasi selesai, auto-complete 72 jam, dan dukungan sengketa.
- Integrasi Azure AI untuk:
  - Matchmaking CoPilot antara lowongan dan profil freelancer.
  - Auto-draft proposal dalam Bahasa Indonesia.
  - Translasi proposal.
  - Peringkat dan sortir pelamar cerdas.
  - Pemrosesan dokumen KYC dan CV/Resume.
- Arsitektur DB simulasi dengan pemisahan tier:
  - Tier 1: Profil, lowongan, matchmaking.
  - Tier 2: Transaksi, escrow, tagihan (isolated/encrypted).
  - Tier 3: Arsip chat, log.
- Notifikasi event-driven untuk proposal, escrow, KYC, sengketa, dan pesan.

## Teknologi

- React 19
- Vite
- React Router DOM
- Azure OpenAI / Document Intelligence (simulasi frontend)
- Azure Cosmos DB / MongoDB (rujukan integrasi)
- TypeScript untuk development
- OpenAI SDK

## Struktur Proyek

- `src/`
  - `App.jsx` — komponen utama aplikasi.
  - `main.jsx` — entry point React dan provider auth.
  - `components/` — UI reusable seperti `Navbar`, `Sidebar`, `JobCard`.
  - `context/` — `AuthContext.jsx` untuk state autentikasi pengguna.
  - `hooks/` — helper navigasi dan Azure AI.
  - `pages/` — halaman untuk `auth`, `freelancer`, `employer`, dan `shared`.
  - `services/azure-api.js` — integrasi Azure API dan fallback untuk runtime browser.
- `assets/` — konfigurasi Azure, style, i18n, dan layanan API klien.
- `azure_reference_code/` — contoh referensi integrasi Azure Cosmos DB dan Document Intelligence.

## Instalasi dan Menjalankan Lokal

1. Pastikan Node.js sudah terpasang.
2. Buka terminal di folder proyek.
3. Jalankan:
   ```bash
   npm install
   ```
4. Untuk memulai server development:
   ```bash
   npm run dev
   ```
5. Akses aplikasi melalui URL yang ditampilkan oleh Vite, biasanya `http://localhost:5173`.

## Konfigurasi Azure

Aplikasi ini menggunakan `assets/azure-api.js` untuk membaca konfigurasi Azure dari:
- `window.AppConfig` di `assets/config.js`
- `localStorage`

Variabel yang dibaca antara lain:
- `AZURE_OPENAI_API_KEY`
- `AZURE_OPENAI_ENDPOINT`
- `AZURE_OPENAI_DEPLOYMENT`
- `AZURE_DOC_INTEL_KEY`
- `AZURE_DOC_INTEL_ENDPOINT`
- `AZURE_COSMOS_ENDPOINT`
- `AZURE_COSMOS_KEY`
- `AZURE_PUBSUB_URL`

> Catatan keamanan: Saat ini integrasi Azure dijalankan dari sisi klien. Untuk produksi, pindahkan semua pemanggilan ke backend agar API key tidak terekspos di browser.

## Catatan

- `package.json` menyediakan skrip standar:
  - `npm run dev` untuk development.
  - `npm run build` untuk produksi.
  - `npm run preview` untuk preview build.
- Aplikasi ini sudah menggunakan pola role-based routing dan flow KYC dasar.
- Untuk pengembangan lanjutan, lengkapi backend nyata dan endpoint Azure yang sesuai.
