# Imgui_B-internal.md

# Referensi Lengkap ImGui untuk Lua (B'internal)

Selamat datang di dokumentasi ImGui untuk Lua! Dokumen ini adalah versi yang disempurnakan dari dokumentasi yang digenerasi secara otomatis, dengan tujuan agar lebih mudah dibaca, dipahami, dan digunakan.

Di sini Anda akan menemukan contoh penggunaan dari tingkat dasar hingga lanjut, serta referensi lengkap untuk semua fungsi dan konstanta (enum) yang tersedia.

**Sumber Data:** Dokumen ini dibuat berdasarkan file `IMGUI.txt` yang digenerasi pada `2025-08-17`.

---

## Daftar Isi
1.  [🚀 Contoh Penggunaan](#-contoh-penggunaan)
    *   [Tingkat Dasar: Jendela & Widget Umum](#tingkat-dasar-jendela--widget-umum)
    *   [Tingkat Menengah: Layout, Input & Popup](#tingkat-menengah-layout-input--popup)
    *   [Tingkat Lanjut: Styling, Tabel & Custom Drawing](#tingkat-lanjut-styling-tabel--custom-drawing)
2.  [🔍 Referensi Fungsi Lengkap](#-referensi-fungsi-lengkap)
    *   [Daftar Fungsi Berdasarkan Kategori](#daftar-fungsi-berdasarkan-kategori)
3.  [🗂️ Referensi Enum & Tabel](#-referensi-enum--tabel)
    *   [Daftar Enum & Tabel yang Tersedia](#daftar-enum--tabel-yang-tersedia)
4.  [🌐 Fungsi Global](#-fungsi-global)

---

## 🚀 Contoh Penggunaan

Berikut adalah contoh-contoh praktis untuk membantu Anda memulai dengan cepat.

### Tingkat Dasar: Jendela & Widget Umum

Ini adalah contoh paling fundamental: cara membuat jendela dan menempatkan beberapa widget dasar di dalamnya.

```lua
-- Pastikan variabel ini dideklarasikan di luar loop utama Anda
-- agar nilainya tetap tersimpan antar frame.
local counter = 0
local my_checkbox_value = false
local my_slider_value = 50.0

-- Di dalam loop render utama Anda:
if ImGui.Begin("Jendela Contoh Dasar") then
    -- 1. Menampilkan teks sederhana
    ImGui.Text("Halo, ini adalah jendela ImGui pertama Anda!")
    ImGui.Separator() -- Garis pemisah

    -- 2. Tombol (Button) yang menambah counter saat diklik
    if ImGui.Button("Klik Saya!") then
        counter = counter + 1
    end
    ImGui.SameLine() -- Menempatkan widget berikutnya di baris yang sama
    ImGui.Text(string.format("Tombol telah diklik %d kali", counter))

    -- 3. Kotak Centang (Checkbox)
    -- Fungsi Checkbox mengembalikan nilai baru dan status perubahan.
    local changed
    my_checkbox_value, changed = ImGui.Checkbox("Aktifkan Opsi Ini", my_checkbox_value)
    if changed then
        -- Lakukan sesuatu jika status checkbox berubah
        print("Status checkbox berubah menjadi:", my_checkbox_value)
    end

    -- 4. Slider untuk angka
    local slider_changed
    my_slider_value, slider_changed = ImGui.SliderFloat("Geser Nilai Ini", my_slider_value, 0.0, 100.0)
    if slider_changed then
        print("Nilai slider berubah menjadi:", my_slider_value)
    end

    -- Selalu akhiri jendela dengan ImGui.End()
    ImGui.End()
end
```

### Tingkat Menengah: Layout, Input & Popup

Contoh ini menunjukkan cara mengatur tata letak, menggunakan input teks, dan membuat menu serta popup.

```lua
-- Variabel di luar loop
local my_text_input = "Ketik sesuatu di sini..."
local my_color = ImVec4(1.0, 0.0, 1.0, 1.0) -- Ungu

-- Di dalam loop render utama:
if ImGui.Begin("Jendela Contoh Menengah", true, ImGui.WindowFlags.MenuBar) then

    -- 1. Menu Bar di dalam jendela
    if ImGui.BeginMenuBar() then
        if ImGui.BeginMenu("File") then
            if ImGui.MenuItem("Buka", "Ctrl+O") then
                print("Menu 'Buka' diklik")
            end
            if ImGui.MenuItem("Simpan", "Ctrl+S") then
                print("Menu 'Simpan' diklik")
            end
            ImGui.Separator()
            if ImGui.MenuItem("Keluar") then
                -- Logika untuk keluar dari aplikasi
            end
            ImGui.EndMenu()
        end
        ImGui.EndMenuBar()
    end

    -- 2. Input Teks
    ImGui.Text("Masukkan nama Anda:")
    local text_changed
    my_text_input, text_changed = ImGui.InputText("##NamaInput", my_text_input, 256)
    -- "##NamaInput" adalah ID unik tersembunyi. Label tidak ditampilkan.

    -- 3. Pemilih Warna (Color Picker)
    ImGui.Text("Pilih warna favorit:")
    ImGui.ColorEdit4("Warna", my_color)

    ImGui.Separator()

    -- 4. Popup Sederhana
    if ImGui.Button("Tampilkan Popup") then
        ImGui.OpenPopup("popup_contoh")
    end

    if ImGui.BeginPopup("popup_contoh") then
        ImGui.Text("Ini adalah pesan dari popup!")
        if ImGui.Button("Tutup") then
            ImGui.CloseCurrentPopup()
        end
        ImGui.EndPopup()
    end
    
    ImGui.End()
end
```

### Tingkat Lanjut: Styling, Tabel & Custom Drawing

Contoh ini menunjukkan cara mengubah tampilan (styling), membuat tabel data, dan menggambar bentuk kustom di latar belakang.

```lua
-- Di dalam loop render utama:
if ImGui.Begin("Jendela Contoh Lanjut") then

    -- 1. Mengubah Style secara sementara
    ImGui.Text("Tombol dengan gaya kustom:")

    -- Mengubah warna tombol menjadi merah
    ImGui.PushStyleColor(ImGui.Col.Button, ImVec4(1.0, 0.2, 0.2, 1.0))
    ImGui.PushStyleColor(ImGui.Col.ButtonHovered, ImVec4(1.0, 0.3, 0.3, 1.0))
    ImGui.PushStyleVar(ImGui.StyleVar.FrameRounding, 12.0) -- Membuat sudut tombol lebih bulat

    if ImGui.Button("Tombol Merah Bulat") then
        -- Aksi...
    end
    
    -- Kembalikan style ke semula. Jumlah Pop harus sama dengan jumlah Push.
    ImGui.PopStyleColor(2)
    ImGui.PopStyleVar(1)

    ImGui.Separator()

    -- 2. Membuat Tabel
    ImGui.Text("Tabel Data Pengguna:")
    local table_flags = ImGui.TableFlags.Borders | ImGui.TableFlags.RowBg
    if ImGui.BeginTable("tabel_data", 3, table_flags) then
        -- Header
        ImGui.TableSetupColumn("ID")
        ImGui.TableSetupColumn("Nama")
        ImGui.TableSetupColumn("Skor")
        ImGui.TableHeadersRow()

        -- Data Baris 1
        ImGui.TableNextRow()
        ImGui.TableNextColumn(); ImGui.Text("001")
        ImGui.TableNextColumn(); ImGui.Text("Alice")
        ImGui.TableNextColumn(); ImGui.Text("850")

        -- Data Baris 2
        ImGui.TableNextRow()
        ImGui.TableNextColumn(); ImGui.Text("002")
        ImGui.TableNextColumn(); ImGui.Text("Bob")
        ImGui.TableNextColumn(); ImGui.Text("920")
        
        ImGui.EndTable()
    end
    
    ImGui.Separator()

    -- 3. Custom Drawing (menggambar di background jendela)
    ImGui.Text("Gambar kustom di bawah:")
    local drawList = ImGui.GetWindowDrawList()
    local canvas_pos = ImGui.GetCursorScreenPos()
    local canvas_size = ImGui.GetContentRegionAvail()
    
    -- Gambar kotak batas
    drawList:AddRect(canvas_pos, ImVec2(canvas_pos.x + canvas_size.x, canvas_pos.y + 100), ImGui.GetColorU32(ImVec4(1,1,1,1)))
    
    -- Gambar garis diagonal
    drawList:AddLine(canvas_pos, ImVec2(canvas_pos.x + canvas_size.x, canvas_pos.y + 100), ImGui.GetColorU32(ImVec4(1,0,0,1)), 2.0)
    
    -- Gambar lingkaran di tengah
    local circle_center = ImVec2(canvas_pos.x + canvas_size.x * 0.5, canvas_pos.y + 50)
    drawList:AddCircleFilled(circle_center, 20.0, ImGui.GetColorU32(ImVec4(0,1,0,1)))

    -- Beri ruang kosong agar widget lain tidak menimpa gambar
    ImGui.Dummy(ImVec2(canvas_size.x, 100))
    
    ImGui.End()
end
```

---

## 🔍 Referensi Fungsi Lengkap

Berikut adalah daftar semua fungsi yang tersedia, dikelompokkan berdasarkan kategori untuk kemudahan pencarian.

### Daftar Fungsi Berdasarkan Kategori

#### 🪟 WINDOW & LAYOUT
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (65 fungsi)</summary>

- `ImGui.Begin()`
- `ImGui.BeginChild()`
- `ImGui.BeginChildFrame()`
- `ImGui.BeginDisabled()`
- `ImGui.BeginGroup()`
- `ImGui.BeginMainMenuBar()`
- `ImGui.BeginMenu()`
- `ImGui.BeginMenuBar()`
- `ImGui.BeginPopup()`
- `ImGui.BeginPopupContextItem()`
- `ImGui.BeginPopupContextVoid()`
- `ImGui.BeginPopupContextWindow()`
- `ImGui.BeginPopupModal()`
- `ImGui.BeginTabBar()`
- `ImGui.BeginTabItem()`
- `ImGui.BeginTable()`
- `ImGui.BeginTooltip()`
- `ImGui.Columns()`
- `ImGui.End()`
- `ImGui.EndChild()`
- `ImGui.EndChildFrame()`
- `ImGui.EndDisabled()`
- `ImGui.EndGroup()`
- `ImGui.EndMainMenuBar()`
- `ImGui.EndMenu()`
- `ImGui.EndMenuBar()`
- `ImGui.EndPopup()`
- `ImGui.EndTabBar()`
- `ImGui.EndTabItem()`
- `ImGui.EndTable()`
- `ImGui.EndTooltip()`
- `ImGui.GetColumnsCount()`
- `ImGui.GetFrameHeightWithSpacing()`
- `ImGui.GetTextLineHeightWithSpacing()`
- `ImGui.GetWindowContentRegionMax()`
- `ImGui.GetWindowContentRegionMin()`
- `ImGui.GetWindowHeight()`
- `ImGui.GetWindowPos()`
- `ImGui.GetWindowSize()`
- `ImGui.GetWindowWidth()`
- `ImGui.Indent()`
- `ImGui.IsWindowAppearing()`
- `ImGui.IsWindowCollapsed()`
- `ImGui.IsWindowFocused()`
- `ImGui.IsWindowHovered()`
- `ImGui.NewLine()`
- `ImGui.NextColumn()`
- `ImGui.SameLine()`
- `ImGui.Separator()`
- `ImGui.SeparatorText()`
- `ImGui.SetNextFrameWantCaptureKeyboard()`
- `ImGui.SetNextFrameWantCaptureMouse()`
- `ImGui.SetNextItemOpen()`
- `ImGui.SetNextItemWidth()`
- `ImGui.SetNextWindowBgAlpha()`
- `ImGui.SetNextWindowCollapsed()`
- `ImGui.SetNextWindowContentSize()`
- `ImGui.SetNextWindowFocus()`
- `ImGui.SetNextWindowPos()`
- `ImGui.SetNextWindowScroll()`
- `ImGui.SetNextWindowSize()`
- `ImGui.SetNextWindowSizeConstraints()`
- `ImGui.Spacing()`
- `ImGui.TableNextColumn()`
- `ImGui.Unindent()`
</details>

#### 🔘 WIDGETS - BASIC
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (30 fungsi)</summary>

- `ImGui.AlignTextToFramePadding()`
- `ImGui.ArrowButton()`
- `ImGui.Bullet()`
- `ImGui.BulletText()`
- `ImGui.Button()`
- `ImGui.CalcTextSize()`
- `ImGui.Checkbox()`
- `ImGui.CheckboxFlags()`
- `ImGui.ColorButton()`
- `ImGui.GetClipboardText()`
- `ImGui.GetTextLineHeight()`
- `ImGui.Image()`
- `ImGui.ImageButton()`
- `ImGui.InvisibleButton()`
- `ImGui.LabelText()`
- `ImGui.LogButtons()`
- `ImGui.LogText()`
- `ImGui.PopButtonRepeat()`
- `ImGui.PopTextWrapPos()`
- `ImGui.PushButtonRepeat()`
- `ImGui.PushTextWrapPos()`
- `ImGui.RadioButton()`
- `ImGui.SetClipboardText()`
- `ImGui.SmallButton()`
- `ImGui.TabItemButton()`
- `ImGui.Text()`
- `ImGui.TextColored()`
- `ImGui.TextDisabled()`
- `ImGui.TextUnformatted()`
- `ImGui.TextWrapped()`
</details>

#### 📝 WIDGETS - INPUT
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (29 fungsi)</summary>

- `ImGui.BeginCombo()`
- `ImGui.BeginListBox()`
- `ImGui.ColorEdit4()`
- `ImGui.Combo()`
- `ImGui.DragFloat()`
- `ImGui.DragInt()`
- `ImGui.DragScalar()`
- `ImGui.EndCombo()`
- `ImGui.EndListBox()`
- `ImGui.GetMouseDragDelta()`
- `ImGui.GetTreeNodeToLabelSpacing()`
- `ImGui.InputFloat()`
- `ImGui.InputInt()`
- `ImGui.InputText()`
- `ImGui.InputTextMultiline()`
- `ImGui.InputTextWithHint()`
- `ImGui.IsMouseDragging()`
- `ImGui.ResetMouseDragDelta()`
- `ImGui.Selectable()`
- `ImGui.SetColorEditOptions()`
- `ImGui.SliderAngle()`
- `ImGui.SliderFloat()`
- `ImGui.SliderInt()`
- `ImGui.SliderScalar()`
- `ImGui.TreeNode()`
- `ImGui.TreeNodeEx()`
- `ImGui.TreePop()`
- `ImGui.VSliderFloat()`
- `ImGui.VSliderInt()`
</details>

#### 📊 WIDGETS - DATA
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (2 fungsi)</summary>

- `ImGui.ProgressBar()`
- `ImGui.SetTooltip()`
</details>

#### 🗂️ CONTAINERS & POPUPS
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (4 fungsi)</summary>

- `ImGui.CloseCurrentPopup()`
- `ImGui.MenuItem()`
- `ImGui.OpenPopup()`
- `ImGui.OpenPopupOnItemClick()`
</details>

#### 🎨 STYLE & THEMING
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (7 fungsi)</summary>

- `ImGui.GetStyleColorVec4()`
- `ImGui.PopID()`
- `ImGui.PopStyleColor()`
- `ImGui.PopStyleVar()`
- `ImGui.PushID()`
- `ImGui.PushStyleColor()`
- `ImGui.PushStyleVar()`
</details>

#### 🖱️ INPUT & INTERACTION
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (21 fungsi)</summary>

- `ImGui.GetItemID()`
- `ImGui.GetItemRectMax()`
- `ImGui.GetItemRectMin()`
- `ImGui.GetItemRectSize()`
- `ImGui.GetMousePos()`
- `ImGui.GetMousePosOnOpeningCurrentPopup()`
- `ImGui.IsItemActivated()`
- `ImGui.IsItemActive()`
- `ImGui.IsItemClicked()`
- `ImGui.IsItemDeactivated()`
- `ImGui.IsItemDeactivatedAfterEdit()`
- `ImGui.IsItemEdited()`
- `ImGui.IsItemFocused()`
- `ImGui.IsItemHovered()`
- `ImGui.IsItemToggledOpen()`
- `ImGui.IsItemVisible()`
- `ImGui.IsMouseClicked()`
- `ImGui.IsMouseDown()`
- `ImGui.IsMouseReleased()`
- `ImGui.SetItemAllowOverlap()`
- `ImGui.SetItemDefaultFocus()`
</details>

#### 🖼️ DRAWING & RENDERING
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (2 fungsi)</summary>

- `ImGui.GetBackgroundDrawList()`
- `ImGui.GetForegroundDrawList()`
</details>

#### 📏 LAYOUT & POSITIONING
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (13 fungsi)</summary>

- `ImGui.GetContentRegionAvail()`
- `ImGui.GetContentRegionMax()`
- `ImGui.GetCursorPos()`
- `ImGui.GetCursorPosX()`
- `ImGui.GetCursorPosY()`
- `ImGui.GetCursorScreenPos()`
- `ImGui.GetCursorStartPos()`
- `ImGui.GetFrameCount()`
- `ImGui.GetFrameHeight()`
- `ImGui.SetCursorPos()`
- `ImGui.SetCursorPosX()`
- `ImGui.SetCursorPosY()`
- `ImGui.SetCursorScreenPos()`
</details>

#### 🔧 UTILITIES & HELPERS
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (8 fungsi)</summary>

- `ImGui.GetVersion()`
- `ImGui.ShowAboutWindow()`
- `ImGui.ShowDemoWindow()`
- `ImGui.ShowFontSelector()`
- `ImGui.ShowMetricsWindow()`
- `ImGui.ShowStyleEditor()`
- `ImGui.ShowStyleSelector()`
- `ImGui.ShowUserGuide()`
</details>

#### 🌐 UNCATEGORIZED
<details>
<summary>Klik untuk melihat/menyembunyikan daftar (69 fungsi)</summary>

- `ImGui.CalcItemWidth()`
- `ImGui.CollapsingHeader()`
- `ImGui.ColorConvertFloat4ToU32()`
- `ImGui.ColorConvertHSVtoRGB()`
- `ImGui.ColorConvertRGBtoHSV()`
- `ImGui.ColorConvertU32ToFloat4()`
- `ImGui.Dummy()`
- `ImGui.GetColorU32()`
- `ImGui.GetColumnIndex()`
- `ImGui.GetColumnOffset()`
- `ImGui.GetColumnWidth()`
- `ImGui.GetFontSize()`
- `ImGui.GetFontTexUvWhitePixel()`
- `ImGui.GetID()`
- `ImGui.GetMouseClickedCount()`
- `ImGui.GetMouseCursor()`
- `ImGui.GetScrollMaxX()`
- `ImGui.GetScrollMaxY()`
- `ImGui.GetScrollX()`
- `ImGui.GetScrollY()`
- `ImGui.GetTime()`
- `ImGui.IsAnyItemActive()`
- `ImGui.IsAnyItemFocused()`
- `ImGui.IsAnyItemHovered()`
- `ImGui.IsAnyMouseDown()`
- `ImGui.IsMouseDoubleClicked()`
- `ImGui.IsMouseHoveringRect()`
- `ImGui.IsPopupOpen()`
- `ImGui.IsRectVisible()`
- `ImGui.LogFinish()`
- `ImGui.LogToClipboard()`
- `ImGui.LogToFile()`
- `ImGui.LogToTTY()`
- `ImGui.PopClipRect()`
- `ImGui.PopItemWidth()`
- `ImGui.PushClipRect()`
- `ImGui.PushItemWidth()`
- `ImGui.SetColumnOffset()`
- `ImGui.SetColumnWidth()`
- `ImGui.SetKeyboardFocusHere()`
- `ImGui.SetMouseCursor()`
- `ImGui.SetScrollFromPosX()`
- `ImGui.SetScrollFromPosY()`
- `ImGui.SetScrollHereX()`
- `ImGui.SetScrollHereY()`
- `ImGui.SetScrollX()`
- `ImGui.SetScrollY()`
- `ImGui.SetTabItemClosed()`
- `ImGui.SetWindowCollapsed()`
- `ImGui.SetWindowFocus()`
- `ImGui.SetWindowFontScale()`
- `ImGui.SetWindowPos()`
- `ImGui.SetWindowSize()`
- `ImGui.ShowDebugLogWindow()`
- `ImGui.ShowStackToolWindow()`
- `ImGui.TableGetColumnCount()`
- `ImGui.TableGetColumnFlags()`
- `ImGui.TableGetColumnIndex()`
- `ImGui.TableGetColumnName()`
- `ImGui.TableGetRowIndex()`
- `ImGui.TableHeader()`
- `ImGui.TableHeadersRow()`
- `ImGui.TableNextRow()`
- `ImGui.TableSetBgColor()`
- `ImGui.TableSetColumnEnabled()`
- `ImGui.TableSetColumnIndex()`
- `ImGui.TableSetupColumn()`
- `ImGui.TableSetupScrollFreeze()`
- `ImGui.TreePush()`
</details>

---

## 🗂️ Referensi Enum & Tabel

Ini adalah konstanta yang digunakan untuk flags, style, warna, dan lainnya.

### Daftar Enum & Tabel yang Tersedia

#### `ImGui.WindowFlags`
Flag untuk mengontrol perilaku jendela.
*Contoh: `ImGui.Begin("Judul", true, ImGui.WindowFlags.NoResize | ImGui.WindowFlags.MenuBar)`*

| Konstanta | Deskripsi (Umum) |
|---|---|
| `ImGui.WindowFlags.None` | Tidak ada flag. |
| `ImGui.WindowFlags.NoTitleBar` | Tanpa title bar. |
| `ImGui.WindowFlags.NoResize` | Jendela tidak bisa diubah ukurannya. |
| `ImGui.WindowFlags.NoMove` | Jendela tidak bisa digerakkan. |
| `ImGui.WindowFlags.NoScrollbar` | Nonaktifkan scrollbar. |
| `ImGui.WindowFlags.MenuBar` | Jendela memiliki menu bar. |
| `ImGui.WindowFlags.AlwaysAutoResize` | Selalu mengubah ukuran jendela sesuai konten. |
| `ImGui.WindowFlags.NoSavedSettings`| Tidak memuat/menyimpan pengaturan di file .ini. |
| *(dan lainnya...)* | |

#### `ImGui.Col`
Enum untuk mengidentifikasi elemen UI yang warnanya bisa diubah.
*Contoh: `ImGui.PushStyleColor(ImGui.Col.Button, ImVec4(1,0,0,1))`*

| Konstanta | Target Elemen |
|---|---|
| `ImGui.Col.Text` | Warna teks default. |
| `ImGui.Col.WindowBg` | Warna latar belakang jendela. |
| `ImGui.Col.Button` | Warna tombol dalam keadaan normal. |
| `ImGui.Col.ButtonHovered` | Warna tombol saat kursor di atasnya. |
| `ImGui.Col.ButtonActive` | Warna tombol saat ditekan. |
| `ImGui.Col.Header` | Warna header (misal: CollapsingHeader). |
| `ImGui.Col.Border` | Warna bingkai (border). |
| *(dan lainnya...)* | |

#### `ImGui.StyleVar`
Enum untuk mengidentifikasi variabel gaya (ukuran, padding, dll).
*Contoh: `ImGui.PushStyleVar(ImGui.StyleVar.FrameRounding, 5.0)`*

| Konstanta | Target Properti |
|---|---|
| `ImGui.StyleVar.Alpha` | Transparansi global. |
| `ImGui.StyleVar.WindowPadding`| Padding di dalam jendela. |
| `ImGui.StyleVar.WindowRounding`| Tingkat kebulatan sudut jendela. |
| `ImGui.StyleVar.FramePadding` | Padding di dalam frame widget (tombol, input). |
| `ImGui.StyleVar.FrameRounding` | Tingkat kebulatan sudut frame. |
| `ImGui.StyleVar.ItemSpacing` | Jarak antar widget. |
| *(dan lainnya...)* | |

#### `ImGui.Cond`
Enum untuk kondisi saat menerapkan suatu perubahan (misal: `SetNextWindowSize`).
*Contoh: `ImGui.SetNextWindowSize(ImVec2(300, 200), ImGui.Cond.FirstUseEver)`*

| Konstanta | Deskripsi Kondisi |
|---|---|
| `ImGui.Cond.Always` | Selalu terapkan. |
| `ImGui.Cond.Once` | Terapkan sekali per sesi. |
| `ImGui.Cond.FirstUseEver` | Terapkan hanya saat pertama kali jendela dibuat. |
| `ImGui.Cond.Appearing` | Terapkan saat jendela baru muncul. |

#### `ImGui.InputTextFlags`
Flag untuk mengontrol perilaku widget `InputText`.

| Konstanta | Deskripsi |
|---|---|
| `ImGui.InputTextFlags.None` | Tidak ada flag. |
| `ImGui.InputTextFlags.CharsDecimal` | Hanya izinkan angka desimal. |
| `ImGui.InputTextFlags.CharsHexadecimal` | Hanya izinkan angka heksadesimal. |
| `ImGui.InputTextFlags.CharsUppercase` | Otomatis ubah menjadi huruf kapital. |
| `ImGui.InputTextFlags.Password` | Sembunyikan karakter (seperti input password). |
| `ImGui.InputTextFlags.ReadOnly` | Teks tidak bisa diedit. |
| `ImGui.InputTextFlags.EnterReturnsTrue` | Menekan Enter akan membuat fungsi mengembalikan `true`. |
| *(dan lainnya...)* | |

#### Enum Lainnya
- **`ImGui.Dir`**: Arah (Kiri, Kanan, Atas, Bawah).
- **`ImGui.MouseButton`**: Tombol mouse (Kiri, Kanan, Tengah).
- **`ImGui.MouseCursor`**: Tipe kursor mouse (Arrow, Hand, TextInput, dll).
- **`ImGui.TableBgTarget`**: Target pewarnaan background tabel.
- **`ImGui.DrawFlags` / `ImGui.DrawListFlags`**: Opsi untuk menggambar.
- **`ImGui.SortDirection`**: Arah pengurutan untuk tabel.
- **`ImGui.DataType`**: Tipe data untuk `DragScalar`, `SliderScalar`, dll.

#### Tabel Khusus
- **`ImGui.BG` / `ImGui.FG`**: Objek *DrawList* untuk menggambar di background/foreground global. Keduanya memiliki fungsi seperti `AddLine()`, `AddRectFilled()`, `AddText()`, dll.

---

## 🌐 Fungsi Global

Fungsi ini biasanya digunakan untuk membuat objek vektor yang dibutuhkan oleh fungsi ImGui lainnya.

- **`ImVec2(x, y)`**
  Membuat objek vektor 2D. Umumnya digunakan untuk ukuran (size), posisi (pos), padding, dll.
  *Contoh: `ImGui.SetNextWindowSize(ImVec2(500, 300))`*

- **`ImVec4(r, g, b, a)`**
  Membuat objek vektor 4D. Umumnya digunakan untuk warna, di mana `r, g, b, a` adalah nilai antara `0.0` dan `1.0`.
  *Contoh: `ImGui.TextColored(ImVec4(1.0, 1.0, 0.0, 1.0), "Teks Kuning")`*

---
_Dokumentasi ini disempurnakan untuk kemudahan penggunaan. Selamat berkarya!_
