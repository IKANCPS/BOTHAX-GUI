# ImGui Documentation for Growtopia Modding

This document provides a quick reference for ImGui functions available in Growtopia modding, categorized for easy lookup. All examples are provided within the `AddHook("OnDraw", "Sample" function() ... end)` block.

**Generated:** 2025-08-17 14:15:17
**Lua Version:** Lua 5.4

---

## 📋 Table of Contents

1.  [🪟 WINDOW & LAYOUT](#-window--layout)
2.  [🔘 WIDGETS - BASIC](#-widgets---basic)
3.  [📝 WIDGETS - INPUT](#-widgets---input)
4.  [📊 WIDGETS - DATA](#-widgets---data)
5.  [🗂️ CONTAINERS & POPUPS](#-containers--popups)
6.  [🎨 STYLE & THEMING](#-style--theming)
7.  [🖱️ INPUT & INTERACTION](#-input--interaction)
8.  [🖼️ DRAWING & RENDERING](#-drawing--rendering)
9.  [📏 LAYOUT & POSITIONING](#-layout--positioning)
10. [🔧 UTILITIES & HELPERS](#-utilities--helpers)
11. [🌐 UNCATEGORIZED](#-uncategorized)
12. [🗂️ TABLES/ENUMS](#-tablesenums)
13. [🌐 GLOBAL IMGUI FUNCTIONS](#-global-imgui-functions)
14. [⚡ QUICK REFERENCE](#-quick-reference)

---

## 🔍 Functions By Category

---

### 🪟 WINDOW & LAYOUT

```lua
AddHook("OnDraw", "ImGui_WindowLayout_Sample", function()
    -- Begin/End blocks are crucial for most ImGui content.
    if ImGui.Begin("My Sample Window") then
        ImGui.Text("Window content here.")

        -- Child Window
        if ImGui.BeginChild("Child1", ImVec2(0, 50), true) then
            ImGui.Text("Inside a child window.")
            ImGui.EndChild()
        end

        -- Child Frame
        if ImGui.BeginChildFrame(ImGui.GetID("ChildFrame1"), ImVec2(0, 50)) then
            ImGui.Text("Inside a child frame.")
            ImGui.EndChildFrame()
        end

        -- Disabled content
        ImGui.BeginDisabled()
        ImGui.Button("Disabled Button")
        ImGui.EndDisabled()

        -- Group content
        ImGui.BeginGroup()
        ImGui.Text("Grouped Text 1")
        ImGui.Text("Grouped Text 2")
        ImGui.EndGroup()

        -- Menu Bar (for main window)
        if ImGui.BeginMenuBar() then
            if ImGui.BeginMenu("File") then
                ImGui.MenuItem("New")
                ImGui.EndMenu()
            end
            ImGui.EndMenuBar()
        end

        -- Tab Bar
        if ImGui.BeginTabBar("MyTabs") then
            if ImGui.BeginTabItem("Tab 1") then
                ImGui.Text("Content of Tab 1")
                ImGui.EndTabItem()
            end
            if ImGui.BeginTabItem("Tab 2") then
                ImGui.Text("Content of Tab 2")
                ImGui.EndTabItem()
            end
            ImGui.EndTabBar()
        end

        -- Table
        if ImGui.BeginTable("MyTable", 3) then
            ImGui.TableSetupColumn("Header 1")
            ImGui.TableSetupColumn("Header 2")
            ImGui.TableSetupColumn("Header 3")
            ImGui.TableHeadersRow()
            ImGui.TableNextRow()
            ImGui.TableNextColumn() ImGui.Text("Row 1, Col 1")
            ImGui.TableNextColumn() ImGui.Text("Row 1, Col 2")
            ImGui.TableNextColumn() ImGui.Text("Row 1, Col 3")
            ImGui.EndTable()
        end

        -- Tooltip
        ImGui.Button("Hover me")
        if ImGui.BeginTooltip() then
            ImGui.Text("This is a tooltip!")
            ImGui.EndTooltip()
        end

        -- Columns (legacy)
        ImGui.Columns(2, "MyColumns", true)
        ImGui.Text("Column 1")
        ImGui.NextColumn()
        ImGui.Text("Column 2")
        ImGui.Columns(1) -- Reset columns

        -- Indent/Unindent
        ImGui.Text("Normal")
        ImGui.Indent()
        ImGui.Text("Indented")
        ImGui.Unindent()

        -- Spacing/NewLine/Separator
        ImGui.Separator()
        ImGui.NewLine()
        ImGui.Spacing()
        ImGui.SeparatorText("Separator Text")

        -- Window Info
        ImGui.Text("Window Pos: " .. tostring(ImGui.GetWindowPos().x) .. ", " .. tostring(ImGui.GetWindowPos().y))
        ImGui.Text("Window Size: " .. tostring(ImGui.GetWindowSize().x) .. ", " .. tostring(ImGui.GetWindowSize().y))
        ImGui.Text("Window Height: " .. tostring(ImGui.GetWindowHeight()))
        ImGui.Text("Window Width: " .. tostring(ImGui.GetWindowWidth()))
        ImGui.Text("Collapsed: " .. tostring(ImGui.IsWindowCollapsed()))
        ImGui.Text("Appearing: " .. tostring(ImGui.IsWindowAppearing()))
        ImGui.Text("Focused: " .. tostring(ImGui.IsWindowFocused()))
        ImGui.Text("Hovered: " .. tostring(ImGui.IsWindowHovered()))

        -- Set Next Window State
        -- ImGui.SetNextWindowPos(ImVec2(100,100), ImGui.Cond.Once)
        -- ImGui.SetNextWindowSize(ImVec2(300,200), ImGui.Cond.Once)
        -- ImGui.SetNextWindowCollapsed(true, ImGui.Cond.Once)
        -- ImGui.SetNextWindowFocus()
        -- ImGui.SetNextWindowBgAlpha(0.7)

        ImGui.End() -- End of My Sample Window
    end
end)
```

### 🔘 WIDGETS - BASIC

```lua
AddHook("OnDraw", "ImGui_WidgetsBasic_Sample", function()
    if ImGui.Begin("Basic Widgets") then
        ImGui.AlignTextToFramePadding()
        ImGui.Text("Aligned Text")

        if ImGui.ArrowButton("##Left", ImGui.Dir.Left) then end
        ImGui.SameLine()
        if ImGui.Button("Button") then end
        ImGui.SameLine()
        if ImGui.SmallButton("Small Btn") then end

        ImGui.Bullet() ImGui.SameLine(); ImGui.Text("Bullet point")
        ImGui.BulletText("Bullet Text here")

        local checkbox_val = true
        checkbox_val = ImGui.Checkbox("Checkbox", checkbox_val)
        -- ImGui.CheckboxFlags("Flags Checkbox", flags_var, ImGui.Flags.SomeFlag)

        ImGui.ColorButton("ColorBtn", ImVec4(1,0,0,1))

        ImGui.Text("Clipboard: " .. ImGui.GetClipboardText())
        if ImGui.Button("Copy 'Hello'") then ImGui.SetClipboardText("Hello") end

        ImGui.LabelText("Label", "Value")

        -- ImGui.LogButtons() -- Logging functions
        -- ImGui.LogText("Log message")

        ImGui.Text("Text Line Height: " .. tostring(ImGui.GetTextLineHeight()))
        ImGui.Text("Text Wrapped:")
        ImGui.PushTextWrapPos(ImGui.GetColumnWidth() * 0.5)
        ImGui.TextWrapped("This text will automatically wrap within half the column width. It's quite useful.")
        ImGui.PopTextWrapPos()

        local radio_selected = 0
        if ImGui.RadioButton("Option A", radio_selected == 0) then radio_selected = 0 end
        ImGui.SameLine()
        if ImGui.RadioButton("Option B", radio_selected == 1) then radio_selected = 1 end

        ImGui.TextColored(ImVec4(0,1,0,1), "Green Text")
        ImGui.TextDisabled("Disabled Text")
        ImGui.TextUnformatted("Unformatted\tText")

        -- ImGui.Image() -- Requires texture ID (not directly exposed in this wrapper context usually)
        -- ImGui.ImageButton() -- Same as above

        ImGui.InvisibleButton("Invisible", ImVec2(50,50))
        if ImGui.IsItemHovered() then ImGui.SetTooltip("Invisible Button Hovered!") end

        ImGui.End()
    end
end)
```

### 📝 WIDGETS - INPUT

```lua
AddHook("OnDraw", "ImGui_WidgetsInput_Sample", function()
    if ImGui.Begin("Input Widgets") then
        local float_val = 0.5
        float_val = ImGui.DragFloat("Drag Float", float_val, 0.01, 0, 1)

        local int_val = 10
        int_val = ImGui.DragInt("Drag Int", int_val, 1, 0, 100)

        -- ImGui.DragScalar("Drag Scalar", ImGui.DataType.Float, float_val_ptr) -- More generic version

        local input_text = "Type here"
        local changed, new_text = ImGui.InputText("Input Text", input_text)
        if changed then input_text = new_text end

        local input_multiline = "Multi-line\ntext input"
        local changed_ml, new_ml_text = ImGui.InputTextMultiline("Input Multiline", input_multiline, ImVec2(0, 50))
        if changed_ml then input_multiline = new_ml_text end

        local input_hint = ""
        local changed_hint, new_hint_text = ImGui.InputTextWithHint("Input Hint", "Enter text...", input_hint)
        if changed_hint then input_hint = new_hint_text end

        local color = ImVec4(1,0,0,1)
        color = ImGui.ColorEdit4("Color Picker", color)

        local combo_items = {"Item A", "Item B", "Item C"}
        local current_item = combo_items[1]
        local combo_changed, selected_idx = ImGui.Combo("Combo", 0, combo_items)
        if combo_changed then current_item = combo_items[selected_idx + 1] end -- Lua arrays are 1-indexed

        -- List Box (manual begin/end)
        local listbox_current_item = 0
        if ImGui.BeginListBox("My Listbox") then
            for i, item in ipairs({"One", "Two", "Three"}) do
                local is_selected = (listbox_current_item == (i-1))
                if ImGui.Selectable(item, is_selected) then
                    listbox_current_item = (i-1)
                end
                if is_selected then ImGui.SetItemDefaultFocus() end
            end
            ImGui.EndListBox()
        end

        local slider_float = 0.5
        slider_float = ImGui.SliderFloat("Slider Float", slider_float, 0, 1)

        local slider_int = 50
        slider_int = ImGui.SliderInt("Slider Int", slider_int, 0, 100)

        local angle = 0.0
        angle = ImGui.SliderAngle("Slider Angle", angle)

        -- ImGui.SliderScalar() -- More generic version

        local vslider_float = 0.5
        vslider_float = ImGui.VSliderFloat("VSliderF", ImVec2(20,80), vslider_float, 0, 1)
        ImGui.SameLine()
        local vslider_int = 50
        vslider_int = ImGui.VSliderInt("VSliderI", ImVec2(20,80), vslider_int, 0, 100)

        -- Tree Node
        if ImGui.TreeNode("Node 1") then
            ImGui.Text("Content of Node 1")
            ImGui.TreePop()
        end

        if ImGui.TreeNodeEx("Node 2 (Ex)", ImGui.TreeNodeFlags.DefaultOpen) then
            ImGui.Text("Content of Node 2")
            ImGui.TreePop()
        end

        -- Input/Mouse States
        ImGui.Text("Mouse Drag Delta: " .. tostring(ImGui.GetMouseDragDelta().x) .. ", " .. tostring(ImGui.GetMouseDragDelta().y))
        if ImGui.IsMouseDragging(ImGui.MouseButton.Left) then ImGui.Text("Left Mouse Dragging") end
        if ImGui.Button("Reset Drag Delta") then ImGui.ResetMouseDragDelta() end

        ImGui.Text("TreeNode to Label Spacing: " .. tostring(ImGui.GetTreeNodeToLabelSpacing()))
        ImGui.End()
    end
end)
```

### 📊 WIDGETS - DATA

```lua
AddHook("OnDraw", "ImGui_WidgetsData_Sample", function()
    if ImGui.Begin("Data Widgets") then
        ImGui.ProgressBar(0.75, ImVec2(0,0), "75%")
        ImGui.Button("Hover me for tooltip")
        ImGui.SetTooltip("This is a simple tooltip via SetTooltip.")
        ImGui.End()
    end
end)
```

### 🗂️ CONTAINERS & POPUPS

```lua
AddHook("OnDraw", "ImGui_ContainersPopups_Sample", function()
    if ImGui.Begin("Containers & Popups") then
        if ImGui.Button("Open Popup") then
            ImGui.OpenPopup("my_popup")
        end

        if ImGui.BeginPopup("my_popup") then
            ImGui.Text("This is a popup!")
            if ImGui.MenuItem("Close") then
                ImGui.CloseCurrentPopup()
            end
            ImGui.EndPopup()
        end

        if ImGui.Button("Open Modal") then
            ImGui.OpenPopup("my_modal")
        end

        if ImGui.BeginPopupModal("my_modal", nil, ImGui.WindowFlags.AlwaysAutoResize) then
            ImGui.Text("This is a modal window.")
            ImGui.Text("Click 'OK' to close.")
            if ImGui.Button("OK") then
                ImGui.CloseCurrentPopup()
            end
            ImGui.EndPopupModal()
        end

        -- Context Popups
        ImGui.Text("Right click this text for context menu.")
        ImGui.OpenPopupOnItemClick("item_context_menu", ImGui.MouseButton.Right)
        if ImGui.BeginPopupContextItem("item_context_menu") then
            ImGui.MenuItem("Option A")
            ImGui.MenuItem("Option B")
            ImGui.EndPopup()
        end

        ImGui.Text("Right click anywhere in this window for context menu.")
        if ImGui.BeginPopupContextWindow("window_context_menu") then
            ImGui.MenuItem("Window Option 1")
            ImGui.MenuItem("Window Option 2")
            ImGui.EndPopup()
        end

        if ImGui.Button("Right click void for context menu") then end
        ImGui.BeginPopupContextVoid("void_context_menu")
        if ImGui.MenuItem("Void Option A") then end
        ImGui.EndPopup()

        ImGui.End()
    end
end)
```

### 🎨 STYLE & THEMING

```lua
AddHook("OnDraw", "ImGui_StyleTheming_Sample", function()
    if ImGui.Begin("Style & Theming") then
        ImGui.Text("Default color.")
        ImGui.PushStyleColor(ImGui.Col.Text, ImVec4(1, 0, 0, 1))
        ImGui.Text("Red text.")
        ImGui.PopStyleColor()

        ImGui.Text("Default frame rounding.")
        ImGui.PushStyleVar(ImGui.StyleVar.FrameRounding, 10.0)
        ImGui.Button("Rounded Button")
        ImGui.PopStyleVar()

        ImGui.Text("Get Style Color: " .. tostring(ImGui.GetStyleColorVec4(ImGui.Col.Button).x))

        -- Push/Pop ID for unique widget IDs within loops
        for i = 1, 3 do
            ImGui.PushID(i)
            ImGui.Button("Button " .. tostring(i))
            ImGui.PopID()
        end
        ImGui.End()
    end
end)
```

### 🖱️ INPUT & INTERACTION

```lua
AddHook("OnDraw", "ImGui_InputInteraction_Sample", function()
    if ImGui.Begin("Input & Interaction") then
        ImGui.Button("Interact with me")
        if ImGui.IsItemHovered() then ImGui.Text("Item Hovered!") end
        if ImGui.IsItemClicked(ImGui.MouseButton.Left) then ImGui.Text("Item Left Clicked!") end
        if ImGui.IsItemActive() then ImGui.Text("Item Active (being dragged/held)") end
        if ImGui.IsItemActivated() then ImGui.Text("Item Activated (just became active)") end
        if ImGui.IsItemDeactivated() then ImGui.Text("Item Deactivated (just released)") end
        if ImGui.IsItemDeactivatedAfterEdit() then ImGui.Text("Item Deactivated After Edit") end
        if ImGui.IsItemEdited() then ImGui.Text("Item Edited") end
        if ImGui.IsItemFocused() then ImGui.Text("Item Focused") end
        if ImGui.IsItemToggledOpen() then ImGui.Text("Item Toggled Open") end
        if ImGui.IsItemVisible() then ImGui.Text("Item Visible") end

        ImGui.Text("Item ID: " .. tostring(ImGui.GetItemID()))
        ImGui.Text("Item Rect Min: " .. tostring(ImGui.GetItemRectMin().x) .. "," .. tostring(ImGui.GetItemRectMin().y))
        ImGui.Text("Item Rect Max: " .. tostring(ImGui.GetItemRectMax().x) .. "," .. tostring(ImGui.GetItemRectMax().y))
        ImGui.Text("Item Rect Size: " .. tostring(ImGui.GetItemRectSize().x) .. "," .. tostring(ImGui.GetItemRectSize().y))

        ImGui.Text("Mouse Pos: " .. tostring(ImGui.GetMousePos().x) .. ", " .. tostring(ImGui.GetMousePos().y))
        ImGui.Text("Popup Open Pos: " .. tostring(ImGui.GetMousePosOnOpeningCurrentPopup().x))

        if ImGui.IsMouseClicked(ImGui.MouseButton.Right) then ImGui.Text("Right Clicked!") end
        if ImGui.IsMouseDown(ImGui.MouseButton.Middle) then ImGui.Text("Middle Mouse Down!") end
        if ImGui.IsMouseReleased(ImGui.MouseButton.Left) then ImGui.Text("Left Mouse Released!") end

        -- ImGui.SetItemAllowOverlap() -- Allows another item to overlap the current one (rarely needed)
        -- ImGui.SetItemDefaultFocus() -- Focuses the item by default (e.g., in a listbox)

        ImGui.End()
    end
end)
```

### 🖼️ DRAWING & RENDERING

```lua
AddHook("OnDraw", "ImGui_DrawingRendering_Sample", function()
    if ImGui.Begin("Drawing & Rendering") then
        local draw_list_bg = ImGui.GetBackgroundDrawList()
        draw_list_bg:AddCircleFilled(ImVec2(100,100), 20, ImGui.ColorConvertFloat4ToU32(ImVec4(1,0,0,1)))

        local draw_list_fg = ImGui.GetForegroundDrawList()
        draw_list_fg:AddRect(ImVec2(150,150), ImVec2(200,200), ImGui.ColorConvertFloat4ToU32(ImVec4(0,0,1,1)), 0, ImGui.DrawFlags.RoundCornersAll, 2)
        draw_list_fg:AddText(ImVec2(160,160), ImGui.ColorConvertFloat4ToU32(ImVec4(1,1,1,1)), "Hello")

        ImGui.Text("See circles and rectangles drawn outside this window.")
        ImGui.End()
    end
end)
```

### 📏 LAYOUT & POSITIONING

```lua
AddHook("OnDraw", "ImGui_LayoutPositioning_Sample", function()
    if ImGui.Begin("Layout & Positioning") then
        ImGui.Text("Current Cursor Pos: " .. tostring(ImGui.GetCursorPos().x) .. ", " .. tostring(ImGui.GetCursorPos().y))
        ImGui.Text("Current Cursor X: " .. tostring(ImGui.GetCursorPosX()))
        ImGui.Text("Current Cursor Y: " .. tostring(ImGui.GetCursorPosY()))
        ImGui.Text("Current Cursor Screen Pos: " .. tostring(ImGui.GetCursorScreenPos().x) .. ", " .. tostring(ImGui.GetCursorScreenPos().y))
        ImGui.Text("Cursor Start Pos: " .. tostring(ImGui.GetCursorStartPos().x) .. ", " .. tostring(ImGui.GetCursorStartPos().y))

        ImGui.SetCursorPosX(50)
        ImGui.Button("Button at X=50")
        ImGui.SetCursorPosY(ImGui.GetCursorPosY() + 20)
        ImGui.Button("Button shifted down")
        ImGui.SetCursorPos(ImVec2(100, 150))
        ImGui.Button("Button at (100,150)")

        -- ImGui.SetCursorScreenPos(ImVec2(300, 50)) -- Sets cursor to absolute screen position

        ImGui.Text("Available Content Region: " .. tostring(ImGui.GetContentRegionAvail().x) .. ", " .. tostring(ImGui.GetContentRegionAvail().y))
        ImGui.Text("Max Content Region: " .. tostring(ImGui.GetContentRegionMax().x) .. ", " .. tostring(ImGui.GetContentRegionMax().y))

        ImGui.Text("Frame Count: " .. tostring(ImGui.GetFrameCount()))
        ImGui.Text("Frame Height: " .. tostring(ImGui.GetFrameHeight()))

        ImGui.End()
    end
end)
```

### 🔧 UTILITIES & HELPERS

```lua
AddHook("OnDraw", "ImGui_Utilities_Sample", function()
    if ImGui.Begin("Utilities & Helpers") then
        ImGui.Text("ImGui Version: " .. ImGui.GetVersion())

        if ImGui.Button("Show Demo Window") then ImGui.ShowDemoWindow() end
        if ImGui.Button("Show About Window") then ImGui.ShowAboutWindow() end
        if ImGui.Button("Show Metrics Window") then ImGui.ShowMetricsWindow() end
        if ImGui.Button("Show Style Editor") then ImGui.ShowStyleEditor() end
        if ImGui.Button("Show User Guide") then ImGui.ShowUserGuide() end

        -- ImGui.ShowFontSelector("Font Selector") -- Requires font atlas

        ImGui.End()
    end
end)
```

### 🌐 UNCATEGORIZED

```lua
AddHook("OnDraw", "ImGui_Uncategorized_Sample", function()
    if ImGui.Begin("Uncategorized Functions") then
        ImGui.Text("Calculated Item Width: " .. tostring(ImGui.CalcItemWidth()))

        if ImGui.CollapsingHeader("Collapsing Header") then
            ImGui.Text("Header content here.")
        end

        local color_float = ImVec4(0.5, 0.2, 0.8, 1.0)
        local color_u32 = ImGui.ColorConvertFloat4ToU32(color_float)
        ImGui.Text(string.format("Float4 to U32: %x", color_u32))
        local converted_float = ImGui.ColorConvertU32ToFloat4(color_u32)
        ImGui.Text(string.format("U32 to Float4: %.2f,%.2f,%.2f,%.2f", converted_float.x, converted_float.y, converted_float.z, converted_float.w))
        
        local h,s,v = ImGui.ColorConvertRGBtoHSV(color_float.x, color_float.y, color_float.z)
        ImGui.Text(string.format("RGB to HSV: %.2f,%.2f,%.2f", h,s,v))
        local r,g,b = ImGui.ColorConvertHSVtoRGB(h,s,v)
        ImGui.Text(string.format("HSV to RGB: %.2f,%.2f,%.2f", r,g,b))

        ImGui.Dummy(ImVec2(50, 50))
        ImGui.Text("Dummy space above.")

        ImGui.Text("Get Color U32 (Red): " .. tostring(ImGui.GetColorU32(ImVec4(1,0,0,1))))

        ImGui.Text("Column Index: " .. tostring(ImGui.GetColumnIndex()))
        -- ImGui.SetColumnOffset(0, 100) -- Set offset for column 0
        -- ImGui.SetColumnWidth(0, 150) -- Set width for column 0
        ImGui.Text("Column Width: " .. tostring(ImGui.GetColumnWidth()))
        ImGui.Text("Column Offset: " .. tostring(ImGui.GetColumnOffset()))

        ImGui.Text("Font Size: " .. tostring(ImGui.GetFontSize()))
        -- ImGui.GetFontTexUvWhitePixel() -- Returns UV coord for white pixel

        ImGui.Text("Get ID for 'MyItem': " .. tostring(ImGui.GetID("MyItem")))

        ImGui.Text("Mouse Clicked Count (Left): " .. tostring(ImGui.GetMouseClickedCount(ImGui.MouseButton.Left)))
        ImGui.Text("Mouse Cursor: " .. tostring(ImGui.GetMouseCursor()))
        ImGui.SetMouseCursor(ImGui.MouseCursor.Hand)
        ImGui.Text("Mouse Cursor set to Hand.")

        ImGui.Text("Scroll X: " .. tostring(ImGui.GetScrollX()) .. ", MaxX: " .. tostring(ImGui.GetScrollMaxX()))
        ImGui.Text("Scroll Y: " .. tostring(ImGui.GetScrollY()) .. ", MaxY: " .. tostring(ImGui.GetScrollMaxY()))
        -- ImGui.SetScrollX(10)
        -- ImGui.SetScrollY(20)
        -- ImGui.SetScrollHereX(0.5) -- Scroll to 50% horizontally
        -- ImGui.SetScrollHereY(0.5) -- Scroll to 50% vertically
        -- ImGui.SetScrollFromPosX(100)
        -- ImGui.SetScrollFromPosY(100)

        ImGui.Text("Time: " .. tostring(ImGui.GetTime()))

        if ImGui.IsAnyItemActive() then ImGui.Text("Any Item Active") end
        if ImGui.IsAnyItemFocused() then ImGui.Text("Any Item Focused") end
        if ImGui.IsAnyItemHovered() then ImGui.Text("Any Item Hovered") end
        if ImGui.IsAnyMouseDown() then ImGui.Text("Any Mouse Down") end
        if ImGui.IsMouseDoubleClicked(ImGui.MouseButton.Left) then ImGui.Text("Left Mouse Double Clicked!") end
        if ImGui.IsMouseHoveringRect(ImVec2(10,10), ImVec2(50,50)) then ImGui.Text("Mouse hovering a specific rect") end
        if ImGui.IsPopupOpen("my_popup") then ImGui.Text("My Popup is Open") end
        if ImGui.IsRectVisible(ImVec2(0,0), ImVec2(100,100)) then ImGui.Text("Rect (0,0)-(100,100) is visible") end

        -- Logging (usually for debug output to console/file/clipboard)
        -- ImGui.LogToClipboard()
        -- ImGui.LogToFile(file_ptr)
        -- ImGui.LogToTTY()
        -- ImGui.LogFinish()

        ImGui.PushItemWidth(100)
        ImGui.InputText("Fixed Width Input", "")
        ImGui.PopItemWidth()

        -- ImGui.PushClipRect(ImVec2(100,100), ImVec2(200,200), false)
        -- ImGui.PopClipRect()

        -- Set Window Properties
        -- ImGui.SetWindowCollapsed(true, ImGui.Cond.Once)
        -- ImGui.SetWindowFocus()
        -- ImGui.SetWindowFontScale(1.5)
        -- ImGui.SetWindowPos(ImVec2(200,200), ImGui.Cond.Always)
        -- ImGui.SetWindowSize(ImVec2(400,300), ImGui.Cond.Always)

        ImGui.ShowDebugLogWindow()
        ImGui.ShowStackToolWindow()

        -- Table Functions (more detailed control)
        if ImGui.BeginTable("DetailedTable", 2) then
            ImGui.TableSetupColumn("A")
            ImGui.TableSetupColumn("B")
            ImGui.TableHeadersRow()

            ImGui.TableNextRow()
            ImGui.TableSetColumnIndex(0)
            ImGui.Text("Cell 1A")
            ImGui.TableSetColumnIndex(1)
            ImGui.Text("Cell 1B")
            ImGui.TableSetBgColor(ImGui.TableBgTarget.RowBg1, ImGui.ColorConvertFloat4ToU32(ImVec4(0.2,0.2,0.2,1)), 0)

            ImGui.TableNextRow()
            ImGui.TableSetColumnIndex(0)
            ImGui.Text("Cell 2A")
            ImGui.TableSetBgColor(ImGui.TableBgTarget.CellBg, ImGui.ColorConvertFloat4ToU32(ImVec4(0.5,0,0,1)), 0)
            ImGui.TableSetColumnIndex(1)
            ImGui.Text("Cell 2B")

            ImGui.Text("Column Count: " .. tostring(ImGui.TableGetColumnCount()))
            ImGui.Text("Column Flags (0): " .. tostring(ImGui.TableGetColumnFlags(0)))
            ImGui.Text("Column Name (1): " .. tostring(ImGui.TableGetColumnName(1)))
            ImGui.Text("Row Index: " .. tostring(ImGui.TableGetRowIndex()))
            
            -- ImGui.TableSetColumnEnabled(0, false)
            -- ImGui.TableSetupScrollFreeze(1,1)

            ImGui.EndTable()
        end

        ImGui.SetTabItemClosed("Tab 1") -- For programmatically closing tabs

        ImGui.TreePush("Manual Tree Push")
        ImGui.Text("Inside pushed tree.")
        ImGui.TreePop()

        ImGui.End()
    end
end)
```

## 🗂️ TABLES/ENUMS

### ImGui.BG (Background DrawList functions)

```lua
AddHook("OnDraw", "ImGui_BG_Sample", function()
    -- These functions draw on the background layer, behind all windows.
    -- Example: Drawing a large red circle in the background
    ImGui.BG.AddCircleFilled(ImVec2(200, 200), 50, ImGui.ColorConvertFloat4ToU32(ImVec4(1, 0, 0, 0.5)), 0)
    ImGui.BG.AddRect(ImVec2(250, 150), ImVec2(350, 250), ImGui.ColorConvertFloat4ToU32(ImVec4(0, 1, 0, 0.5)), 0, ImGui.DrawFlags.RoundCornersAll, 2.0)
    ImGui.BG.AddLine(ImVec2(10,10), ImVec2(50,50), ImGui.ColorConvertFloat4ToU32(ImVec4(1,1,0,1)), 2.0)
    ImGui.BG.AddText(ImVec2(10,100), ImGui.ColorConvertFloat4ToU32(ImVec4(1,1,1,1)), "Background Text")
end)
```

### ImGui.Col (Color Identifiers)

```lua
AddHook("OnDraw", "ImGui_Col_Sample", function()
    if ImGui.Begin("Color Examples") then
        ImGui.Text("Default text.")
        ImGui.PushStyleColor(ImGui.Col.Text, ImGui.ColorConvertFloat4ToU32(ImVec4(1, 0, 0, 1))) -- Set text color to red
        ImGui.Text("Red text (ImGui.Col.Text).")
        ImGui.PopStyleColor()

        ImGui.PushStyleColor(ImGui.Col.Button, ImGui.ColorConvertFloat4ToU32(ImVec4(0, 0.5, 0.8, 1)))
        ImGui.Button("Custom Button Color (ImGui.Col.Button)")
        ImGui.PopStyleColor()

        ImGui.PushStyleColor(ImGui.Col.WindowBg, ImGui.ColorConvertFloat4ToU32(ImVec4(0.1, 0.1, 0.1, 0.8)))
        if ImGui.BeginChild("CustomBgChild", ImVec2(0, 50), true) then
            ImGui.Text("This child has custom background.")
            ImGui.EndChild()
        end
        ImGui.PopStyleColor()

        ImGui.Text("Accessing a color enum: " .. tostring(ImGui.Col.TitleBg))
        ImGui.End()
    end
end)
```

### ImGui.Cond (Condition Flags)

```lua
AddHook("OnDraw", "ImGui_Cond_Sample", function()
    if ImGui.Begin("Condition Flags") then
        -- Window will only appear at this position the very first time.
        ImGui.SetNextWindowPos(ImVec2(50, 50), ImGui.Cond.FirstUseEver)
        -- Window size will always be set to this.
        ImGui.SetNextWindowSize(ImVec2(300, 200), ImGui.Cond.Always)

        ImGui.Text("Window properties set with conditions.")
        ImGui.End()
    end
end)
```

### ImGui.DataType (Data Type Identifiers)

```lua
AddHook("OnDraw", "ImGui_DataType_Sample", function()
    if ImGui.Begin("Data Type Example") then
        local my_int = 123
        -- ImGui.DragScalar("My S32", ImGui.DataType.S32, my_int_ptr, 1, 0, 200) -- Example, requires pointer

        ImGui.Text("DataType.Float: " .. tostring(ImGui.DataType.Float))
        ImGui.Text("DataType.S32: " .. tostring(ImGui.DataType.S32))
        ImGui.End()
    end
end)
```

### ImGui.Dir (Direction Flags)

```lua
AddHook("OnDraw", "ImGui_Dir_Sample", function()
    if ImGui.Begin("Direction Example") then
        if ImGui.ArrowButton("Left Arrow", ImGui.Dir.Left) then ImGui.Text("Left pressed!") end
        ImGui.SameLine()
        if ImGui.ArrowButton("Right Arrow", ImGui.Dir.Right) then ImGui.Text("Right pressed!") end
        ImGui.SameLine()
        if ImGui.ArrowButton("Up Arrow", ImGui.Dir.Up) then ImGui.Text("Up pressed!") end
        ImGui.SameLine()
        if ImGui.ArrowButton("Down Arrow", ImGui.Dir.Down) then ImGui.Text("Down pressed!") end
        ImGui.End()
    end
end)
```

### ImGui.DrawFlags (Drawing Flags)

```lua
AddHook("OnDraw", "ImGui_DrawFlags_Sample", function()
    if ImGui.Begin("Draw Flags Example") then
        local draw_list = ImGui.GetWindowDrawList()
        local p = ImGui.GetCursorScreenPos()

        -- Rounded rectangle
        draw_list:AddRectFilled(ImVec2(p.x, p.y), ImVec2(p.x + 100, p.y + 50), ImGui.ColorConvertFloat4ToU32(ImVec4(0,1,0,1)), 10.0, ImGui.DrawFlags.RoundCornersTopLeft + ImGui.DrawFlags.RoundCornersBottomRight)
        ImGui.Dummy(ImVec2(100, 50)) -- Advance cursor

        ImGui.Text("Rectangle above has top-left & bottom-right corners rounded.")
        ImGui.End()
    end
end)
```

### ImGui.DrawListFlags (DrawList Behavior Flags)

```lua
AddHook("OnDraw", "ImGui_DrawListFlags_Sample", function()
    if ImGui.Begin("DrawList Flags Example") then
        ImGui.Text("These flags control rendering quality.")
        ImGui.Text("e.g., ImGui.DrawListFlags.AntiAliasedLines makes lines smoother.")
        ImGui.Text("Usually set globally or on specific draw lists.")
        ImGui.End()
end)
```

### ImGui.FG (Foreground DrawList functions)

```lua
AddHook("OnDraw", "ImGui_FG_Sample", function()
    -- These functions draw on the foreground layer, over all windows.
    -- Example: Drawing a blue square in the foreground
    ImGui.FG.AddRectFilled(ImVec2(50, 50), ImVec2(150, 150), ImGui.ColorConvertFloat4ToU32(ImVec4(0, 0, 1, 0.7)), 0, ImGui.DrawFlags.RoundCornersAll)
    ImGui.FG.AddCircle(ImVec2(100,100), 70, ImGui.ColorConvertFloat4ToU32(ImVec4(1,1,0,1)), 0, 2.0)
    ImGui.FG.AddText(ImVec2(100,60), ImGui.ColorConvertFloat4ToU32(ImVec4(1,1,1,1)), "Foreground Text")
end)
```

### ImGui.InputTextFlags (InputText Behavior Flags)

```lua
AddHook("OnDraw", "ImGui_InputTextFlags_Sample", function()
    if ImGui.Begin("InputText Flags Example") then
        local text1 = "Read Only Text"
        ImGui.InputText("ReadOnly", text1, ImGui.InputTextFlags.ReadOnly)

        local text2 = "Password"
        local changed, new_text2 = ImGui.InputText("Password", text2, ImGui.InputTextFlags.Password)
        if changed then text2 = new_text2 end

        local text3 = "Numbers only"
        local changed, new_text3 = ImGui.InputText("Numbers", text3, ImGui.InputTextFlags.CharsDecimal)
        if changed then text3 = new_text3 end

        ImGui.Text("Flags combine with bitwise OR (|) operator.")
        ImGui.End()
    end
end)
```

### ImGui.MouseButton (Mouse Button Identifiers)

```lua
AddHook("OnDraw", "ImGui_MouseButton_Sample", function()
    if ImGui.Begin("Mouse Button Example") then
        if ImGui.IsMouseClicked(ImGui.MouseButton.Left) then ImGui.Text("Left Mouse Button Clicked!") end
        if ImGui.IsMouseClicked(ImGui.MouseButton.Right) then ImGui.Text("Right Mouse Button Clicked!") end
        if ImGui.IsMouseClicked(ImGui.MouseButton.Middle) then ImGui.Text("Middle Mouse Button Clicked!") end
        ImGui.End()
    end
end)
```

### ImGui.MouseCursor (Mouse Cursor Types)

```lua
AddHook("OnDraw", "ImGui_MouseCursor_Sample", function()
    if ImGui.Begin("Mouse Cursor Example") then
        ImGui.Text("Move mouse over buttons to see different cursors.")

        if ImGui.Button("Arrow Cursor") then ImGui.SetMouseCursor(ImGui.MouseCursor.Arrow) end
        ImGui.SameLine()
        if ImGui.Button("TextInput Cursor") then ImGui.SetMouseCursor(ImGui.MouseCursor.TextInput) end
        ImGui.SameLine()
        if ImGui.Button("Hand Cursor") then ImGui.SetMouseCursor(ImGui.MouseCursor.Hand) end
        ImGui.SameLine()
        if ImGui.Button("NotAllowed Cursor") then ImGui.SetMouseCursor(ImGui.MouseCursor.NotAllowed) end
        ImGui.End()
    end
end)
```

### ImGui.SortDirection (Table Sort Direction)

```lua
AddHook("OnDraw", "ImGui_SortDirection_Sample", function()
    if ImGui.Begin("Sort Direction Example") then
        ImGui.Text("Used with ImGui tables for column sorting.")
        ImGui.Text("None: " .. tostring(ImGui.SortDirection.None))
        ImGui.Text("Ascending: " .. tostring(ImGui.SortDirection.Ascending))
        ImGui.Text("Descending: " .. tostring(ImGui.SortDirection.Descending))
        ImGui.End()
    end
end)
```

### ImGui.StyleVar (Style Variable Identifiers)

```lua
AddHook("OnDraw", "ImGui_StyleVar_Sample", function()
    if ImGui.Begin("StyleVar Example") then
        ImGui.Text("Normal Frame Padding.")
        ImGui.PushStyleVar(ImGui.StyleVar.FramePadding, ImVec2(20, 20))
        ImGui.Button("Large Padding Button")
        ImGui.PopStyleVar()

        ImGui.Text("Normal Window Rounding.")
        ImGui.PushStyleVar(ImGui.StyleVar.WindowRounding, 0.0)
        if ImGui.BeginChild("SquareChild", ImVec2(0,50), true) then
            ImGui.Text("This child has square corners.")
            ImGui.EndChild()
        end
        ImGui.PopStyleVar()
        ImGui.End()
    end
end)
```

### ImGui.TableBgTarget (Table Background Target)

```lua
AddHook("OnDraw", "ImGui_TableBgTarget_Sample", function()
    if ImGui.Begin("Table Bg Target") then
        if ImGui.BeginTable("BgTable", 2) then
            ImGui.TableSetupColumn("Header A")
            ImGui.TableSetupColumn("Header B")
            ImGui.TableHeadersRow()

            ImGui.TableNextRow()
            ImGui.TableSetBgColor(ImGui.TableBgTarget.RowBg0, ImGui.ColorConvertFloat4ToU32(ImVec4(0.1,0.5,0.1,1)))
            ImGui.TableNextColumn(); ImGui.Text("Row 0, Col A")
            ImGui.TableNextColumn(); ImGui.Text("Row 0, Col B")

            ImGui.TableNextRow()
            ImGui.TableSetBgColor(ImGui.TableBgTarget.RowBg1, ImGui.ColorConvertFloat4ToU32(ImVec4(0.1,0.1,0.5,1)))
            ImGui.TableNextColumn(); ImGui.Text("Row 1, Col A")
            ImGui.TableNextColumn(); ImGui.Text("Row 1, Col B")

            ImGui.TableNextRow()
            ImGui.TableNextColumn(); ImGui.Text("Row 2, Col A")
            ImGui.TableSetBgColor(ImGui.TableBgTarget.CellBg, ImGui.ColorConvertFloat4ToU32(ImVec4(0.8,0.2,0.2,1)))
            ImGui.TableNextColumn(); ImGui.Text("Row 2, Col B (custom bg)")
            ImGui.EndTable()
        end
        ImGui.End()
    end
end)
```

### ImGui.WindowFlags (Window Behavior Flags)

```lua
AddHook("OnDraw", "ImGui_WindowFlags_Sample", function()
    -- Example with multiple flags
    if ImGui.Begin("Borderless & Non-Resizable Window", nil, ImGui.WindowFlags.NoTitleBar + ImGui.WindowFlags.NoResize + ImGui.WindowFlags.AlwaysAutoResize) then
        ImGui.Text("This window has no title bar, cannot be resized, and auto-resizes to content.")
        ImGui.Button("A Button")
        ImGui.End()
    end

    if ImGui.Begin("Transparent Background", nil, ImGui.WindowFlags.NoBackground) then
        ImGui.Text("This window has no background.")
        ImGui.Text("Only content is visible.")
        ImGui.End()
    end

    -- Tooltip flag for specific tooltip-like windows
    -- ImGui.Begin("MyTooltip", nil, ImGui.WindowFlags.Tooltip)

    -- Modal windows are usually opened with ImGui.BeginPopupModal
    -- Child windows are opened with ImGui.BeginChild
end)
```

---

## 🌐 GLOBAL IMGUI FUNCTIONS

These are global functions that are not part of the `ImGui` table but are essential for creating vectors.

```lua
AddHook("OnDraw", "ImGui_GlobalFunctions_Sample", function()
    if ImGui.Begin("Global Functions") then
        -- ImVec2: Used for sizes and 2D positions (x, y)
        local size_vec = ImVec2(100, 50)
        ImGui.Button("Button with Size", size_vec)

        -- ImVec4: Used for colors (r, g, b, a) or 4D vectors
        local color_vec = ImVec4(1.0, 0.5, 0.0, 1.0) -- Orange color
        ImGui.TextColored(color_vec, "Orange Text")
        ImGui.End()
    end
end)
```

---

## ⚡ QUICK REFERENCE

**WINDOW MANAGEMENT:**
```lua
AddHook("OnDraw", "QuickRef_Window", function()
  if ImGui.Begin("Window Title") then
    -- Your content here
    ImGui.Text("Hello from Quick Reference Window!")
    ImGui.End()
  end
end)
```

**COMMON WIDGETS:**
```lua
AddHook("OnDraw", "QuickRef_Widgets", function()
  if ImGui.Begin("Quick Ref Widgets") then
    ImGui.Text("Hello World")

    if ImGui.Button("Click Me") then -- returns true when clicked
      -- Button was pressed
      log("Button clicked!")
    end

    local slider_val = 50.0
    local changed, new_slider_val = ImGui.SliderFloat("Slider", slider_val, 0.0, 100.0)
    if changed then slider_val = new_slider_val end
    ImGui.Text("Slider Value: " .. tostring(slider_val))
    ImGui.End()
  end
end)
```

**GLOBAL HELPERS:**
```lua
AddHook("OnDraw", "QuickRef_Helpers", function()
  if ImGui.Begin("Quick Ref Helpers") then
    local rect_size = ImVec2(150, 40)     -- For sizes and positions
    ImGui.Button("Sized Button", rect_size)

    local text_color = ImVec4(1.0, 0.0, 0.0, 1.0)        -- For colors (0.0-1.0 range)
    ImGui.TextColored(text_color, "Red text example")
    ImGui.End()
  end
end)
```

---

```
