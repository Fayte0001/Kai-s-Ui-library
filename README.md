# KAI'S UI LIBRARY

A powerful, customizable UI framework for Roblox experiences that provides professional-grade interface components with modern design aesthetics and seamless integration.

![KAI'S UI LIBRARY](https://images.pexels.com/photos/5483077/pexels-photo-5483077.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1)

## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Core Features](#core-features)
- [Theme Configuration](#theme-configuration)
- [Components](#components)
  - [Window](#window)
  - [Tabs](#tabs)
  - [Sections](#sections)
  - [Button](#button)
  - [Toggle](#toggle)
  - [Slider](#slider)
  - [Input](#input)
  - [Label](#label)
- [Theme Editor](#theme-editor)
- [Advanced Usage](#advanced-usage)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [License](#license)

## Introduction

KAI'S UI LIBRARY is a comprehensive Roblox UI framework designed to streamline the creation of beautiful, responsive user interfaces. With an emphasis on modern design principles, smooth animations, and developer flexibility, this library enables you to create professional interfaces with minimal effort.

## Installation

1. Ensure you have a `DraggableObject` module in your ReplicatedStorage
2. Add the UI library module to your project:

```lua
-- Server script setup
local UILibModule = script:WaitForChild("UICornerStrokeLib")
UILibModule.Parent = game:GetService("ReplicatedStorage")
```

3. Require the module in your client scripts:

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local UICornerStrokeLib = require(ReplicatedStorage:WaitForChild("UICornerStrokeLib"))
```

## Quick Start

Create a simple window with a button:

```lua
-- Create a window
local window = UICornerStrokeLib.CreateWindow({
    Title = "My First Window",
    Size = UDim2.new(0, 600, 0, 400)
})

-- Add a tab
local tab = window:AddTab("Home", "rbxassetid://7059346434")

-- Add a button to the default section
tab:AddElement("Button", {
    Text = "Click Me!",
    OnClick = function()
        print("Button clicked!")
    end
})
```

## Core Features

- **Modern Aesthetics**: Clean, professional UI components with consistent styling
- **Theme Customization**: Comprehensive theming system with color schemes and visual options
- **Responsive Design**: Automatic layout capabilities with responsive sizing
- **Component Library**: Extensive collection of UI components (buttons, toggles, sliders, etc.)
- **Tab-Based Organization**: Structured UI with tabs, sections, and elements
- **Interactive Elements**: Smooth animations and transitions for all interactions
- **Drag-and-Drop Windows**: Intuitive window movement and positioning
- **Live Theme Editor**: Built-in theme customization tool

## Theme Configuration

The library comes with a default theme, but you can customize it to match your experience:

```lua
UICornerStrokeLib.SetTheme({
    -- Primary colors
    BackgroundColor = Color3.fromRGB(30, 30, 30),
    PrimaryColor = Color3.fromRGB(50, 50, 50),
    AccentColor = Color3.fromRGB(85, 170, 255),
    
    -- Visual settings
    CornerRadius = UDim.new(0, 6),
    StrokeThickness = 1,
    
    -- Enable features
    EnableAnimations = true,
    EnableShadows = true
})
```

### Available Theme Properties

| Category | Properties |
|----------|------------|
| Colors | BackgroundColor, PrimaryColor, SecondaryColor, TextColor, AccentColor, SuccessColor, WarningColor, ErrorColor, DisabledColor |
| Visual Effects | HoverModifier, CornerRadius, StrokeThickness |
| Typography | FontTitle, FontButton, FontContent, TitleTextSize, ButtonTextSize, ContentTextSize |
| Animation | TransitionSpeed, AnimationEasing, AnimationDirection, EnableAnimations |
| Shadows | ShadowColor, ShadowTransparency, EnableShadows |
| Layout | Spacing, ZIndex, EnableAutoLayout, EnableResponsiveScaling |

## Components

### Window

The Window is the main container for your UI. It provides a draggable frame with a title bar and content area.

```lua
local window = UICornerStrokeLib.CreateWindow({
    Title = "My Window",
    Size = UDim2.new(0, 650, 0, 450),
    IncludeThemeEditor = true -- Optional theme editor
})
```

### Tabs

Tabs organize content into separate pages within a window.

```lua
local homeTab = window:AddTab("Home", "rbxassetid://7059346434")
local settingsTab = window:AddTab("Settings", "rbxassetid://7059346435")
```

### Sections

Sections group related elements within a tab.

```lua
local generalSection = homeTab:AddSection({
    Title = "General Settings",
    Size = UDim2.new(1, -24, 0, 0) -- Height will auto-adjust
})

-- Adding elements to a section
generalSection:AddElement("Button", {
    Text = "Save Settings"
})
```

### Button

Buttons provide clickable actions with hover effects and animations.

```lua
local saveButton = tab:AddElement("Button", {
    Text = "Save Changes",
    LayoutOrder = 1,
    OnClick = function()
        -- Your action here
        print("Button clicked!")
    end
})

-- Update button text
saveButton:SetText("Changes Saved")

-- Disable button
saveButton:SetDisabled(true)
```

### Toggle

Toggles provide an on/off switch with animated state transitions.

```lua
local darkModeToggle = tab:AddElement("Toggle", {
    Text = "Dark Mode",
    Default = true, -- Start enabled
    LayoutOrder = 2,
    OnToggle = function(state)
        print("Dark mode:", state)
    end
})

-- Get toggle state
local isEnabled = darkModeToggle:GetState()

-- Set toggle state
darkModeToggle:SetState(false)
```

### Slider

Sliders allow users to select a value within a range.

```lua
local volumeSlider = tab:AddElement("Slider", {
    Text = "Volume",
    Min = 0,
    Max = 100,
    Step = 1,
    Default = 50,
    LayoutOrder = 3,
    OnChange = function(value)
        print("Volume set to:", value)
    end
})

-- Get slider value
local currentVolume = volumeSlider:GetValue()

-- Set slider value
volumeSlider:SetValue(75)
```

### Input

Text input fields for user text entry.

```lua
local nameInput = tab:AddElement("Input", {
    Placeholder = "Enter your name",
    Text = "Player", -- Default text
    LayoutOrder = 4,
    OnFocusLost = function(text)
        print("Name set to:", text)
    end,
    OnTextChanged = function(text)
        print("Typing:", text)
    end
})

-- Get input text
local name = nameInput:GetText()

-- Set input text
nameInput:SetText("New Player")
```

### Label

Text labels for displaying information.

```lua
local infoLabel = tab:AddElement("Label", {
    Text = "Welcome to my game!",
    Height = 30, -- Optional custom height
    TextWrapped = true,
    RichText = true, -- Enable rich text formatting
    LayoutOrder = 5,
    Alignment = Enum.TextXAlignment.Center
})

-- Update label text
infoLabel:SetText("Thanks for playing!")

-- Change label color
infoLabel:SetColor(Color3.fromRGB(255, 255, 255))
```

## Theme Editor

The library includes a built-in theme editor that allows real-time customization:

```lua
local window = UICornerStrokeLib.CreateWindow({
    Title = "My App",
    IncludeThemeEditor = true -- This adds a Theme Editor tab
})
```

The theme editor provides:
- Color customization for all theme colors
- Numeric setting adjustments (corner radius, stroke thickness)
- Reset to default theme option

## Advanced Usage

### Creating Custom Layouts

```lua
-- Create a window with custom sections
local window = UICornerStrokeLib.CreateWindow({
    Title = "Dashboard"
})

local mainTab = window:AddTab("Dashboard")

-- Top stats section
local statsSection = mainTab:AddSection({
    Title = "Statistics",
    Size = UDim2.new(1, -24, 0, 100)
})

-- Add some stat labels
statsSection:AddElement("Label", {
    Text = "Players: 42",
    LayoutOrder = 1
})

statsSection:AddElement("Label", {
    Text = "Average Score: 1,250",
    LayoutOrder = 2
})

-- Controls section
local controlsSection = mainTab:AddSection({
    Title = "Controls",
    Size = UDim2.new(1, -24, 0, 0) -- Auto height
})

controlsSection:AddElement("Button", {
    Text = "Reset Statistics",
    LayoutOrder = 1
})
```

### Theme Listeners

Register callbacks for theme changes:

```lua
local function onThemeChanged(newTheme)
    print("Theme was updated!")
    -- Update custom UI elements
end

local listenerId = UICornerStrokeLib.RegisterThemeListener(onThemeChanged)

-- Later, unregister if needed
UICornerStrokeLib.UnregisterThemeListener(listenerId)
```

## API Reference

### Core Functions

| Function | Description |
|----------|-------------|
| `UICornerStrokeLib.CreateWindow(settings)` | Creates a new window UI |
| `UICornerStrokeLib.CreateSection(parent, settings)` | Creates a section container |
| `UICornerStrokeLib.CreateButton(parent, settings)` | Creates a button |
| `UICornerStrokeLib.CreateToggle(parent, settings)` | Creates a toggle switch |
| `UICornerStrokeLib.CreateSlider(parent, settings)` | Creates a slider |
| `UICornerStrokeLib.CreateInput(parent, settings)` | Creates a text input field |
| `UICornerStrokeLib.CreateLabel(parent, settings)` | Creates a text label |
| `UICornerStrokeLib.SetTheme(newTheme)` | Updates the current theme |
| `UICornerStrokeLib.GetTheme()` | Returns the current theme |
| `UICornerStrokeLib.ResetTheme()` | Resets to default theme |
| `UICornerStrokeLib.RegisterThemeListener(callback)` | Registers a theme change listener |
| `UICornerStrokeLib.UnregisterThemeListener(id)` | Unregisters a theme listener |
| `UICornerStrokeLib.CreateTween(target, properties, duration)` | Creates an animation tween |

### Window Methods

| Method | Description |
|--------|-------------|
| `window:AddTab(tabName, tabIcon)` | Adds a tab to the window |
| `window:Resize(newSize)` | Resizes the window |

### Tab Methods

| Method | Description |
|--------|-------------|
| `tab:AddSection(settings)` | Adds a section to the tab |
| `tab:AddElement(elementType, elementSettings)` | Adds an element to the default section |

### Section Methods

| Method | Description |
|--------|-------------|
| `section:AddElement(elementType, elementSettings)` | Adds an element to the section |

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This library is licensed under the MIT License - see the LICENSE file for details.

---

© 2025 KAI'S UI LIBRARY. All rights reserved.
