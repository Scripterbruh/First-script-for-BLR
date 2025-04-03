
-- Create a ScreenGui for the mobile button
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "MobileButton"
screenGui.Parent = game.StarterGui

-- Create a mobile button (gray and transparent)
local mobileButton = Instance.new("TextButton")
mobileButton.Name = "Tsbr11💀"
mobileButton.Text = "Tsbr11💀"
mobileButton.BackgroundColor3 = Color3.new(0.5, 0.5, 0.5)
mobileButton.BackgroundTransparency = 0.5
mobileButton.Size = UDim2.new(0, 50, 0, 50)
mobileButton.Position = UDim2.new(0, 10, 0, 10)
mobileButton.Parent = screenGui

-- Create a menu that will be displayed when the button is clicked
local menu = Instance.new("Frame")
menu.Name = "Menu"
menu.Size = UDim2.new(0, 200, 0, 250)
menu.Position = UDim2.new(0, 60, 0, 10)
menu.BackgroundColor3 = Color3.new(1, 1, 1)
menu.Visible = false
menu.Parent = screenGui

-- Create menu buttons
local kaiserButton = Instance.new("TextButton")
kaiserButton.Name = "Kaiser"
kaiserButton.Text = "Kaiser"
kaiserButton.Size = UDim2.new(0, 150, 0, 50)
kaiserButton.Position = UDim2.new(0, 25, 0, 25)
kaiserButton.Parent = menu

local nelIsagiButton = Instance.new("TextButton")
nelIsagiButton.Name = "NEL Isagi"
nelIsagiButton.Text = "NEL Isagi"
nelIsagiButton.Size = UDim2.new(0, 150, 0, 50)
nelIsagiButton.Position = UDim2.new(0, 25, 0, 100)
nelIsagiButton.Parent = menu

local reoButton = Instance.new("TextButton")
reoButton.Name = "Reo"
reoButton.Text = "Reo"
reoButton.Size = UDim2.new(0, 150, 0, 50)
reoButton.Position = UDim2.new(0, 25, 0, 175)
reoButton.Parent = menu

local noCdButton = Instance.new("TextButton")
noCdButton.Name = "No CD"
noCdButton.Text = "No CD"
noCdButton.Size = UDim2.new(0, 150, 0, 50)
noCdButton.Position = UDim2.new(0, 25, 0, 225)
noCdButton.Parent = menu

-- Function to display the menu when the button is clicked
local function displayMenu()
    menu.Visible = true
end

-- Function to execute the script when a button is clicked
local function executeScript(style)
    game.Players.LocalPlayer.PlayerStats.Style.Value = style
    menu.Visible = false
end

local function noCdScript()
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    local Controllers = ReplicatedStorage:FindFirstChild("Controllers")
    if Controllers then
        local AbilityController = Controllers:FindFirstChild("AbilityController") and require(Controllers.AbilityController)
        if AbilityController and AbilityController.AbilityCooldown then
            -- Store original function
            local originalCooldown = AbilityController.AbilityCooldown
            -- Override cooldown function to set cooldown to 0
            AbilityController.AbilityCooldown = function(self, abilityName, time, ...)
                return originalCooldown(self, abilityName, 0, ...) -- Force cooldown to 0
            end
            print("[SUCCESS] Ability cooldown set to 0 (instant spam)!")
        else
            print("[WARNING] AbilityController or AbilityCooldown not found!")
        end
    else
        print("[WARNING] Controllers folder not found in ReplicatedStorage!")
    end
end

-- Connect functions to buttons
mobileButton.MouseButton1Click:Connect(displayMenu)
kaiserButton.MouseButton1Click:Connect(function()
    executeScript("Kaiser")
end)
nelIsagiButton.MouseButton1Click:Connect(function()
    executeScript("NEL Isagi")
end)
reoButton.MouseButton1Click:Connect(function()
    executeScript("Reo")
end)
noCdButton.MouseButton1Click:Connect(noCdScript)
