# 🎨 Panduan ImGui Lua Lengkap (B'Internal Version)
### Dari Nol Sampai Jago! 🚀

![Banner Keren Anda](https://via.placeholder.com/900x300.png?text=Taruh+Gambar+Keren+Kamu+Di+Sini!)

Halo semua! Selamat datang di panduan ImGui untuk Lua.

Dokumentasi ini dibuat khusus buat kalian yang mau belajar bikin UI (User Interface) keren pakai ImGui, tapi mungkin bingung mau mulai dari mana. Tenang aja, kita bakal bahas semuanya pelan-pelan, dari yang paling dasar sampai fitur-fitur yang lebih canggih.

Gak perlu takut, semuanya dijelasin pake bahasa yang santai dan contoh yang gampang dimengerti. Yuk, kita mulai!

---

## 💬 Gabung Komunitas Kita!

Punya pertanyaan, nemu masalah, atau cuma mau pamer hasil karyamu? Langsung aja gabung ke server Discord kita! Di sana banyak teman-teman yang siap bantu dan diajak ngobrol.

**[>> Klik di sini untuk gabung Discord! <<](https://discord.gg/GANTI_DENGAN_LINK_INVITE_KAMU)**

## 📚 Sumber Daya & Referensi

Panduan ini adalah versi "manusiawi" dari file dokumentasi mentah `IMGUI.txt`. Kalau kamu tipe yang suka lihat daftar lengkap semua fungsi tanpa banyak penjelasan, kamu bisa download filenya di bawah ini.

**[📥 Download IMGUI.txt (Referensi Cepat)](LINK_KE_FILE_IMGUI.TXT_DI_GITHUB_KAMU)**

---

## ✨ Langkah Pertama: "Hello, ImGui!"

Oke, cukup basa-basinya, ayo kita mulai ngoding!

Hal pertama yang wajib kamu tahu adalah ImGui perlu "digambar" setiap frame. Di lingkungan scripting kita, ini biasanya dilakukan di dalam sebuah *hook* bernama `OnDraw` atau `draw`. Anggap saja ini adalah kanvas kosong yang diberikan ke kamu setiap detik untuk digambar.

**Struktur dasarnya selalu seperti ini:**

```lua
-- Nama hook bisa 'OnDraw' atau 'draw', tergantung platform-nya
AddHook("OnDraw", "MyFirstImGui", function()
    -- Semua kode ImGui kamu ditaruh di sini!
end)
