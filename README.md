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

Prestige UI is a modern, feature-rich UI library for Roblox that provides a sleek and customizable interface system.

### Features
- 🎨 **14 Pre-built Themes** (Dark, Ocean, Sunset, Forest, Midnight, Purple, Cyberpunk, Neon, Dracula, Nord, Monokai, Gruvbox, Tokyo, Rose)
- 🧩 **Comprehensive Component Library** (Buttons, Toggles, Sliders, Dropdowns, Text Boxes, etc.)
- 🔔 **Built-in Notification System**
- 🎭 **Smooth Animations** using TweenService
- 🔍 **Search Functionality**
- 🎯 **Draggable Windows**
- ⌨️ **Keybind Support**
- 📱 **Mobile Support** with automatic responsive scaling
- 🪟 **Minimizable Interface** with corner icon

---

## Installation

### Method 1: Direct Load
```lua
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL_HERE"))()
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
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL_HERE"))()

-- Create a new UI window
local Window = PrestigeUI:Create("Prestige Hub")

-- Create a tab
local MainTab = Window:AddTab("Main")

-- Add a button
Window:AddButton(MainTab, "Click Me!", function()
    print("Button clicked!")
end)
```

### Complete Example
```lua
local PrestigeUI = loadstring(game:HttpGet("YOUR_URL_HERE"))()

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

### `PrestigeUI:Create(title)`
Creates a new UI window with loading animation.

**Parameters:**
- `title` (string, optional): Window title (default: "Prestige Hub")

**Returns:** Window object

**Example:**
```lua
local Window = PrestigeUI:Create("My Hub")
```

**Features:**
- Automatic mobile detection and responsive sizing
- Loading bar animation (0-100%)
- Draggable top bar
- Minimize and close buttons
- Smooth fade-in animation

---

### `Window:AddTab(tabName)`
Creates a new tab in the sidebar.

**Parameters:**
- `tabName` (string): Name of the tab

**Returns:** Content frame (ScrollingFrame) for the tab

**Example:**
```lua
local MainTab = Window:AddTab("Main")
local SettingsTab = Window:AddTab("Settings")
local AboutTab = Window:AddTab("About")
```

**Features:**
- Automatic tab switching
- Hover effects
- First tab is automatically active
- Mobile and PC touch/click support

---

### `Window:Close()`
Closes and destroys the UI window with smooth animation.

**Example:**
```lua
Window:Close()
```

**Features:**
- Smooth fade-out animation
- Disconnects all events
- Cleans up all UI elements
- Clears global reference

---

## UI Components

### 1. Button
Creates a clickable button with hover and press effects.

**Syntax:**
```lua
Window:AddButton(parent, text, callback)
```

**Parameters:**
- `parent` (Frame): Parent container (usually a tab)
- `text` (string): Button text
- `callback` (function): Function to execute on click

**Returns:** Container frame

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

**Features:**
- Hover color change
- Scale animation on hover (PC only)
- Press animation
- Touch and mouse support
- Automatic theme updates

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
- `textSize` (number, optional): Font size (default: 16 on PC, 12 on mobile)

**Returns:** TextLabel object

**Example:**
```lua
Window:AddLabel(MainTab, "Welcome to Prestige UI!", 20)
Window:AddLabel(MainTab, "Version 2.0", 14)
```

---

### 3. Paragraph
Creates a formatted text block with title and content.

**Syntax:**
```lua
Window:AddParagraph(parent, title, content)
```

**Parameters:**
- `parent` (Frame): Parent container
- `title` (string): Paragraph title (displays in Primary color)
- `content` (string): Paragraph content (displays in TextSecondary color)

**Returns:** Container frame

**Example:**
```lua
Window:AddParagraph(MainTab, "About", 
    "This is a comprehensive UI library with many features and customization options.")
```

---

### 4. Toggle
Creates an animated toggle switch with on/off states.

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

**Features:**
- Smooth slide animation
- Color transition
- Scale effect on hover
- Touch and mouse support

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

**Features:**
- Real-time value updates
- Visual fill indicator
- Draggable button
- Hover effects
- Click-to-set functionality
- Mobile and PC support

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

**Features:**
- Focus animations
- Mobile tap-to-focus support
- Enter key submission
- Placeholder text

---

### 7. Dropdown
Creates an animated dropdown menu with multiple options.

**Syntax:**
```lua
Window:AddDropdown(parent, placeholder, options, callback)
```

**Parameters:**
- `parent` (Frame): Parent container
- `placeholder` (string): Default text
- `options` (table): Array of option strings
- `callback` (function): Function called with selected option

**Returns:** Table with `Container` and `Dropdown` frame

**Example:**
```lua
Window:AddDropdown(MainTab, "Select Weapon", 
    {"Sword", "Bow", "Staff", "Axe"}, 
    function(selected)
        print("Selected weapon:", selected)
    end
)
```

**Features:**
- Smooth expand/collapse animation
- Scrollable option list
- Automatic size adjustment
- Touch and mouse support
- Animation debouncing

---

### 8. Keybind
Creates a keybind selector that waits for key press.

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

**Features:**
- "..." indicator while listening
- Color change during selection
- Stores connection in Window.Connections

---

### 9. Color Picker
Creates a modal color selection tool with RGB sliders and live preview.

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

**Features:**
- RGB sliders (0-255)
- Live color preview
- Apply and Cancel buttons
- Modal overlay blocks other input
- Hover scale effect

---

### 10. Divider
Creates a visual separator with optional text label.

**Syntax:**
```lua
Window:AddDivider(parent, text)
```

**Parameters:**
- `parent` (Frame): Parent container
- `text` (string, optional): Divider text

**Returns:** Container frame

**Example:**
```lua
Window:AddDivider(MainTab, "Combat Features")
Window:AddDivider(MainTab) -- Just a line
```

---

### 11. Section
Creates a collapsible section container with title and organized layout.

**Syntax:**
```lua
Window:AddSection(parent, title)
```

**Parameters:**
- `parent` (Frame): Parent container
- `title` (string, optional): Section title

**Returns:** Section frame (use as parent for other elements)

**Example:**
```lua
local PlayerSection = Window:AddSection(MainTab, "Player Options")
Window:AddButton(PlayerSection, "Reset", function() end)
Window:AddSlider(PlayerSection, 16, 100, 16, function(val) end)
```

**Features:**
- Automatic sizing
- Internal padding
- Organized layout with UIListLayout

---

### 12. Search Bar
Creates a search bar that filters tab content in real-time.

**Syntax:**
```lua
Window:AddSearchBar(parent)
```

**Parameters:**
- `parent` (Frame): Parent container (usually a tab or Sidebar)

**Returns:** SearchBox (TextBox object)

**Example:**
```lua
local SearchBar = Window:AddSearchBar(MainTab)
-- Automatically filters tabs and content as you type
```

**Features:**
- Real-time filtering
- Searches tab names and all text content
- Shows/hides matching tabs
- Icon indicator
- Focus animations

---

## Theming System

### Available Themes
Prestige UI includes **14 pre-built themes**:

1. **Dark** - Modern dark theme (default)
2. **Ocean** - Blue ocean-inspired
3. **Sunset** - Warm sunset colors
4. **Forest** - Green nature theme
5. **Midnight** - Deep purple
6. **Purple** - Elegant purple
7. **Cyberpunk** - Neon magenta/cyan
8. **Neon** - Bright green
9. **Dracula** - Popular Dracula palette
10. **Nord** - Nordic colors
11. **Monokai** - Classic Monokai
12. **Gruvbox** - Retro Gruvbox
13. **Tokyo** - Tokyo Night
14. **Rose** - Rose Pine

### Setting a Theme
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
```lua
Window:CreateCustomTheme(themeTable)
```

**Theme Structure:**
```lua
{
    Primary = Color3.fromRGB(r, g, b),      -- Main accent color
    Secondary = Color3.fromRGB(r, g, b),    -- Secondary background
    Tertiary = Color3.fromRGB(r, g, b),     -- Element backgrounds
    Text = Color3.fromRGB(r, g, b),         -- Primary text
    TextSecondary = Color3.fromRGB(r, g, b),-- Secondary text
    Dark = Color3.fromRGB(r, g, b),         -- Main background
    Accent = Color3.fromRGB(r, g, b)        -- Highlight color
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
Display temporary notification messages with icons.

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
    Message = "Operation completed!",
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

**Features:**
- Color-coded accent bars
- Slide-in/slide-out animations
- Auto-dismiss with timer
- Manual close button
- Stack multiple notifications

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

**Features:**
- Modal overlay blocks all input
- Cooldown system prevents spam
- Smooth animations
- Multiple button support

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

**Features:**
- Follows mouse cursor
- Fade in/out animations
- High ZIndex for visibility

---

### Minimize to Corner
Minimize the UI to a small draggable icon in the corner.

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

-- Default keybind: RightShift toggles UI
```

**Features:**
- Draggable minimized icon
- Fade animations
- Double-click to restore
- Automatically creates/destroys icon

---

### Custom Toggle Keybind
Change the default toggle keybind (RightShift).

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

local MainTab = Window:AddTab("Main")

Window:AddLabel(MainTab, "Welcome!", 18)

Window:AddButton(MainTab, "Infinite Jump", function()
    local Player = game.Players.LocalPlayer
    game:GetService("UserInputService").JumpRequest:Connect(function()
        Player.Character:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping")
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

Window:SetTheme("Cyberpunk")

local SettingsTab = Window:AddTab("Settings")

Window:AddSearchBar(SettingsTab)

Window:AddDivider(SettingsTab, "Player Settings")

Window:AddSlider(SettingsTab, 16, 200, 16, function(value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)

Window:AddSlider(SettingsTab, 50, 200, 50, function(value)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = value
end)

Window:AddDivider(SettingsTab, "Visual Settings")

Window:AddToggle(SettingsTab, "Enable ESP", function(state)
    print("ESP:", state)
end)

Window:AddColorPicker(SettingsTab, "ESP Color", 
    Color3.fromRGB(255, 0, 255), 
    function(color)
        print("ESP Color:", color)
    end
)

Window:AddDivider(SettingsTab, "Keybinds")

Window:AddKeybind(SettingsTab, "Toggle UI", Enum.KeyCode.RightShift, function(key)
    Window.ToggleKeybind = key
end)
```

---

## API Reference

### Window Methods
| Method | Description | Returns |
|--------|-------------|---------|
| `Create(title)` | Create new window | Window object |
| `AddTab(name)` | Add new tab | ScrollingFrame |
| `AddButton(parent, text, callback)` | Add button | Container Frame |
| `AddLabel(parent, text, size)` | Add label | TextLabel |
| `AddParagraph(parent, title, content)` | Add paragraph | Container Frame |
| `AddToggle(parent, text, callback)` | Add toggle | Table {Container, Toggle, GetState()} |
| `AddSlider(parent, min, max, default, callback)` | Add slider | Table {Container, GetValue()} |
| `AddTextBox(parent, placeholder, callback)` | Add text box | TextBox |
| `AddDropdown(parent, placeholder, options, callback)` | Add dropdown | Table {Container, Dropdown} |
| `AddKeybind(parent, text, default, callback)` | Add keybind | Table {Container, GetKey()} |
| `AddColorPicker(parent, text, default, callback)` | Add color picker | Table {Container, GetColor()} |
| `AddDivider(parent, text)` | Add divider | Container Frame |
| `AddSection(parent, title)` | Add section | Section Frame |
| `AddSearchBar(parent)` | Add search bar | TextBox |
| `Notify(options)` | Show notification | None |
| `ShowDialog(options)` | Show dialog | None |
| `AddTooltip(element, text)` | Add tooltip | None |
| `SetTheme(name)` | Set theme | None |
| `CreateCustomTheme(table)` | Create custom theme | None |
| `ApplyTheme()` | Apply current theme | None |
| `MinimizeToCorner()` | Minimize UI | None |
| `RestoreFromCorner()` | Restore UI | None |
| `Close()` | Close UI | None |

### Window Properties
| Property | Type | Description |
|----------|------|-------------|
| `Theme` | Table | Current theme colors |
| `ToggleKeybind` | Enum.KeyCode | Keybind to toggle UI (default: RightShift) |
| `Tabs` | Table | Array of tab objects |
| `ActiveTab` | String | Name of active tab |
| `MainFrame` | Frame | Main UI frame |
| `ScreenGui` | ScreenGui | Root ScreenGui object |
| `IsMobileMode` | Boolean | Whether mobile mode is active |
| `Connections` | Table | All event connections |
| `ThemeElements` | Table | All registered theme elements |

---

## Tips & Best Practices

### 1. Organization
- Group related features in the same tab
- Use dividers and sections to separate features
- Add search bars to tabs with many elements
- Use consistent naming conventions

### 2. User Experience
- Provide clear labels and descriptions
- Use appropriate notification types
- Add tooltips for complex features
- Test on both mobile and PC

### 3. Performance
- Don't create too many UI elements at once
- Use sections to organize large tabs
- Clean up connections when closing
- Use callbacks efficiently

### 4. Theming
- Test your UI with different themes
- Use custom themes for branding
- Ensure text is readable on all backgrounds
- Use AddSection for better organization

### 5. Error Handling
- Wrap callbacks in pcall for safety
- Validate user input from text boxes
- Provide feedback for actions
- Check for nil values

---

## Troubleshooting

### UI Not Showing
```lua
-- Make sure the script is running in a LocalScript
print(Window.ScreenGui.Parent) -- Should be PlayerGui
```

### Theme Not Applying
```lua
-- Ensure theme name is correct (case-sensitive)
Window:SetTheme("Dark") -- ✅ Correct
Window:SetTheme("dark") -- ❌ Wrong
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

### Mobile Issues
- TextBox not focusing? Added automatic touch-to-focus
- Dropdown not opening? Uses touch and mouse support
- Tabs not switching? Tab buttons support both input types

---

## Credits

**Prestige UI Library**
- Modern UI library for Roblox
- Smooth animations and transitions
- Extensive customization options
- Mobile and PC support

---

## Version History

**v2.0 - Current Release**
- Complete theme system rewrite
- Mobile support and responsive design
- Section components
- Improved animations
- Dialog cooldown system
- Better touch support
- Enhanced notification system

---

*Last Updated: October 2025*
