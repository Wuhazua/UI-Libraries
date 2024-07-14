# Fluent UI
This documentation is for Fluent UI Credit To dawid

## Booting the Fluent UI Library
```lua
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
```

## Accessibility
```lua
function Init()
    local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
end

function Test()
    print(Fluent.Options)
end

Init()
Test()
```

## Creating a Window
```lua
local Window = Fluent:CreateWindow({
    Title = "Fluent " .. Fluent.Version,
    SubTitle = "by dawid",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when theres no MinimizeKeybind
})
```

## Creating Options
```lua
local Options = Fluent.Options
```

## Creating Notifications
```lua
Fluent:Notify({
        Title = "Notification",
        Content = "This is a notification",
        SubContent = "SubContent", -- Optional
        Duration = 5 -- Set to nil to make the notification not disappear
})
```

## Creating Dialogs
```lua
Window:Dialog({
    Title = "Title",
    Content = "This is a dialog",
    Buttons = {
        { 
            Title = "Confirm",
            Callback = function()
                print("Confirmed the dialog.")
            end 
        }, {
            Title = "Cancel",
            Callback = function()
                print("Cancelled the dialog.")
            end 
        }
    }
})
```

## Tab Icons 
https://lucide.dev/icons/

## Creating Tabs
```lua
-- Fluent provides Lucide Icons, they are optional
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}
```

## Tab (Settings) With Interface And Configs
```lua
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)
```

## Selecting Main Tab (Do this to avoid being on the "New Tab" when you execute the UI.)
```lua
Window:SelectTab(1)
```

## Creating Sections
```lua
local Section = Tab:AddSection("Section Name")
```

## Creating Paragraphs
```lua
Tab:AddParagraph({
    Title = "Paragraph",
    Content = "This is a paragraph.\nSecond line!"
})
```

## Creating Buttons
```lua
Tab:AddButton({
    Title = "Button",
    Description = "Very important button",
    Callback = function()
        print("Hello, world!")
    end
})
```

## Creating Toggles
```lua
local Toggle = Tab:AddToggle("MyToggle", 
{
    Title = "Toggle", 
    Description = "Toggle description",
    Default = false
    Callback = function(state)
	if state then
	    print("Toggle On")
	else
	    print("Toggle Off")
        end
    end 
})
```

## Event Handling
```lua
Toggle:OnChanged(function()
    print("Toggle changed:", Options.MyToggle.Value)
end)
```

## Changing Value
```lua
Toggle:SetValue(false)
```

## Creating Sliders
```lua
local Slider = Tab:AddSlider("Slider", 
{
    Title = "Slider",
    Description = "This is a slider",
    Default = 2,
    Min = 0,
    Max = 5,
    Rounding = 1,
    Callback = function(Value)
        print("Slider was changed:", Value)
    end
})
```

## Event Handling
```lua
Slider:OnChanged(function(Value)
    print("Slider changed:", Value)
end)
```

## Changing Value
```lua
Slider:SetValue(3)
```

## Creating Dropdowns
```lua
local Dropdown = Tab:AddDropdown("Dropdown", {
    Title = "Dropdown",
    Description = "Dropdown description",
    Values = {"one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen"},
    Multi = false,
    Default = 1,
})
```

## Event Handling
```lua
Dropdown:OnChanged(function(Value)
    print("Dropdown changed:", Value)
end)
```

## Changing Value 
```lua
Dropdown:SetValue("four")
```

## Creating ColorPickers
```lua
local Colorpicker = Tab:AddColorpicker("Colorpicker", {
    Title = "Colorpicker",
    Description = "Description for colorpicker",
    Default = Color3.fromRGB(96, 205, 255)
})

Colorpicker:OnChanged(function()
    print("Colorpicker changed:", Colorpicker.Value)
end)
    
Colorpicker:SetValueRGB(Color3.fromRGB(0, 255, 140))
```

## Transparency Colorpicker
```lua
local TColorpicker = Tab:AddColorpicker("TransparencyColorpicker", {
    Title = "Colorpicker",
    Description = "but you can change the transparency.",
    Transparency = 0,
    Default = Color3.fromRGB(96, 205, 255)
})
```

## Event Handling
```lua
Colorpicker:OnChanged(function()
    print("Colorpicker changed:", Colorpicker.Value)
end)

TColorpicker:OnChanged(function()
    print(
        "TColorpicker changed:", TColorpicker.Value,
        "Transparency:", TColorpicker.Transparency
    )
end)
```

## Creating Keybinds
```lua
local Keybind = Tab:AddKeybind("Keybind", {
    Title = "Keybind",
    Description = "Keybind Description",
    Mode = "Toggle", -- Always, Toggle, Hold
    Default = "LeftControl", -- String as the name of the keybind (MB1, MB2 for mouse buttons)

    -- Occurs when the keybind is clicked, Value is `true`/`false`
    Callback = function(Value)
        print("Keybind clicked!", Value)
    end,

    -- Occurs when the keybind itself is changed, `New` is a KeyCode Enum OR a UserInputType Enum
    ChangedCallback = function(New)
        print("Keybind changed!", New)
    end
})
``` 

## Event Handling
```lua
-- OnClick is only fired when you press the keybind and the mode is Toggle
-- Otherwise, you will have to use Keybind:GetState()
Keybind:OnClick(function()
    print("Keybind clicked:", Keybind:GetState())
end)

Keybind:OnChanged(function()
    print("Keybind changed:", Keybind.Value)
end)

task.spawn(function()
    while true do
        wait(1)
        -- example for checking if a keybind is being pressed
        local state = Keybind:GetState()
        if state then
            print("Keybind is being held down")
        end

        if Fluent.Unloaded then break end
    end
end)
```

## Creating Inputs
```lua
local Input = Tab:AddInput("Input", {
    Title = "Input",
    Description = "Input Description",
    Default = "Default",
    Placeholder = "Placeholder",
    Numeric = false, -- Only allows numbers
    Finished = false, -- Only calls callback when you press enter
    Callback = function(Value)
        print("Input changed:", Value)
    end
})
```

## Event Handling
```lua
Input:OnChanged(function()
    print("Input updated:", Input.Value)
end)
```

## Toggle GUI Transparency
```lua
Fluent:ToggleTransparency(false) and Fluent:ToggleTransparency(true)
```

## Toggle Acrylic (Blur)
```lua
Fluent:ToggleAcrylic(false) or Fluent:ToggleAcrylic(true)
```

## Destroy Fluent
```lua
Fluent:Destroy()
```

## Save Manager (Auto Load Config)
```lua
SaveManager:LoadAutoloadConfig()
```

## Disable coroutines when exiting Fluent window
```lua
function Test()
    while task.wait() do
        print("something")
        if Fluent.Unloaded then break end
    end
end

coroutine.resume(coroutine.create(Test))
```

