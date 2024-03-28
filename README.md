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
