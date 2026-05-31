# VERTEX HUB 🚀

**VERTEX HUB** adalah launcher script dengan antarmuka GUI elegan, animasi splash screen full layar, dan daftar script bawaan yang dapat dijalankan dengan satu klik – GUI akan menutup otomatis.

![Version](https://img.shields.io/badge/version-1.0.0-blue)

## ✨ Fitur

- **Splash Screen Full Layar** – Animasi masuk dengan teks besar "VERTEX HUB" dan indikator "Loading..." di kanan bawah selama 5 detik.
- **GUI Compact** – Ukuran 280x350, dapat digeser (draggable), tanpa tombol close (lebih simpel).
- **Animasi Tombol** – Tombol script muncul satu per satu dalam waktu 1 detik dengan efek fade-in & scale-up.
- **Auto Close** – Setelah mengklik salah satu script, GUI akan langsung tertutup otomatis.
- **4 Script Bawaan** (langsung dari repository GitHub):
  - [🌍] Guess My Country!
  - [OG] Last Letter
  - Stop The Timer
  - Sambung Kata ID

## 📦 Cara Penggunaan

1. **Salin seluruh kode** dari `vertexhub.lua`.
2. **Tempelkan kode** ke executor yang Anda gunakan.
3. **Jalankan script** – akan muncul splash screen selama 5 detik.
4. Setelah splash selesai, GUI utama akan muncul dengan 4 tombol script.
5. **Klik tombol script** yang ingin dijalankan – script akan dieksekusi dan GUI akan otomatis tertutup.

> **Catatan**: Pastikan koneksi internet stabil karena script akan mengambil file dari GitHub menggunakan `game:HttpGet()`.

## 🎨 Penyesuaian Tampilan (Opsional)

Jika ingin mengubah ukuran GUI atau durasi splash, edit nilai berikut di dalam kode:
- **Ukuran GUI**: `mainFrame.Size = UDim2.new(0, 280, 0, 350)` (lebar, tinggi)
- **Durasi Splash**: angka `5.0` pada `task.wait(5.0)`
- **Kecepatan animasi tombol**: ubah `interval = 1.0 / totalButtons`

## ⚠️ Catatan Penting

- Executor yang digunakan harus mendukung `game:HttpGet` dan `loadstring`.
- URL GitHub yang digunakan sudah fix mengarah ke repository. Jangan ubah kecuali Anda mengganti script.
- Jika terjadi error "Gagal menjalankan script", periksa koneksi internet dan pastikan URL raw GitHub masih valid.

## 📄 Lisensi

Script ini dibuat untuk keperluan edukasi dan penggunaan pribadi. Gunakan dengan bijak sesuai aturan permainan yang Anda mainkan.

---

**Dibuat untuk VERTEX HUB**
