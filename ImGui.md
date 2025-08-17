# 🗂️ IMGUI Lua Documentation (Categorized)

**Generated:** 2025-08-17 14:15:17  
**Lua Version:** Lua 5.4

---

## 📊 Statistik

- **Functions:** 250 _(dikategorikan dalam 13 kategori)_
- **Tables/Enums:** 15 _(Total items: 217)_
- **Other Properties:** 0
- **Global ImGui Functions:** 2

---

## 📋 Daftar Isi

1. 📝 Widgets - Input (29)
2. 🪟 Window & Layout (65)
3. 🔘 Widgets - Basic (30)
4. 🖱️ Input & Interaction (21)
5. 🖼️ Drawing & Rendering (2)
6. 📊 Widgets - Data (2)
7. 🔧 Utilities & Helpers (8)
8. 🌐 Uncategorized (69)
9. 🗂️ Containers & Popups (4)
10. 📏 Layout & Positioning (13)
11. 🎨 Style & Theming (7)
12. 🗂️ Tables/Enums (15)
13. 🌐 Global Functions (2)

💡 **TIP:** Gunakan `Ctrl + F` untuk mencari kategori/fungsi tertentu!

---

## 🔍 Functions by Category

### 🪟 Window & Layout
<details>
<summary>Lihat Daftar (65 functions)</summary>

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

---

### 🔘 Widgets - Basic
<details>
<summary>Lihat Daftar (30 functions)</summary>

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

---

### 📝 Widgets - Input
<details>
<summary>Lihat Daftar (29 functions)</summary>

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

---

### 📊 Widgets - Data
- `ImGui.ProgressBar()`
- `ImGui.SetTooltip()`

---

### 🗂️ Containers & Popups
- `ImGui.CloseCurrentPopup()`
- `ImGui.MenuItem()`
- `ImGui.OpenPopup()`
- `ImGui.OpenPopupOnItemClick()`

---

### 🎨 Style & Theming
- `ImGui.GetStyleColorVec4()`
- `ImGui.PopID()`
- `ImGui.PopStyleColor()`
- `ImGui.PopStyleVar()`
- `ImGui.PushID()`
- `ImGui.PushStyleColor()`
- `ImGui.PushStyleVar()`

---

### 🖱️ Input & Interaction
<details>
<summary>Lihat Daftar (21 functions)</summary>

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

---

### 🖼️ Drawing & Rendering
- `ImGui.GetBackgroundDrawList()` (Lua)
- `ImGui.GetForegroundDrawList()` (Lua)

---

### 📏 Layout & Positioning
<details>
<summary>Lihat Daftar (13 functions)</summary>

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

---

### 🔧 Utilities & Helpers
- `ImGui.GetVersion()`
- `ImGui.ShowAboutWindow()`
- `ImGui.ShowDemoWindow()`
- `ImGui.ShowFontSelector()`
- `ImGui.ShowMetricsWindow()`
- `ImGui.ShowStyleEditor()`
- `ImGui.ShowStyleSelector()`
- `ImGui.ShowUserGuide()`

---

### 🌐 Uncategorized
<details>
<summary>Lihat Daftar (69 functions)</summary>

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

## 🗂️ Tables / Enums

<details>
<summary>Klik untuk melihat isi tabel/enums lengkap!</summary>

- **ImGui.BG** (11 items)
- **ImGui.Col** (54 items)
- **ImGui.Cond** (5 items)
- **ImGui.DataType** (11 items)
- **ImGui.Dir** (6 items)
- **ImGui.DrawFlags** (14 items)
- **ImGui.DrawListFlags** (5 items)
- **ImGui.FG** (11 items)
- **ImGui.InputTextFlags** (22 items)
- **ImGui.MouseButton** (4 items)
- **ImGui.MouseCursor** (11 items)
- **ImGui.SortDirection** (3 items)
- **ImGui.StyleVar** (26 items)
- **ImGui.TableBgTarget** (4 items)
- **ImGui.WindowFlags** (30 items)

</details>

---

## 🌐 Global ImGui Functions

- `ImVec2()`
- `ImVec4()`

---

## ⚡ Quick Reference (Most Commonly Used)

**Window Management:**
```lua
if ImGui.Begin("Window Title") then
  -- Your content here
  ImGui.End()
end
```

**Common Widgets:**
```lua
ImGui.Text("Hello World")
if ImGui.Button("Click Me") then
  -- Button was pressed
end
value, changed = ImGui.SliderFloat("Slider", value, 0.0, 100.0)
```

**Global Helpers:**
```lua
ImVec2(width, height)     -- For sizes and positions
ImVec4(r, g, b, a)        -- For colors (0.0-1.0 range)
```

---

## ✅ Documentation Complete

_Silakan kontribusi jika ada penambahan atau perbaikan pada dokumentasi ini!_
