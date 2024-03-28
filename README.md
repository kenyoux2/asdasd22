----------------------------------------------------------------------------------------------------------------------------------------------
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
----------------------------------------------------------------------------------------------------------------------------------------------
local Window = Fluent:CreateWindow({
    Title = "Zephyr Hub",
    SubTitle = "Version 1.01",
    TabWidth = 160,
    Size = UDim2.fromOffset(500, 350),
    Acrylic = false,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.End
})
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "home" }),
}
local Options = Fluent.Options
do

--------------------------------------------------------------------------------------------------------------------------------------------
---Close UI
local ToggleUI = Instance.new("ScreenGui")
local ToggleButton = Instance.new("TextButton")
local ToggleButtonHUI = Instance.new("UICorner")
ToggleUI.Name = "ToggleUI"
ToggleUI.Parent = game.CoreGui
ToggleUI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = ToggleUI
ToggleButton.BackgroundColor3 = Color3.fromRGB(30,20,20)
ToggleButton.BackgroundTransparency = 0.1
ToggleButton.BorderSizePixel = 0
ToggleButton.Position = UDim2.new(0.120833337, 0, 0.0952890813, 0)
ToggleButton.Size = UDim2.new(0, 50, 0, 50)
ToggleButton.Font = Enum.Font.SourceSans
ToggleButton.Text = "Alchey"
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.TextSize = 15.000
ToggleButton.Draggable = true
ToggleButton.MouseButton1Click:Connect(function()
	game:GetService("VirtualInputManager"):SendKeyEvent(true,Enum.KeyCode.End,false,game)
end)
--------------------------------------------------------------------------------------------------------------------------------------------
--Remove Effect
if game:GetService("ReplicatedStorage").Effect.Container:FindFirstChild("Death") then
	game:GetService("ReplicatedStorage").Effect.Container.Death:Destroy()
end
if game:GetService("ReplicatedStorage").Effect.Container:FindFirstChild("Respawn") then
	game:GetService("ReplicatedStorage").Effect.Container.Respawn:Destroy()
end
--------------------------------------------------------------------------------------------------------------------------------------------
-- Hehe
--------------------------------------------------------------------------------------------------------------------------------------------
--Create Tabs



local ToggleLevel = Tabs.Main:AddToggle("ToggleFarm", {Title = "Auto Farm", Default = false })
ToggleFarm:OnChanged(function(Value)
local co1 = coroutine.create(function()
local player = game:GetService("Players").LocalPlayer
local mouse = player:GetMouse()
local beam = false
local UIS = game:GetService("UserInputService")
local keyBind = "F"
UIS.InputBegan:Connect(function(input,Chatting)
if Chatting then return end
if input.KeyCode == Enum.KeyCode[keyBind] then
    if beam == false then
        beam = true
        while beam == true do
            wait (0.01)
            local pos = mouse.Hit.Position
            local A_1 = pos
            local Event = game:GetService("Workspace")[player.Name].Bow.Shot.ShootArrow
            Event:FireServer(A_1)
        end
    else
        beam = false
    end
end
end)
end)

local co2 = coroutine.create(function()
local player = game:GetService("Players").LocalPlayer
local mouse = player:GetMouse()
local UIS = game:GetService("UserInputService")
local keyBind = "F"
UIS.InputBegan:Connect(function(input,Chatting)
if Chatting then return end
if input.KeyCode == Enum.KeyCode[keyBind] then
    for count = 0, 50, 1 do
        wait (0.001)
        local pos = mouse.Hit.Position
        local A_1 = pos
        local A_2 = 0
        local A_3 = game:GetService("Workspace")[player.Name]
        local Event = game:GetService("Workspace")[player.Name]["Star Cannon"].Shoot.RemoteEvent
        Event:FireServer(A_1, A_2, A_3)
    end
    wait (1)
end
end)
end)

coroutine.resume(co1)
coroutine.resume(co2)

local player = game:GetService("Players").LocalPlayer
local mouse = player:GetMouse()
local beam = false
local UIS = game:GetService("UserInputService")
local keyBind = "F"
UIS.InputBegan:Connect(function(input,Chatting)
if Chatting then return end
if input.KeyCode == Enum.KeyCode[keyBind] then
    if beam == false then
        beam = true
        while beam == true do
            wait (0.001)
            local pos = mouse.Hit.Position
            local A_1 = pos
            local A_2 = 0
            local A_3 = game:GetService("Workspace")[player.Name]
            local Event = game:GetService("Workspace")[player.Name].Musket.Shoot.RemoteEvent
            Event:FireServer(A_1, A_2, A_3)
        end
    else
        beam = false
    end
end
end)
