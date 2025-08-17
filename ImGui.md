# 🎨 ImGui Lua - Template Dasar

```lua
local hook_type = "OnDraw"
local hook_name = "my_imgui"

-- Cara 1: Fungsi Terpisah
function imGui()
    ImGui.Begin("My Window")
    ImGui.Text("Hello from function!")
    if ImGui.Button("Click Me") then
        LogToConsole("Button ditekan!")
    end
    ImGui.End()
end
AddHook(hook_type, hook_name, imGui)

-- Cara 2: Fungsi Anonim
AddHook(hook_type, hook_name, function()
    ImGui.Begin("My Window")
    ImGui.Text("Hello from inline function!")
    if ImGui.Button("Click Me Too") then
        LogToConsole("Button inline ditekan!")
    end
    ImGui.End()
end)
