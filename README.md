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
    ToggleButton.Text = "Zephyr"
    ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    ToggleButton.TextSize = 15.000
    ToggleButton.Draggable = true
    ToggleButton.MouseButton1Click:Connect(function()
        game:GetService("VirtualInputManager"):SendKeyEvent(true,Enum.KeyCode.End,false,game)
    end)
 
 --Vars
 LocalPlayer = game:GetService("Players").LocalPlayer
 Camera = workspace.CurrentCamera
 VirtualUser = game:GetService("VirtualUser")
 MarketplaceService = game:GetService("MarketplaceService")
 
 --Get Current Vehicle
 function GetCurrentVehicle()
     return LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") and LocalPlayer.Character.Humanoid.SeatPart and LocalPlayer.Character.Humanoid.SeatPart.Parent
 end
 
 --Regular TP
 function TP(cframe)
     GetCurrentVehicle():SetPrimaryPartCFrame(cframe)
 end
 
 --Velocity TP
 function VelocityTP(cframe)
     TeleportSpeed = math.random(600, 600)
     Car = GetCurrentVehicle()
     local BodyGyro = Instance.new("BodyGyro", Car.PrimaryPart)
     BodyGyro.P = 5000
     BodyGyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
     BodyGyro.CFrame = Car.PrimaryPart.CFrame
     local BodyVelocity = Instance.new("BodyVelocity", Car.PrimaryPart)
     BodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
     BodyVelocity.Velocity = CFrame.new(Car.PrimaryPart.Position, cframe.p).LookVector * TeleportSpeed
     wait((Car.PrimaryPart.Position - cframe.p).Magnitude / TeleportSpeed)
     BodyVelocity.Velocity = Vector3.new()
     wait(0.1)
     BodyVelocity:Destroy()
     BodyGyro:Destroy()
 end
 
 --Auto Farm
 local ToggleFarm = Tabs.Main:AddToggle("ToggleFarm", {Title = "Auto Farm", Default = true })
 ToggleFarm:OnChanged(function(Value)
     _G.AutoFarm = Value
 end)
 Options.ToggleLevel:SetValue(false)
 if _G.AutoFarm then
 StartPosition = CFrame.new(4940.19775, 66.0195084, -1933.99927, 0.343969434, -0.00796990748, -0.938947022, 0.00281227613, 0.999968231, -0.00745762791, 0.938976645, -7.53822824e-05, 0.343980938)
 EndPosition = CFrame.new(1827.3407, 66.0150146, -658.946655, -0.366112858, 0.00818905979, 0.930534422, 0.00240773871, 0.999966264, -0.00785277691, -0.930567324, -0.000634518801, -0.366120219)
 AutoFarmFunc = coroutine.create(function()
     while wait() do
         if not AutoFarm then
             AutoFarmRunning = false
             coroutine.yield()
         end
         AutoFarmRunning = true
         pcall(function()
             if not GetCurrentVehicle() and tick() - (LastNotif or 0) > 5 then
                 LastNotif = tick()
             else
                 TP(StartPosition + (TouchTheRoad and Vector3.new(0,0,0) or Vector3.new(0, 0, 0)))
                 VelocityTP(EndPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
                 TP(EndPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
                 VelocityTP(StartPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
             end
         end)
     end
 end)
 
 --Anti AFK
 local ToggleAFK = Tabs.Main:AddToggle("ToggleAFK", {Title = "Anti AFK", Default = true })
 ToggleAFK:OnChanged(function(Value)
     _G.AutoAFK = Value
 end)
 Options.ToggleAFK:SetValue(false)
 if _G.AutoAFK then
 LocalPlayer.Idled:Connect(function()
     VirtualUser:CaptureController()
     VirtualUser:ClickButton2(Vector2.new(), Camera.CFrame)
 end)
