# WAD Task Manager - Frontend

Frontend aplikasi manajemen tugas (Task Manager) yang dikembangkan dengan **React**, **Vite**, dan **Tailwind CSS**. Aplikasi ini terhubung dengan backend REST API (Express + Prisma) dan mendukung fitur real-time menggunakan **Socket.IO**.

## Fitur Utama

- 🎨 **UI Modern & Premium**: Menggunakan Tailwind CSS dengan gaya *Glassmorphism* dan animasi yang mulus.
- 🔐 **Autentikasi Aman**: Login berbasis JWT Access Token & Refresh Token (mendukung enkripsi Argon2 di sisi backend).
- ⚡ **Real-time Sync**: Sinkronisasi data seketika antar perangkat berkat integrasi WebSocket (Socket.IO).
- 📋 **Manajemen Tugas Lengkap**: Membuat, mengedit, memfilter, dan menghapus tugas dengan mudah.

## Persyaratan (Prerequisites)

Pastikan sistem Anda telah menginstal:
- [Node.js](https://nodejs.org/) (disarankan versi 18 atau terbaru)
- Backend **WAD Task Manager** (terletak di folder terpisah, contoh: `wadv-capstone`) harus sudah berjalan.

## Menjalankan Backend Terlebih Dahulu

Agar frontend dapat bekerja dengan baik, **Backend** (Express + MySQL) harus dinyalakan di `localhost:3000`. Berikut adalah ringkasan cara menjalankan backend (sesuaikan dengan lokasi folder backend Anda):

```bash
# Pindah ke folder backend
cd path/to/wadv-capstone

# Install dependensi backend
npm install

# Push skema database Prisma (pastikan MySQL menyala di XAMPP/Laragon)
npx prisma db push

# Jalankan seeder agar data awal (termasuk user Admin) terbentuk
npx prisma db seed

# Jalankan server backend (biasanya di port 3000)
npm run dev
```

*Kredensial Seed Default Backend:*
- Admin: `admin@example.com` / `admin123`
- User: `budi@example.com` / `password123`

---

## Cara Instalasi & Menjalankan Frontend

Jika backend sudah berjalan di port 3000, ikuti langkah berikut untuk menjalankan frontend:

### 1. Clone atau Unduh Repositori
Pindahkan terminal Anda ke folder tempat frontend akan disimpan, lalu clone project ini:

```bash
git clone <url-repository-frontend-anda> wadv-frontend
cd wadv-frontend
```

*(Jika Anda sudah berada di dalam folder `wadv-frontend`, lewati perintah `git clone`)*

### 2. Install Dependensi

Jalankan perintah berikut untuk mengunduh semua *package* (React, Axios, Tailwind, Lucide, dll):

```bash
npm install
```

### 3. Konfigurasi Proxy (Otomatis)

Frontend ini dikonfigurasi melalui Vite (lihat `vite.config.js`) untuk mem-forward seluruh request API secara otomatis ke `http://localhost:3000`. Oleh karena itu, **Anda tidak perlu membuat file `.env` khusus** selama backend berjalan di port standar (3000).

### 4. Menjalankan Server Pengembangan (Dev Server)

Jalankan perintah:

```bash
npm run dev
```

Terminal akan menampilkan URL lokal (contoh: `http://localhost:5173/`).
Buka URL tersebut di browser Anda untuk melihat aplikasi WAD Task Manager.

---

## Struktur Folder Utama

```text
wadv-frontend/
├── src/
│   ├── components/    # Komponen Reusable UI (Navbar, TaskCard, TaskForm)
│   ├── contexts/      # State Management Global (Auth, Socket, Notif)
│   ├── hooks/         # Custom React Hooks
│   ├── lib/           # Konfigurasi Library pihak ketiga (Axios dengan interceptor)
│   ├── pages/         # Halaman Utama (Login, Register, Tasks, Profile)
│   ├── services/      # Fungsi khusus pemanggilan API (task.service.js)
│   ├── App.jsx        # Root dan Routing Aplikasi
│   └── index.css      # Konfigurasi utama Tailwind CSS
├── postcss.config.js  # Konfigurasi PostCSS
├── tailwind.config.js # Tema & Konfigurasi warna Tailwind CSS
└── vite.config.js     # Konfigurasi Vite & API Proxy
```

## Teknologi yang Digunakan

- [React 19](https://react.dev/)
- [Vite](https://vitejs.dev/)
- [Tailwind CSS v3](https://tailwindcss.com/)
- [React Hook Form](https://react-hook-form.com/)
- [Lucide React](https://lucide.dev/)
- [Axios](https://axios-http.com/)
- [Socket.IO Client](https://socket.io/)
