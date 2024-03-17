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


 local ToggleFarm = Tabs.Main:AddToggle("ToggleFarm", {Title = "Auto Farm", Default = false })
 ToggleFarm:OnChanged(function(Value)
     _G.AutoFarm = Value
 end)
 Options.ToggleFarm:SetValue(false)
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
 
 local ToggleAFK = Tabs.Main:AddToggle("ToggleAFK", {Title = "Auto AFK", Default = true })
 ToggleAFK:OnChanged(function(Value)
     _G.AutoAFK = Value
 end)
 Options.ToggleAFK:SetValue(false)
 LocalPlayer.Idled:Connect(function()
    VirtualUser:CaptureController()
    VirtualUser:ClickButton2(Vector2.new(), Camera.CFrame)
      end
    end
   end
   end)
end


