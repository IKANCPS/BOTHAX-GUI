# CALL HOOK
```markdown
1.hook_type = "OnDraw", "draw"
2.hook_name = bebas
```

EXAMPLE :
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
