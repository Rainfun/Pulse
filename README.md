# Pulse Documentation
Created by .kollinxd on discord

## Issues & Suggestions

Found a bug or want a feature? Join the discord.

**Pulse Discord:** https://discord.gg/4R4wTGJjz5

We actually read suggestions and fix bugs pretty fast.

## Installation

```lua
local Pulse = loadstring(game:HttpGet("https://raw.githubusercontent.com/Rainfun/Pulse/refs/heads/main/A/Pulse",true))()
```

---

## Basic Usage

```lua
local window = Pulse:CreateWindow({
    Name = "My Hub",
    Theme = "Dark"
})

local tab = window:CreateTab({
    Name = "Main",
    Icon = "home"
})

tab:CreateButton({
    Name = "Test Button",
    Callback = function()
        print("works")
    end
})
```

That's it. You now have a working UI.

---

## Window Creation

```lua
local window = Pulse:CreateWindow({
    Name = "Hub Name",
    Theme = "Dark",  -- Dark, Light, Ocean, Purple
    Size = UDim2.new(0, 550, 0, 450),  -- optional
    Position = UDim2.new(0.5, 0, 0.5, 0),  -- optional
    Icon = "home",  -- optional
    MinimizeKey = Enum.KeyCode.RightControl  -- optional
})
```

### Window Functions

**Toggle visibility**
```lua
window:Toggle()
```

**Destroy window**
```lua
window:Destroy()
```

**Change theme**
```lua
window:SetTheme("Ocean")
```

**Send notification**
```lua
window:Notify({
    Title = "Title",
    Text = "Message here",
    Duration = 3,
    Type = "success"  -- info, success, warning, error
})
```

**Create tab**
```lua
local tab = window:CreateTab({
    Name = "Tab Name",
    Icon = "home"
})
```

---

## Components

### Section
Just a divider with text. Good for organizing.

```lua
tab:CreateSection("Section Name")
```

### Button
Does what you think it does.

```lua
tab:CreateButton({
    Name = "Button",
    Description = "does a thing",  -- optional
    Icon = "zap",  -- optional
    Callback = function()
        -- your code
    end
})
```

### Toggle
On/off switch.

```lua
local toggle = tab:CreateToggle({
    Name = "Feature Name",
    Description = "turns on feature",  -- optional
    Icon = "toggle-left",  -- optional
    Default = false,
    Callback = function(value)
        if value then
            print("enabled")
        else
            print("disabled")
        end
    end
})

toggle:SetValue(true)  -- change state
```

### Slider
Draggable value selector.

```lua
local slider = tab:CreateSlider({
    Name = "Speed",
    Min = 16,
    Max = 200,
    Default = 16,
    Increment = 1,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
    end
})

slider:SetValue(50)  -- set value
```

### Dropdown
Pick from a list.

```lua
local dropdown = tab:CreateDropdown({
    Name = "Select Option",
    Options = {"Option 1", "Option 2", "Option 3"},
    Default = "Option 1",
    Callback = function(value)
        print("selected:", value)
    end
})

dropdown:SetValue("Option 2")  -- change selection
dropdown:Toggle()  -- open/close manually
```

### TextBox
Text input.

```lua
local textbox = tab:CreateTextBox({
    Name = "Enter Text",
    Placeholder = "type here...",  -- optional
    Default = "",
    Callback = function(text)
        print("entered:", text)
    end
})

textbox:SetValue("new text")  -- set text
```

### Keybind
Let users set their own keybinds.

```lua
local keybind = tab:CreateKeybind({
    Name = "Keybind",
    Default = Enum.KeyCode.E,
    Callback = function(key)
        print("pressed:", key.Name)
    end
})

keybind:SetValue(Enum.KeyCode.Q)  -- change key
```

The callback fires whenever the key is pressed.

### Color Picker
Full HSV color selector with RGB inputs.

```lua
local picker = tab:CreateColorPicker({
    Name = "Color",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(color)
        print(color.R, color.G, color.B)
    end
})

picker:SetValue(Color3.fromRGB(0, 255, 0))  -- change color
picker:Toggle()  -- open/close picker
```

### Label
Simple text display. Updates dynamically.

```lua
local label = tab:CreateLabel("Some text here")

label:SetText("new text")  -- update text
```

### Paragraph
Text with a title. Auto-sizes based on content.

```lua
local para = tab:CreateParagraph({
    Title = "Info",
    Content = "Some longer text that wraps automatically. You can put whatever here."
})

para:SetTitle("New Title")
para:SetContent("Updated text")
```

---

## Themes

Built-in themes: `Dark`, `Light`, `Ocean`, `Purple`

### Using built-in themes
```lua
window:SetTheme("Ocean")
```

### Custom themes
```lua
window:SetTheme({
    Primary = Color3.fromRGB(0, 0, 0),
    Secondary = Color3.fromRGB(10, 10, 10),
    Accent = Color3.fromRGB(34, 197, 94),
    AccentHover = Color3.fromRGB(40, 220, 105),
    Text = Color3.fromRGB(255, 255, 255),
    TextDim = Color3.fromRGB(180, 180, 180),
    TextDark = Color3.fromRGB(120, 120, 120),
    Border = Color3.fromRGB(60, 60, 60),
    BorderLight = Color3.fromRGB(80, 80, 80),
    Background = Color3.fromRGB(5, 5, 5),
    Hover = Color3.fromRGB(20, 20, 20),
    Error = Color3.fromRGB(220, 38, 38),
    Success = Color3.fromRGB(34, 197, 94),
    Warning = Color3.fromRGB(251, 191, 36),
    Info = Color3.fromRGB(59, 130, 246)
})
```

You need all the properties or it'll break. Just copy the template above and change colors.

---

## Icons

Pulse uses Lucide icons. Over 1000+ available.

Common ones: `home`, `settings`, `eye`, `zap`, `shield`, `arrow-up`, `plane`, `crosshair`, `star`, `heart`, `user`, `lock`, `package`, `trash`, `copy`, `save`

Full list: https://lucide.dev/icons/

If an icon doesn't load, it falls back to a default package icon.

---

## Complete Example

```lua
local Pulse = loadstring(game:HttpGet("https://raw.githubusercontent.com/Rainfun/Pulse/refs/heads/main/A/Pulse",true))()

local window = Pulse:CreateWindow({
    Name = "Example Hub",
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.RightControl
})

-- Main tab
local main = window:CreateTab({
    Name = "Main",
    Icon = "home"
})

main:CreateSection("Player")

local speedSlider = main:CreateSlider({
    Name = "Walk Speed",
    Min = 16,
    Max = 200,
    Default = 16,
    Increment = 1,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
    end
})

local jumpSlider = main:CreateSlider({
    Name = "Jump Power",
    Min = 50,
    Max = 200,
    Default = 50,
    Increment = 1,
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
    end
})

main:CreateSection("Combat")

local autoFarm = main:CreateToggle({
    Name = "Auto Farm",
    Default = false,
    Callback = function(value)
        _G.AutoFarm = value
    end
})

-- Settings tab
local settings = window:CreateTab({
    Name = "Settings",
    Icon = "settings"
})

settings:CreateSection("UI")

local themeDropdown = settings:CreateDropdown({
    Name = "Theme",
    Options = {"Dark", "Light", "Ocean", "Purple"},
    Default = "Dark",
    Callback = function(value)
        window:SetTheme(value)
    end
})

local notifToggle = settings:CreateToggle({
    Name = "Notifications",
    Default = true,
    Callback = function(value)
        _G.NotificationsEnabled = value
    end
})

-- Show startup notification
window:Notify({
    Title = "Loaded",
    Text = "Hub initialized successfully",
    Duration = 3,
    Type = "success"
})
```

---

## Mobile Support

Everything automatically adjusts for mobile. Dropdowns and color pickers work with touch. No extra code needed.

---

## Tips

- Use sections to organize your UI
- Don't spam notifications, they stack up
- Keybinds only work on PC (obviously)
- Color pickers can get laggy if you spam them
- The UI saves position when dragged
- Minimize key defaults to RightControl

---

## Support

If this library helped your project, consider supporting my project:

**Perplexity:** https://discord.gg/nJwxBbAYw6

Thanks for using Pulse UI.

---

*Last updated: 10/30/2025 5:35 pm*
