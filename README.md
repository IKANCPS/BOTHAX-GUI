# 📖 Panduan Lengkap ImGui untuk Lua


<!-- Ganti URL di atas dengan link gambar Anda. Anda bisa upload gambar ke imgur.com -->

Selamat datang di panduan lengkap penggunaan ImGui dengan Lua! Dokumentasi ini dirancang untuk membantu Anda, mulai dari pemula hingga pengguna mahir, dalam membuat antarmuka grafis (GUI) yang fungsional dan menarik.

Panduan ini dibuat berdasarkan file `IMGUI.txt` yang berisi daftar lengkap fungsi, namun disajikan dengan cara yang lebih terstruktur, dengan penjelasan dan contoh kode yang mudah diikuti.

---

### **🔗 Link Penting & Komunitas**

> [💬 **Bergabung dengan Komunitas Discord Kami!**](https://discord.gg/your-invite-code)
> <!-- Ganti dengan link invite Discord Anda -->
>
> Dapatkan bantuan, bagikan proyek Anda, atau sekadar mengobrol dengan sesama developer.

> [📄 **Unduh File Referensi `IMGUI.txt`**](./IMGUI.txt)
> <!-- Link ini akan berfungsi jika IMGUI.txt ada di folder yang sama dengan file MD ini. -->
>
> Lihat daftar fungsi asli yang menjadi dasar dari panduan ini.

---

### **📋 Daftar Isi (Table of Contents)**

1.  [**Bab 1: Persiapan dan Window Pertama Anda**](#bab-1-persiapan-dan-window-pertama-anda)
    -   Memahami 'Hook' (`OnDraw`)
    -   Membuat Window dengan `ImGui.Begin` & `ImGui.End`
2.  [**Bab 2: Widget Dasar (The Essentials)**](#) <!-- Akan kita isi nanti -->
3.  [**Bab 3: Input dari Pengguna (User Input)**](#) <!-- Akan kita isi nanti -->
4.  [**Bab 4: Tata Letak dan Posisi (Layouting)**](#) <!-- Akan kita isi nanti -->
5.  ... dan seterusnya.

---

## Bab 1: Persiapan dan Window Pertama Anda

Sebelum kita bisa menampilkan tombol, slider, atau teks, kita perlu menyiapkan "kanvas" tempat semuanya akan digambar. Di sinilah kita akan belajar tentang **hook** dan cara membuat **window** pertama kita.

### Langkah A: Memahami 'Hook'

ImGui perlu digambar setiap frame. Untuk melakukan ini, kita perlu "menumpang" pada proses render game/aplikasi. Ini dilakukan menggunakan sebuah *hook* ke fungsi `OnDraw` atau `draw`.

Semua kode ImGui Anda **wajib** berada di dalam fungsi callback dari hook ini.

**Struktur Dasar:**
```lua
-- Nama hook bisa 'OnDraw', 'draw', atau nama lain tergantung platform Anda.
-- "MyImGuiMenu" adalah nama unik untuk hook Anda.
AddHook("OnDraw", "MyImGuiMenu", function()
    -- Semua kode ImGui Anda akan ditulis di sini
end)
