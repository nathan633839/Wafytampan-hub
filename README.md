# Wafytampan-hub
Script
local Player = game.Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local Humanoid = Character:WaitForChild("Humanoid")

-- Pengaturan default
local settings = {
    walkSpeed = 16,
    gravity = 196.2,
    jumpPower = 50,
    language = "English"
}

-- Terjemahan multi bahasa
local translations = {
    English = {
        title = "wafytampan hub",
        walkSpeed = "Walk Speed",
        gravity = "Gravity",
        jumpPower = "Jump Power",
        close = "X",
        minimize = "-",
        language = "Language:"
    },
    Indonesia = {
        title = "wafytampan hub",
        walkSpeed = "Kecepatan Jalan",
        gravity = "Gravitasi",
        jumpPower = "Kekuatan Lompat",
        close = "X",
        minimize = "-",
        language = "Bahasa:"
    },
    Spanish = {
        title = "wafytampan hub",
        walkSpeed = "Velocidad de Caminar",
        gravity = "Gravedad",
        jumpPower = "Poder de Salto",
        close = "X",
        minimize = "-",
        language = "Idioma:"
    }
}

-- Membuat GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "CharacterControls"
ScreenGui.Parent = Player.PlayerGui

local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 300, 0, 250)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -125)
MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

-- Judul dengan efek warna unik
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Size = UDim2.new(0, 200, 0, 30)
Title.Position = UDim2.new(0, 10, 0, 10)
Title.BackgroundTransparency = 1
Title.Text = "wafytampan hub"
Title.TextColor3 = Color3.fromHSV(tick()%5/5, 0.8, 1) -- Warna berubah
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = MainFrame

-- Animasi warna judul
spawn(function()
    while Title and Title.Parent do
        Title.TextColor3 = Color3.fromHSV(tick()%5/5, 0.8, 1)
        wait(0.1)
    end
end)

-- Tombol close
local CloseButton = Instance.new("TextButton")
CloseButton.Name = "CloseButton"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -40, 0, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 60, 60)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Text = "X"
CloseButton.Font = Enum.Font.GothamBold
CloseButton.TextSize = 18
CloseButton.Parent = MainFrame

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Tombol minimize
local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Name = "MinimizeButton"
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -80, 0, 0)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(80, 80, 100)
MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeButton.Text = "-"
MinimizeButton.Font = Enum.Font.GothamBold
MinimizeButton.TextSize = 18
MinimizeButton.Parent = MainFrame

local isMinimized = false
local originalSize = MainFrame.Size
MinimizeButton.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    if isMinimized then
        MainFrame.Size = UDim2.new(0, 300, 0, 40)
    else
        MainFrame.Size = originalSize
    end
end)

-- Slider untuk Walk Speed
local WalkSpeedSlider = Instance.new("Frame")
WalkSpeedSlider.Name = "WalkSpeedSlider"
WalkSpeedSlider.Size = UDim2.new(0, 280, 0, 50)
WalkSpeedSlider.Position = UDim2.new(0, 10, 0, 50)
WalkSpeedSlider.BackgroundTransparency = 1
WalkSpeedSlider.Parent = MainFrame

local WalkSpeedLabel = Instance.new("TextLabel")
WalkSpeedLabel.Name = "Label"
WalkSpeedLabel.Size = UDim2.new(0, 280, 0, 20)
WalkSpeedLabel.BackgroundTransparency = 1
WalkSpeedLabel.Text = "Walk Speed: " .. settings.walkSpeed
WalkSpeedLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
WalkSpeedLabel.Font = Enum.Font.Gotham
WalkSpeedLabel.TextSize = 14
WalkSpeedLabel.TextXAlignment = Enum.TextXAlignment.Left
WalkSpeedLabel.Parent = WalkSpeedSlider

local WalkSpeedBar = Instance.new("Frame")
WalkSpeedBar.Name = "Bar"
WalkSpeedBar.Size = UDim2.new(0, 280, 0, 10)
WalkSpeedBar.Position = UDim2.new(0, 0, 0, 25)
WalkSpeedBar.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
WalkSpeedBar.BorderSizePixel = 0
WalkSpeedBar.Parent = WalkSpeedSlider

local WalkSpeedFill = Instance.new("Frame")
WalkSpeedFill.Name = "Fill"
WalkSpeedFill.Size = UDim2.new((settings.walkSpeed - 16) / (50 - 16), 0, 1, 0)
WalkSpeedFill.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
WalkSpeedFill.BorderSizePixel = 0
WalkSpeedFill.Parent = WalkSpeedBar

local WalkSpeedButton = Instance.new("TextButton")
WalkSpeedButton.Name = "Button"
WalkSpeedButton.Size = UDim2.new(0, 280, 0, 30)
WalkSpeedButton.Position = UDim2.new(0, 0, 0, 20)
WalkSpeedButton.BackgroundTransparency = 1
WalkSpeedButton.Text = ""
WalkSpeedButton.Parent = WalkSpeedSlider

-- Slider untuk Gravity
local GravitySlider = Instance.new("Frame")
GravitySlider.Name = "GravitySlider"
GravitySlider.Size = UDim2.new(0, 280, 0, 50)
GravitySlider.Position = UDim2.new(0, 10, 0, 110)
GravitySlider.BackgroundTransparency = 1
GravitySlider.Parent = MainFrame

local GravityLabel = Instance.new("TextLabel")
GravityLabel.Name = "Label"
GravityLabel.Size = UDim2.new(0, 280, 0, 20)
GravityLabel.BackgroundTransparency = 1
GravityLabel.Text = "Gravity: " .. settings.gravity
GravityLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
GravityLabel.Font = Enum.Font.Gotham
GravityLabel.TextSize = 14
GravityLabel.TextXAlignment = Enum.TextXAlignment.Left
GravityLabel.Parent = GravitySlider

local GravityBar = Instance.new("Frame")
GravityBar.Name = "Bar"
GravityBar.Size = UDim2.new(0, 280, 0, 10)
GravityBar.Position = UDim2.new(0, 0, 0, 25)
GravityBar.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
GravityBar.BorderSizePixel = 0
GravityBar.Parent = GravitySlider

local GravityFill = Instance.new("Frame")
GravityFill.Name = "Fill"
GravityFill.Size = UDim2.new((settings.gravity - 50) / (300 - 50), 0, 1, 0)
GravityFill.BackgroundColor3 = Color3.fromRGB(255, 100, 0)
GravityFill.BorderSizePixel = 0
GravityFill.Parent = GravityBar

local GravityButton = Instance.new("TextButton")
GravityButton.Name = "Button"
GravityButton.Size = UDim2.new(0, 280, 0, 30)
GravityButton.Position = UDim2.new(0, 0, 0, 20)
GravityButton.BackgroundTransparency = 1
GravityButton.Text = ""
GravityButton.Parent = GravitySlider

-- Slider untuk Jump Power
local JumpPowerSlider = Instance.new("Frame")
JumpPowerSlider.Name = "JumpPowerSlider"
JumpPowerSlider.Size = UDim2.new(0, 280, 0, 50)
JumpPowerSlider.Position = UDim2.new(0, 10, 0, 170)
JumpPowerSlider.BackgroundTransparency = 1
JumpPowerSlider.Parent = MainFrame

local JumpPowerLabel = Instance.new("TextLabel")
JumpPowerLabel.Name = "Label"
JumpPowerLabel.Size = UDim2.new(0, 280, 0, 20)
JumpPowerLabel.BackgroundTransparency = 1
JumpPowerLabel.Text = "Jump Power: " .. settings.jumpPower
JumpPowerLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
JumpPowerLabel.Font = Enum.Font.Gotham
JumpPowerLabel.TextSize = 14
JumpPowerLabel.TextXAlignment = Enum.TextXAlignment.Left
JumpPowerLabel.Parent = JumpPowerSlider

local JumpPowerBar = Instance.new("Frame")
JumpPowerBar.Name = "Bar"
JumpPowerBar.Size = UDim2.new(0, 280, 0, 10)
JumpPowerBar.Position = UDim2.new(0, 0, 0, 25)
JumpPowerBar.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
JumpPowerBar.BorderSizePixel = 0
JumpPowerBar.Parent = JumpPowerSlider

local JumpPowerFill = Instance.new("Frame")
JumpPowerFill.Name = "Fill"
JumpPowerFill.Size = UDim2.new((settings.jumpPower - 0) / (100 - 0), 0, 1, 0)
JumpPowerFill.BackgroundColor3 = Color3.fromRGB(0, 255, 100)
JumpPowerFill.BorderSizePixel = 0
JumpPowerFill.Parent = JumpPowerBar

local JumpPowerButton = Instance.new("TextButton")
JumpPowerButton.Name = "Button"
JumpPowerButton.Size = UDim2.new(0, 280, 0, 30)
JumpPowerButton.Position = UDim2.new(0, 0, 0, 20)
JumpPowerButton.BackgroundTransparency = 1
JumpPowerButton.Text = ""
JumpPowerButton.Parent = JumpPowerSlider

-- Pilihan bahasa di kanan bawah
local LanguageFrame = Instance.new("Frame")
LanguageFrame.Name = "LanguageFrame"
LanguageFrame.Size = UDim2.new(0, 120, 0, 20)
LanguageFrame.Position = UDim2.new(1, -130, 1, -30)
LanguageFrame.BackgroundTransparency = 1
LanguageFrame.Parent = MainFrame

local LanguageLabel = Instance.new("TextLabel")
LanguageLabel.Name = "Label"
LanguageLabel.Size = UDim2.new(0, 60, 0, 20)
LanguageLabel.BackgroundTransparency = 1
LanguageLabel.Text = "Language:"
LanguageLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
LanguageLabel.Font = Enum.Font.Gotham
LanguageLabel.TextSize = 12
LanguageLabel.TextXAlignment = Enum.TextXAlignment.Left
LanguageLabel.Parent = LanguageFrame

local LanguageDropdown = Instance.new("TextButton")
LanguageDropdown.Name = "Dropdown"
LanguageDropdown.Size = UDim2.new(0, 60, 0, 20)
LanguageDropdown.Position = UDim2.new(0, 60, 0, 0)
LanguageDropdown.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
LanguageDropdown.TextColor3 = Color3.fromRGB(255, 255, 255)
LanguageDropdown.Text = settings.language
LanguageDropdown.Font = Enum.Font.Gotham
LanguageDropdown.TextSize = 12
LanguageDropdown.Parent = LanguageFrame

-- Fungsi untuk mengupdate slider
local function updateSlider(slider, value, min, max, property)
    local fill = slider:FindFirstChild("Bar"):FindFirstChild("Fill")
    local label = slider:FindFirstChild("Label")
    
    if fill and label then
        local normalized = math.clamp((value - min) / (max - min), 0, 1)
        fill.Size = UDim2.new(normalized, 0, 1, 0)
        
        if property == "walkSpeed" then
            label.Text = translations[settings.language].walkSpeed .. ": " .. math.floor(value)
            Humanoid.WalkSpeed = value
        elseif property == "gravity" then
            label.Text = translations[settings.language].gravity .. ": " .. math.floor(value)
            workspace.Gravity = value
        elseif property == "jumpPower" then
            label.Text = translations[settings.language].jumpPower .. ": " .. math.floor(value)
            Humanoid.JumpPower = value
        end
    end
end

-- Fungsi untuk mengupdate semua text berdasarkan bahasa
local function updateLanguage()
    Title.Text = translations[settings.language].title
    WalkSpeedLabel.Text = translations[settings.language].walkSpeed .. ": " .. settings.walkSpeed
    GravityLabel.Text = translations[settings.language].gravity .. ": " .. settings.gravity
    JumpPowerLabel.Text = translations[settings.language].jumpPower .. ": " .. settings.jumpPower
    CloseButton.Text = translations[settings.language].close
    MinimizeButton.Text = translations[settings.language].minimize
    LanguageLabel.Text = translations[settings.language].language
end

-- Fungsi untuk menangani input slider
local function setupSlider(slider, property, min, max, default)
    local button = slider:FindFirstChild("Button")
    local bar = slider:FindFirstChild("Bar")
    
    if button and bar then
        local isDragging = false
        
        button.MouseButton1Down:Connect(function(x)
            isDragging = true
            local xOffset = x - bar.AbsolutePosition.X
            local percent = math.clamp(xOffset / bar.AbsoluteSize.X, 0, 1)
            local value = min + (max - min) * percent
            settings[property] = value
            updateSlider(slider, value, min, max, property)
        end)
        
        button.MouseButton1Up:Connect(function()
            isDragging = false
        end)
        
        button.MouseMoved:Connect(function(x, y)
            if isDragging then
                local xOffset = x - bar.AbsolutePosition.X
                local percent = math.clamp(xOffset / bar.AbsoluteSize.X, 0, 1)
                local value = min + (max - min) * percent
                settings[property] = value
                updateSlider(slider, value, min, max, property)
            end
        end)
    end
end

-- Setup semua slider
setupSlider(WalkSpeedSlider, "walkSpeed", 16, 50, settings.walkSpeed)
setupSlider(GravitySlider, "gravity", 50, 300, settings.gravity)
setupSlider(JumpPowerSlider, "jumpPower", 0, 100, settings.jumpPower)

-- Terapkan pengaturan awal
Humanoid.WalkSpeed = settings.walkSpeed
workspace.Gravity = settings.gravity
Humanoid.JumpPower = settings.jumpPower

-- Setup dropdown bahasa
LanguageDropdown.MouseButton1Click:Connect(function()
    local languages = {"English", "Indonesia", "Spanish"}
    local currentIndex = table.find(languages, settings.language) or 1
    local nextIndex = currentIndex % #languages + 1
    settings.language = languages[nextIndex]
    LanguageDropdown.Text = settings.language
    updateLanguage()
end)

-- Update awal untuk bahasa
updateLanguage()
