# PrestigeUI - A Sleek & Modern Roblox UI Library

PrestigeUI is a powerful, dark-themed UI library designed for Roblox exploits and scripts. It features a modern, clean design, smooth animations, and a straightforward API for creating complex, multi-tab interfaces quickly.

## ✨ Features

- **Dark & Modern Theme**: Aesthetic design using dark tones and a vibrant primary color
- **Easy Setup**: Single loadstring for instant access
- **Tabbed Interface**: Organize your features with easy-to-use tabs
- **Comprehensive Controls**: Includes Buttons, Toggles, TextBoxes, Sliders, and Dropdowns
- **Full Responsiveness**: Supports dragging, minimizing, and a default Right Shift toggle key

## 🚀 Setup & Initialization

To start using PrestigeUI, simply load the library via the raw GitHub link and call the `:Create()` method.

### 1. Load the Library

Use the provided loadstring to fetch and execute the library code.

```lua
-- Load the Prestige UI Library
local PrestigeUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/sbertinato7-boop/PrestigeUILib/refs/heads/main/main"))()
```
### 2. Create the UI

The `:Create()` function initializes the main window.

| Method | Arguments | Returns | Description |
|--------|-----------|---------|-------------|
| `:Create(title)` | `string` title (optional) | `table` myUI | Creates and displays the main UI frame with a loading animation. |

**Example:**
```lua
local myUI = PrestigeUI:Create("Prestige Hub")
-- The UI is now created and visible
```

## 🧭 API Reference: Structure

### Adding Tabs

Tabs are the primary way to organize content within the UI. They are added to the main UI instance and return a reference to the content frame (which you pass to control methods).

| Method | Arguments | Returns | Description |
|--------|-----------|---------|-------------|
| `:AddTab(name)` | `string` name | `ScrollingFrame` | Adds a new tab to the sidebar. Returns the container where controls should be added. |

**Example:**
```lua
local mainTab = myUI:AddTab("Main Features")
local settingsTab = myUI:AddTab("User Settings")
-- You would use 'mainTab' or 'settingsTab' as the first argument in all control functions.
```

## 🧩 API Reference: Controls

All control functions require the tab's content container (the value returned from :AddTab()) as their first argument, followed by specific control parameters.

### 1. Buttons

Buttons execute a function immediately upon being clicked.

| Method | Arguments | Description |
|--------|-----------|-------------|
| `:AddButton(parent, text, callback)` | `Frame parent, string text, function callback()` | Creates a button. The callback function is executed when the button is clicked. |

**Example:**
```lua
myUI:AddButton(mainTab, "Execute Script", function()
    print("Script executed!")
end)
```
### 2. Toggles

Toggles (on/off switches) execute a function whenever their state changes, passing the new state as a boolean argument.

| Method | Arguments | Description |
|--------|-----------|-------------|
| `:AddToggle(parent, text, callback)` | `Frame parent, string text, function callback(state)` | Creates a toggle switch. callback is called with the current state (true or false). |

**Example:**
```lua
myUI:AddToggle(settingsTab, "Infinite Jump", function(is_enabled)
    if is_enabled then
        print("Infinite Jump: ON")
        -- Logic to enable feature
    else
        print("Infinite Jump: OFF")
        -- Logic to disable feature
    end
end)
```

### 3. Text Boxes

Text boxes allow the user to input text and execute a function when the input is finalized (by pressing Enter or losing focus).

| Method | Arguments | Description |
|--------|-----------|-------------|
| `:AddTextBox(parent, placeholder, callback)` | `Frame parent, string placeholder, function callback(text)` | Creates a text input field. callback is called with the text entered by the user. |

**Example:**
```lua
myUI:AddTextBox(settingsTab, "Enter your username...", function(input_text)
    print("User entered:", input_text)
end)
```

### 4. Sliders

Sliders provide a numerical control within a defined range.

| Method | Arguments | Description |
|--------|-----------|-------------|
| `:AddSlider(parent, min, max, default, callback)` | `Frame parent, number min, number max, number default, function callback(value)` | Creates a slider. callback fires when the value is changed, passing the current value (integer). |

**Example:**
```lua
-- Slider from 1 to 100, starting at 50
myUI:AddSlider(settingsTab, 1, 100, 50, function(speed_value)
    print("WalkSpeed set to:", speed_value)
end)
```

### 5. Dropdowns

Dropdowns allow the user to select one option from a list.

| Method | Arguments | Description |
|--------|-----------|-------------|
| `:AddDropdown(parent, placeholder, options, callback)` | `Frame parent, string placeholder, table options, function callback(option)` | Creates a dropdown. options is an array of strings. callback is called with the selected option. |

**Example:**
```lua
myUI:AddDropdown(settingsTab, "Select a Weapon", {"Sword", "Axe", "Wand"}, function(selected_item)
    print("Item selected:", selected_item)
end)
```

### 6. Paragraphs + Labels

Use these elements for static text, descriptions, and informational content.
| Method | Arguments | Description |
|--------|-----------|-------------|
| `:AddParagraph(parent, title, content)` | `Frame parent, string title, string content` | Creates a framed block of text with a bold title and smaller content text. Ideal for displaying information. |
| `:AddLabel(parent, text, textSize)` | `Frame parent, string text, number textSize (optional)` | Creates a simple text label. textSize defaults to 16. |

**Example:**
```lua
myUI:AddParagraph(infoTab, "Welcome!", "This library was designed for maximum efficiency and a clean look.")
myUI:AddLabel(mainTab, "Script Status: Idle", 14)
```

## 📜 Full Example Script

This script demonstrates how to set up the UI and use all the core controls.

```lua
-- ========================================
-- PRESTIGE UI EXAMPLE SCRIPT
-- ========================================

-- Load the Prestige UI Library
local PrestigeUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/sbertinato7-boop/PrestigeUILib/refs/heads/main/main"))()

-- Create a new UI
local myUI = PrestigeUI:Create("Prestige Hub")

-- Add the tabs for organization
local mainTab = myUI:AddTab("Main Functions")
local settingsTab = myUI:AddTab("Configuration")
local infoTab = myUI:AddTab("About")

-- ====================
-- MAIN TAB CONTROLS
-- ====================
myUI:AddLabel(mainTab, "Welcome to Prestige Hub!", 18)

myUI:AddButton(mainTab, "Say Hello", function()
    print("Hello, Prestige UI!")
end)

myUI:AddButton(mainTab, "Print Time", function()
    print("Time:", os.time())
end)

-- ====================
-- SETTINGS TAB CONTROLS
-- ====================
-- Toggle
myUI:AddToggle(settingsTab, "Enable Debug Mode", function(state)
    print("Debug Mode enabled:", state)
end)

-- Text Box
myUI:AddTextBox(settingsTab, "Enter your favorite number...", function(text)
    print("Favorite number entered:", text)
end)

-- Dropdown
myUI:AddDropdown(settingsTab, "Choose Server Region", {"US-East", "Europe", "Asia"}, function(region)
    print("Selected Region:", region)
end)

-- Slider
myUI:AddSlider(settingsTab, 0, 100, 50, function(value)
    print("Volume Level:", value)
end)

-- ====================
-- INFO TAB CONTROLS
-- ====================
myUI:AddParagraph(infoTab, "Library Information", "This is an example UI demonstrating the full capabilities of the PrestigeUI library. All controls are responsive and fully functional.")

myUI:AddLabel(infoTab, "Version: 1.0.0", 14)

-- NOTE: The UI can be toggled by pressing **Right Shift**.
```
