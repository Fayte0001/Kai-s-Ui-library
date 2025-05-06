# KAI'S UI LIBRARY DOCUMENTATION

## Table of Contents
1. [Installation](#installation)
2. [Basic Usage](#basic-usage)
3. [Components](#components)
   - [Window](#window)
   - [Tabs](#tabs)
   - [Sections](#sections)
   - [Buttons](#buttons)
   - [Labels](#labels)
   - [Input Fields](#input-fields)
   - [Sliders](#sliders)
   - [Toggle Switches](#toggle-switches)
4. [Theme Customization](#theme-customization)
5. [Examples](#examples)

## Installation

1. Place the `UICornerStrokeLib` module script in ReplicatedStorage
2. Create a LocalScript in StarterPlayerScripts with the following code:

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local UICornerStrokeLib = require(ReplicatedStorage:WaitForChild("UICornerStrokeLib"))

-- Create your UI here
local window = UICornerStrokeLib.CreateWindow({
    Title = "My UI Window",
    Size = UDim2.new(0, 600, 0, 400)
})
```

## Basic Usage

The library follows a hierarchical structure:
1. Create a Window
2. Add Tabs to the Window
3. Add Sections to Tabs
4. Add Components to Sections

```lua
local window = UICornerStrokeLib.CreateWindow({
    Title = "App Name",
    Size = UDim2.new(0, 650, 0, 450)
})

local mainTab = window:AddTab("Main", "rbxassetid://3926305904")
local section = mainTab:AddSection({
    Title = "My Section",
    Size = UDim2.new(1, -24, 0, 200)
})

section:AddElement("Button", {
    Text = "Click Me",
    OnClick = function()
        print("Button clicked!")
    end
})
```

## Components

### Window

Creates the main application window.

```lua
local window = UICornerStrokeLib.CreateWindow({
    Title = "Window Title",  -- Window title text
    Size = UDim2.new(0, 600, 0, 400),  -- Window size
    DisplayOrder = 10  -- (Optional) GUI display order
})
```

### Tabs

Add tabs to organize your interface.

```lua
local tab = window:AddTab("Tab Name", "iconId")  -- Second parameter is optional icon
```

### Sections

Group components within tabs.

```lua
local section = tab:AddSection({
    Title = "Section Title",  -- Optional
    Size = UDim2.new(1, -24, 0, 150),  -- Width should account for padding
    NoLayout = false  -- Optional, disables automatic layout
})
```

### Buttons

Interactive button elements.

```lua
section:AddElement("Button", {
    Text = "Button Text",
    OnClick = function()
        -- Button click handler
    end
})
```

### Labels

Text display elements.

```lua
section:AddElement("Label", {
    Text = "Label Text",
    Height = 20,  -- Fixed height
    TextWrapped = true,  -- Optional
    RichText = true,  -- Optional
    Alignment = Enum.TextXAlignment.Left  -- Optional
})
```

### Input Fields

Text input components.

```lua
local input = section:AddElement("Input", {
    Placeholder = "Enter text...",
    OnFocusLost = function(text)
        print("User entered:", text)
    end,
    OnTextChanged = function(text)  -- Optional
        print("Text changing:", text)
    end
})
```

### Sliders

Range input controls.

```lua
local slider = section:AddElement("Slider", {
    Text = "Slider Label",
    Min = 0,
    Max = 100,
    Default = 50,
    Step = 1,  -- Optional
    OnChange = function(value)
        print("New value:", value)
    end
})
```

### Toggle Switches

On/off toggle controls.

```lua
local toggle = section:AddElement("Toggle", {
    Text = "Toggle Label",
    Default = false,  -- Initial state
    OnToggle = function(state)
        print("Toggle state:", state)
    end
})
```

## Theme Customization

The library comes with a comprehensive theme system.

### Get Current Theme
```lua
local currentTheme = UICornerStrokeLib.GetTheme()
```

### Modify Theme
```lua
UICornerStrokeLib.SetTheme({
    AccentColor = Color3.fromRGB(255, 100, 100),
    EnableAnimations = false,
    TextColor = Color3.new(1, 1, 1)
})
```

### Reset to Default Theme
```lua
UICornerStrokeLib.ResetTheme()
```

### Available Theme Properties

| Property | Type | Description |
|----------|------|-------------|
| BackgroundColor | Color3 | Main background color |
| PrimaryColor | Color3 | Primary UI color |
| SecondaryColor | Color3 | Secondary UI color |
| TextColor | Color3 | Text color |
| AccentColor | Color3 | Accent/highlight color |
| SuccessColor | Color3 | Color for success states |
| WarningColor | Color3 | Color for warning states |
| ErrorColor | Color3 | Color for error states |
| DisabledColor | Color3 | Color for disabled elements |
| CornerRadius | UDim | Corner rounding amount |
| StrokeThickness | number | Border thickness |
| HoverModifier | number | Color modification on hover |
| FontTitle | Enum.Font | Title font |
| FontButton | Enum.Font | Button font |
| FontContent | Enum.Font | Content font |
| TitleTextSize | number | Font size for titles |
| ButtonTextSize | number | Font size for buttons |
| ContentTextSize | number | Font size for general content |
| TransitionSpeed | number | Animation speed |
| EnableAnimations | boolean | Whether to enable animations |
| EnableShadows | boolean | Whether to render shadows |
| EnableAutoLayout | boolean | Whether to enable automatic layout |
| EnableResponsiveScaling | boolean | Whether to enable responsive sizing |

## Examples

### Complete UI Example

```lua
local window = UICornerStrokeLib.CreateWindow({
    Title = "Settings Panel",
    Size = UDim2.new(0, 650, 0, 450)
})

-- First Tab
local generalTab = window:AddTab("General", "rbxassetid://3926305904")

-- Section with toggle switches
local settingsSection = generalTab:AddSection({
    Title = "App Settings",
    Size = UDim2.new(1, -24, 0, 150)
})

settingsSection:AddElement("Toggle", {
    Text = "Enable Notifications",
    Default = true,
    OnToggle = function(state)
        print("Notifications:", state)
    end
})

-- Section with sliders
local volumeSection = generalTab:AddSection({
    Title = "Audio Settings",
    Size = UDim2.new(1, -24, 0, 120)
})

volumeSection:AddElement("Slider", {
    Text = "Master Volume",
    Min = 0,
    Max = 100,
    Default = 80,
    OnChange = function(value)
        print("Volume set to:", value)
    end
})

-- Second Tab
local accountTab = window:AddTab("Account", "rbxassetid://3926307971")

local profileSection = accountTab:AddSection({
    Size = UDim2.new(1, -24, 0, 200)
})

profileSection:AddElement("Label", {
    Text = "Account Information",
    Font = Enum.Font.GothamBold,
    TextSize = 16,
    Height = 30
})

local nameInput = profileSection:AddElement("Input", {
    Placeholder = "Enter your username",
    OnFocusLost = function(text)
        print("Username updated to:", text)
    end
})

profileSection:AddElement("Button", {
    Text = "Save Changes",
    OnClick = function()
        print("Saving account changes...")
    end
})
```

### Theme Customization Example

```lua
-- Change to dark red theme
UICornerStrokeLib.SetTheme({
    AccentColor = Color3.fromRGB(200, 50, 50),
    BackgroundColor = Color3.fromRGB(30, 30, 30),
    PrimaryColor = Color3.fromRGB(50, 50, 50),
    TextColor = Color3.new(0.9, 0.9, 0.9)
})

-- Disable animations
UICornerStrokeLib.SetTheme({
    EnableAnimations = false
})
```

### Advanced Styling Example

```lua
-- Create a custom styled section with gradient and shadow
local advancedSection = tab:AddSection({
    Title = "Advanced Section",
    Size = UDim2.new(1, -24, 0, 200),
    BackgroundColor3 = Color3.fromRGB(60, 60, 70),
    Shadow = true,
    Transparency = 0.1
})

-- Add custom styled button
local customButton = advancedSection:AddElement("Button", {
    Text = "Custom Button",
    OnClick = function() 
        print("Custom button clicked!")
    end
})

-- Style the button frame directly (advanced usage)
UICornerStrokeLib.ApplyStyle(customButton.Button, {
    BackgroundTransparency = 0.1,
    StrokeColor = Color3.fromRGB(100, 100, 200),
    StrokeThickness = 2,
    Gradient = true,
    GradientRotation = 45
})
```
