hook_type = "OnDraw", "draw"

hook_name = bebas
```lua
function imGui()
-- code ImGui
end

AddHook(hook_type, hook_name, imGui)
```
```lua
AddHook(hook_type, hook_name, function()
-- code ImGui
end)
```
