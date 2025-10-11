# Prestige UI Library - Complete Documentation

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Getting Started](#getting-started)
4. [Core Functions](#core-functions)
5. [UI Components](#ui-components)
6. [Theming System](#theming-system)
7. [Advanced Features](#advanced-features)
8. [Examples](#examples)
9. [API Reference](#api-reference)

---

## Introduction

**Prestige UI** is a modern, feature-rich UI library for Roblox that provides a sleek and customizable interface system. It includes:

- 🎨 **15 Pre-built Themes** (Dark, Ocean, Sunset, Forest, Midnight, Purple, Cyberpunk, Neon, Minimal, Dracula, Nord, Monokai, Gruvbox, Tokyo, Rose)
- 🧩 **Comprehensive Component Library** (Buttons, Toggles, Sliders, Dropdowns, Text Boxes, etc.)
- 🔔 **Built-in Notification System**
- 🎭 **Smooth Animations** using TweenService
- 🔍 **Search Functionality**
- 🎯 **Draggable Windows**
- ⌨️ **Keybind Support**
- 📱 **Minimizable Interface**

---

## Installation

### Method 1: Direct Copy
```lua
-- Copy the entire PrestigeUI library code into your script
local PrestigeUI = loadstring(game:HttpGet("YOUR_SCRIPT_URL"))()
```

### Method 2: Local Module
```lua
-- Save the library as a ModuleScript and require it
local PrestigeUI = require(game.ReplicatedStorage.PrestigeUI)
```

---

## Getting Started

### Basic Setup

```lua
-- Load the library
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL"))()

-- Create a new UI window
local Window = PrestigeUI:Create("My Hub")

-- Create a tab
local MainTab = Window:AddTab("Main")

-- Add a button
Window:AddButton(MainTab, "Click Me!", function()
    print("Button clicked!")
end)
```

### Complete Example

```lua
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL"))()

-- Create window
local Window = PrestigeUI:Create("Prestige Hub")

-- Set theme
Window:SetTheme("Ocean")

-- Create tabs
local HomeTab = Window:AddTab("Home")
local SettingsTab = Window:AddTab("Settings")

-- Add components
Window:AddLabel(HomeTab, "Welcome to Prestige UI!", 18)
Window:AddButton(HomeTab, "Test Button", function()
    Window:Notify({
        Title = "Success",
        Message = "Button clicked!",
        Duration = 3,
        Type = "Success"
    })
end)

-- Add toggle
Window:AddToggle(SettingsTab, "Enable Feature", function(state)
    print("Toggle state:", state)
end)
```

---

## Core Functions

### PrestigeUI:Create(title)
Creates a new UI window.

**Parameters:**
- `title` (string, optional): Window title (default: "Prestige Hub")

**Returns:** Window object

**Example:**
```lua
local Window = PrestigeUI:Create("My Custom Hub")
```

---

### Window:AddTab(tabName)
Creates a new tab in the sidebar.

**Parameters:**
- `tabName` (string): Name of the tab

**Returns:** Content frame for the tab

**Example:**
```lua
local MainTab = Window:AddTab("Main")
local SettingsTab = Window:AddTab("Settings")
```

---

### Window:Close()
Closes and destroys the UI window with a smooth animation.

**Example:**
```lua
Window:Close()
```

---

## UI Components

### 1. Button

Creates a clickable button with hover effects.

**Syntax:**
```lua
Window:AddButton(parent, text, callback)
```

**Parameters:**
- `parent` (Frame): Parent container (usually a tab)
- `text` (string): Button text
- `callback` (function): Function to execute on click

**Example:**
```lua
Window:AddButton(MainTab, "Execute Script", function()
    print("Script executed!")
    Window:Notify({
        Title = "Success",
        Message = "Script executed successfully!",
        Type = "Success"
    })
end)
```

---

### 2. Label

Creates a text label for displaying information.

**Syntax:**
```lua
Window:AddLabel(parent, text, textSize)
```

**Parameters:**
- `parent` (Frame): Parent container
- `text` (string): Label text
- `textSize` (number, optional): Font size (default: 16)

**Example:**
```lua
Window:AddLabel(MainTab, "Welcome to Prestige UI!", 20)
Window:AddLabel(MainTab, "Version 1.0", 14)
```

---

### 3. Paragraph

Creates a formatted text block with a title and content.

**Syntax:**
```lua
Window:AddParagraph(parent, title, content)
```

**Parameters:**
- `parent` (Frame): Parent container
- `title` (string): Paragraph title
- `content` (string): Paragraph content

**Example:**
```lua
Window:AddParagraph(MainTab, "About", 
    "This is a comprehensive UI library with many features and customization options.")
```

---

### 4. Toggle

Creates a toggle switch with on/off states.

**Syntax:**
```lua
Window:AddToggle(parent, text, callback)
```

**Parameters:**
- `parent` (Frame): Parent container
- `text` (string): Toggle label
- `callback` (function): Function called with boolean state

**Returns:** Table with `Container`, `Toggle`, and `GetState()` function

**Example:**
```lua
local MyToggle = Window:AddToggle(MainTab, "Enable ESP", function(state)
    if state then
        print("ESP Enabled")
        -- Enable ESP code
    else
        print("ESP Disabled")
        -- Disable ESP code
    end
end)

-- Get current state
local isEnabled = MyToggle.GetState()
```

---

### 5. Slider

Creates a draggable slider for numeric input.

**Syntax:**
```lua
Window:AddSlider(parent, min, max, default, callback)
```

**Parameters:**
- `parent` (Frame): Parent container
- `min` (number): Minimum value
- `max` (number): Maximum value
- `default` (number): Default value
- `callback` (function): Function called with current value

**Returns:** Table with `Container` and `GetValue()` function

**Example:**
```lua
local SpeedSlider = Window:AddSlider(MainTab, 16, 100, 16, function(value)
    print("Speed set to:", value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)

-- Get current value
local currentSpeed = SpeedSlider.GetValue()
```

---

### 6. TextBox

Creates an input field for text entry.

**Syntax:**
```lua
Window:AddTextBox(parent, placeholder, callback)
```

**Parameters:**
- `parent` (Frame): Parent container
- `placeholder` (string): Placeholder text
- `callback` (function): Function called when Enter is pressed

**Returns:** TextBox object

**Example:**
```lua
local NameBox = Window:AddTextBox(MainTab, "Enter your name...", function(text)
    print("Name entered:", text)
    Window:Notify({
        Title = "Welcome",
        Message = "Hello, " .. text .. "!",
        Type = "Info"
    })
end)
```

---

### 7. Dropdown

Creates a dropdown menu with multiple options.

**Syntax:**
```lua
Window:AddDropdown(parent, placeholder, options, callback)
```

**Parameters:**
- `parent` (Frame): Parent container
- `placeholder` (string): Default text
- `options` (table): Array of option strings
- `callback` (function): Function called with selected option

**Example:**
```lua
Window:AddDropdown(MainTab, "Select Weapon", 
    {"Sword", "Bow", "Staff", "Axe"}, 
    function(selected)
        print("Selected weapon:", selected)
    end
)
```

---

### 8. Keybind

Creates a keybind selector.

**Syntax:**
```lua
Window:AddKeybind(parent, text, default, callback)
```

**Parameters:**
- `parent` (Frame): Parent container
- `text` (string): Keybind label
- `default` (Enum.KeyCode): Default key
- `callback` (function): Function called with selected key

**Returns:** Table with `Container` and `GetKey()` function

**Example:**
```lua
local Keybind = Window:AddKeybind(MainTab, "Toggle UI", Enum.KeyCode.RightShift, function(key)
    print("Keybind set to:", key.Name)
end)

-- Get current key
local currentKey = Keybind.GetKey()
```

---

### 9. Color Picker

Creates a color selection tool with RGB sliders.

**Syntax:**
```lua
Window:AddColorPicker(parent, text, default, callback)
```

**Parameters:**
- `parent` (Frame): Parent container
- `text` (string): Color picker label
- `default` (Color3): Default color
- `callback` (function): Function called with selected color

**Returns:** Table with `Container` and `GetColor()` function

**Example:**
```lua
local ColorPicker = Window:AddColorPicker(MainTab, "ESP Color", 
    Color3.fromRGB(0, 180, 255), 
    function(color)
        print("Color selected:", color)
        -- Apply color to ESP
    end
)

-- Get current color
local currentColor = ColorPicker.GetColor()
```

---

### 10. Divider

Creates a visual separator with optional text.

**Syntax:**
```lua
Window:AddDivider(parent, text)
```

**Parameters:**
- `parent` (Frame): Parent container
- `text` (string, optional): Divider text

**Example:**
```lua
Window:AddDivider(MainTab, "Combat Features")
Window:AddDivider(MainTab) -- Just a line
```

---

### 11. Search Bar

Creates a search bar for filtering tab content.

**Syntax:**
```lua
Window:AddSearchBar(parent)
```

**Parameters:**
- `parent` (Frame): Parent container (usually a tab)

**Returns:** SearchBox object

**Example:**
```lua
local SearchBar = Window:AddSearchBar(MainTab)
-- Automatically filters content as you type
```

---

## Theming System

### Available Themes

Prestige UI includes 15 pre-built themes:

1. **Dark** - Modern dark theme (default)
2. **Ocean** - Blue ocean-inspired theme
3. **Sunset** - Warm sunset colors
4. **Forest** - Green nature theme
5. **Midnight** - Deep purple theme
6. **Purple** - Elegant purple theme
7. **Cyberpunk** - Neon cyberpunk style
8. **Neon** - Bright neon green
9. **Minimal** - Clean minimal design
10. **Dracula** - Popular Dracula theme
11. **Nord** - Nordic color palette
12. **Monokai** - Classic Monokai theme
13. **Gruvbox** - Retro Gruvbox colors
14. **Tokyo** - Tokyo Night theme
15. **Rose** - Rose Pine theme

### Setting a Theme

**Syntax:**
```lua
Window:SetTheme(themeName)
```

**Example:**
```lua
Window:SetTheme("Ocean")
Window:SetTheme("Cyberpunk")
Window:SetTheme("Dracula")
```

---

### Creating Custom Themes

**Syntax:**
```lua
Window:CreateCustomTheme(themeTable)
```

**Parameters:**
- `themeTable` (table): Table with color definitions

**Theme Structure:**
```lua
{
    Primary = Color3.fromRGB(r, g, b),      -- Main accent color
    Secondary = Color3.fromRGB(r, g, b),    -- Secondary background
    Tertiary = Color3.fromRGB(r, g, b),     -- Tertiary elements
    Text = Color3.fromRGB(r, g, b),         -- Primary text color
    TextSecondary = Color3.fromRGB(r, g, b),-- Secondary text color
    Dark = Color3.fromRGB(r, g, b),         -- Darkest background
    Accent = Color3.fromRGB(r, g, b)        -- Accent highlights
}
```

**Example:**
```lua
Window:CreateCustomTheme({
    Primary = Color3.fromRGB(255, 100, 150),
    Secondary = Color3.fromRGB(30, 30, 35),
    Tertiary = Color3.fromRGB(40, 40, 45),
    Text = Color3.fromRGB(255, 255, 255),
    TextSecondary = Color3.fromRGB(180, 180, 190),
    Dark = Color3.fromRGB(20, 20, 25),
    Accent = Color3.fromRGB(255, 200, 100)
})
```

---

## Advanced Features

### Notifications

Display temporary notification messages.

**Syntax:**
```lua
Window:Notify(options)
```

**Options:**
- `Title` (string): Notification title
- `Message` (string): Notification message
- `Duration` (number): Display duration in seconds (default: 3)
- `Type` (string): "Info", "Success", "Warning", or "Error"

**Example:**
```lua
-- Info notification
Window:Notify({
    Title = "Information",
    Message = "This is an info message",
    Duration = 3,
    Type = "Info"
})

-- Success notification
Window:Notify({
    Title = "Success",
    Message = "Operation completed successfully!",
    Duration = 5,
    Type = "Success"
})

-- Warning notification
Window:Notify({
    Title = "Warning",
    Message = "Please be careful!",
    Duration = 4,
    Type = "Warning"
})

-- Error notification
Window:Notify({
    Title = "Error",
    Message = "Something went wrong!",
    Duration = 5,
    Type = "Error"
})
```

---

### Dialog Boxes

Display modal dialog boxes with custom buttons.

**Syntax:**
```lua
Window:ShowDialog(options)
```

**Options:**
- `Title` (string): Dialog title
- `Message` (string): Dialog message
- `Buttons` (table): Array of button definitions `{{"Text", callback}, ...}`

**Example:**
```lua
Window:ShowDialog({
    Title = "Confirm Action",
    Message = "Are you sure you want to proceed?",
    Buttons = {
        {"Yes", function()
            print("User confirmed")
            -- Execute action
        end},
        {"No", function()
            print("User cancelled")
        end}
    }
})
```

---

### Tooltips

Add hover tooltips to any element.

**Syntax:**
```lua
Window:AddTooltip(element, text)
```

**Parameters:**
- `element` (GuiObject): UI element to add tooltip to
- `text` (string): Tooltip text

**Example:**
```lua
local MyButton = Window:AddButton(MainTab, "Hover Me", function() end)
Window:AddTooltip(MyButton, "This button does something cool!")
```

---

### Minimize to Corner

Minimize the UI to a small draggable icon.

**Syntax:**
```lua
Window:MinimizeToCorner()
Window:RestoreFromCorner()
```

**Example:**
```lua
-- Minimize
Window:MinimizeToCorner()

-- Restore
Window:RestoreFromCorner()

-- Toggle keybind (default: RightShift)
-- Press RightShift to toggle between minimized and restored
```

---

### Custom Toggle Keybind

Change the default toggle keybind.

**Example:**
```lua
-- Set custom keybind
Window.ToggleKeybind = Enum.KeyCode.Insert

-- Now pressing Insert will toggle the UI
```

---

## Examples

### Example 1: Simple Script Hub

```lua
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL"))()
local Window = PrestigeUI:Create("Simple Hub")

-- Main Tab
local MainTab = Window:AddTab("Main")

Window:AddLabel(MainTab, "Welcome!", 18)
Window:AddButton(MainTab, "Infinite Jump", function()
    local Player = game.Players.LocalPlayer
    local InfiniteJump = true
    
    game:GetService("UserInputService").JumpRequest:Connect(function()
        if InfiniteJump then
            Player.Character:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping")
        end
    end)
    
    Window:Notify({
        Title = "Success",
        Message = "Infinite Jump enabled!",
        Type = "Success"
    })
end)

Window:AddButton(MainTab, "Speed Boost", function()
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 100
    Window:Notify({
        Title = "Success",
        Message = "Speed set to 100!",
        Type = "Success"
    })
end)
```

---

### Example 2: Advanced Configuration

```lua
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL"))()
local Window = PrestigeUI:Create("Advanced Hub")

-- Set theme
Window:SetTheme("Cyberpunk")

-- Settings Tab
local SettingsTab = Window:AddTab("Settings")

-- Add search bar
Window:AddSearchBar(SettingsTab)

-- Divider
Window:AddDivider(SettingsTab, "Player Settings")

-- Speed slider
Window:AddSlider(SettingsTab, 16, 200, 16, function(value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)

-- Jump power slider
Window:AddSlider(SettingsTab, 50, 200, 50, function(value)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
end)

-- Divider
Window:AddDivider(SettingsTab, "Visual Settings")

-- ESP toggle
Window:AddToggle(SettingsTab, "Enable ESP", function(state)
    -- ESP code here
    print("ESP:", state)
end)

-- ESP color picker
Window:AddColorPicker(SettingsTab, "ESP Color", 
    Color3.fromRGB(255, 0, 255), 
    function(color)
        print("ESP Color:", color)
    end
)

-- Divider
Window:AddDivider(SettingsTab, "Keybinds")

-- Toggle keybind
Window:AddKeybind(SettingsTab, "Toggle UI", Enum.KeyCode.RightShift, function(key)
    Window.ToggleKeybind = key
end)
```

---

### Example 3: Multi-Tab Hub

```lua
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL"))()
local Window = PrestigeUI:Create("Multi-Tab Hub")

-- Home Tab
local HomeTab = Window:AddTab("Home")
Window:AddLabel(HomeTab, "Welcome to the Hub!", 20)
Window:AddParagraph(HomeTab, "About", 
    "This is a feature-rich script hub with multiple tabs and options.")

-- Combat Tab
local CombatTab = Window:AddTab("Combat")
Window:AddButton(CombatTab, "Kill Aura", function()
    print("Kill Aura activated")
end)
Window:AddSlider(CombatTab, 1, 20, 5, function(value)
    print("Kill Aura Range:", value)
end)

-- Movement Tab
local MovementTab = Window:AddTab("Movement")
Window:AddToggle(MovementTab, "Fly", function(state)
    print("Fly:", state)
end)
Window:AddToggle(MovementTab, "No Clip", function(state)
    print("No Clip:", state)
end)

-- Visual Tab
local VisualTab = Window:AddTab("Visual")
Window:AddToggle(VisualTab, "ESP", function(state)
    print("ESP:", state)
end)
Window:AddToggle(VisualTab, "Fullbright", function(state)
    print("Fullbright:", state)
end)

-- Settings Tab
local SettingsTab = Window:AddTab("Settings")
Window:AddDropdown(SettingsTab, "Select Theme", 
    {"Dark", "Ocean", "Sunset", "Cyberpunk", "Dracula"}, 
    function(theme)
        Window:SetTheme(theme)
    end
)
```

---

## API Reference

### Window Methods

| Method | Description | Returns |
|--------|-------------|---------|
| `Create(title)` | Create new window | Window object |
| `AddTab(name)` | Add new tab | Content frame |
| `AddButton(parent, text, callback)` | Add button | Container |
| `AddLabel(parent, text, size)` | Add label | Label object |
| `AddParagraph(parent, title, content)` | Add paragraph | Container |
| `AddToggle(parent, text, callback)` | Add toggle | Toggle object |
| `AddSlider(parent, min, max, default, callback)` | Add slider | Slider object |
| `AddTextBox(parent, placeholder, callback)` | Add text box | TextBox object |
| `AddDropdown(parent, placeholder, options, callback)` | Add dropdown | Container |
| `AddKeybind(parent, text, default, callback)` | Add keybind | Keybind object |
| `AddColorPicker(parent, text, default, callback)` | Add color picker | ColorPicker object |
| `AddDivider(parent, text)` | Add divider | Container |
| `AddSearchBar(parent)` | Add search bar | SearchBox object |
| `Notify(options)` | Show notification | None |
| `ShowDialog(options)` | Show dialog | None |
| `AddTooltip(element, text)` | Add tooltip | None |
| `SetTheme(name)` | Set theme | None |
| `CreateCustomTheme(table)` | Create custom theme | None |
| `MinimizeToCorner()` | Minimize UI | None |
| `RestoreFromCorner()` | Restore UI | None |
| `Close()` | Close UI | None |

---

### Window Properties

| Property | Type | Description |
|----------|------|-------------|
| `Theme` | Table | Current theme colors |
| `ToggleKeybind` | Enum.KeyCode | Keybind to toggle UI |
| `Tabs` | Table | Array of tab objects |
| `ActiveTab` | String | Name of active tab |
| `MainFrame` | Frame | Main UI frame |
| `ScreenGui` | ScreenGui | Root ScreenGui object |

---

## Tips & Best Practices

### 1. Organization
- Group related features in the same tab
- Use dividers to separate sections
- Add search bars to tabs with many elements

### 2. User Experience
- Provide clear labels and descriptions
- Use appropriate notification types
- Add tooltips for complex features
- Choose readable themes

### 3. Performance
- Don't create too many UI elements at once
- Clean up connections when closing
- Use callbacks efficiently

### 4. Theming
- Test your UI with different themes
- Use custom themes for branding
- Ensure text is readable on all backgrounds

### 5. Error Handling
- Wrap callbacks in pcall for safety
- Validate user input from text boxes
- Provide feedback for actions

---

## Troubleshooting

### UI Not Showing
```lua
-- Make sure the script is running in a LocalScript
-- Check if the ScreenGui is parented correctly
print(Window.ScreenGui.Parent) -- Should be PlayerGui
```

### Theme Not Applying
```lua
-- Ensure theme name is correct (case-sensitive)
Window:SetTheme("Dark") -- Correct
Window:SetTheme("dark") -- Wrong
```

### Callbacks Not Working
```lua
-- Make sure callback is a function
Window:AddButton(MainTab, "Test", function()
    print("This works!")
end)

-- Not this:
Window:AddButton(MainTab, "Test", print("This doesn't work"))
```

### Elements Not Visible
```lua
-- Check if parent is correct
local Tab = Window:AddTab("Main")
Window:AddButton(Tab, "Button", function() end) -- Correct parent
```

---

## Credits

**Prestige UI Library**
- Modern UI library for Roblox
- Smooth animations and transitions
- Extensive customization options
- Regular updates and improvements

---

## Version History

**v1.0** - Initial Release
- Core UI framework
- 15 pre-built themes
- All basic components
- Notification system
- Search functionality
- Minimize/restore features

---

## Support

For issues, suggestions, or contributions:
- Test thoroughly before reporting bugs
- Provide clear reproduction steps
- Include error messages if any
- Suggest improvements with examples

---

**End of Documentation**

*Last Updated: 2024*
