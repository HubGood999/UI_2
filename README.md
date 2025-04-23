spawn(function()
    while task.wait() do
        pcall(function()
            if _G.Enabled_Walk_Speed then
                game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = _G.Walk_Speed
            else
                game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
            end
        end)
    end
end)
spawn(function()
    while task.wait() do
        pcall(function()
            if _G.Enabled_Jump_Power then
                game.Players.LocalPlayer.Character.Humanoid.JumpPower = _G.Jump_Power
            else
                game.Players.LocalPlayer.Character.Humanoid.JumpPower = 50
            end
        end)
    end
end)
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Exterme City KaK",
    SubTitle = "by God N",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl 
})

local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "home" }),
    Player = Window:AddTab({ Title = "Player", Icon = "layers" })
}
Tabs.Player:AddButton({
    Title = "Respawn ReviveSystem",
    Description = 'Click for Respawn',
    Callback = function()
        game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer("Respawn",game:GetService("Players").LocalPlayer)
    end
})
task.wait()
Tabs.Player:AddInput("Jump Power", {
    Title = "Player Name",
    Default = false,
    Placeholder = "Placeholder",
    Numeric = false,
    Finished = false,
    Callback = function(Input)
        v = Input
        local args = {
            [1] = game:GetService("Players"):WaitForChild(v)
        }

        game:GetService("ReplicatedStorage"):WaitForChild("RemoteEventA"):WaitForChild("AED_Remote"):FireServer(unpack(args))
    end
})
Tabs.Player:AddSection("Humanoid")
task.wait()
Tabs.Player:AddInput("Walk Speed", {
    Title = "Walk Speed",
    Default = false,
    Placeholder = "Placeholder",
    Numeric = false,
    Finished = false,
    Callback = function(Input)
        _G.Walk_Speed = Input
    end
})
task.wait()
Tabs.Player:AddInput("Jump Power", {
    Title = "Jump Power",
    Default = false,
    Placeholder = "Placeholder",
    Numeric = false,
    Finished = false,
    Callback = function(Input)
        _G.Jump_Power = Input
    end
})
task.wait()
Tabs.Player:AddToggle("Enabled Walk Speed", {Title = "Enabled Walk Speed", Default = false, Callback = function(Toggle)
    _G.Enabled_Walk_Speed = Toggle
end})
task.wait()
Tabs.Player:AddToggle("Enabled Jump Power", {Title = "Enabled Jump Power", Default =false, Callback = function(Toggle)
    _G.Enabled_Jump_Power = Toggle
end})
