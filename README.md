local redzlib = loadstring(game:HttpGet("https://raw.githubusercontent.com/tbao143/Library-ui/refs/heads/main/Redzhubui"))()

local Window = redzlib:MakeWindow({
    Title = "Matrix hub v4.2",
    SubTitle = "by Matrix Community",
    SaveFolder = "AmirHubConfigs"
})

Window:AddMinimizeButton({
    Button = { Image = "rbxassetid://71014873973869", BackgroundTransparency = 0 },
    Corner = { CornerRadius = UDim.new(35, 1) },
})

-- Abas principais
local TrollTab = Window:MakeTab({"Troll", "trollicon"})
local ESPTab = Window:MakeTab({"ESP", "espicon"})
local ConfigTab = Window:MakeTab({"Configurações", "configicon"})

Window:SelectTab(TrollTab)

------------------------------------------------------
-- ABA: TROLL
------------------------------------------------------
local playerList = {}
for _, plr in pairs(game.Players:GetPlayers()) do
    if plr ~= game.Players.LocalPlayer then
        table.insert(playerList, plr.Name)
    end
end

local selectedPlayer

TrollTab:AddDropdown({
    Name = "Escolher Jogador",
    Options = playerList,
    Callback = function(v)
        selectedPlayer = v
    end
})

TrollTab:AddButton({
    Name = "Fling",
    Callback = function()
        local target = game.Players:FindFirstChild(selectedPlayer)
        if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
            local myHRP = game.Players.LocalPlayer.Character.HumanoidRootPart
            local targetHRP = target.Character:FindFirstChild("HumanoidRootPart")
            myHRP.CFrame = targetHRP.CFrame
            wait(0.2)
            myHRP.Velocity = Vector3.new(9999, 9999, 9999)
        end
    end
})

TrollTab:AddButton({
    Name = "Kill (Break Joints)",
    Callback = function()
        local target = game.Players:FindFirstChild(selectedPlayer)
        if target and target.Character then
            target.Character:BreakJoints()
        end
    end
})

------------------------------------------------------
-- ABA: ESP
------------------------------------------------------
ESPTab:AddButton({
    Name = "Ativar ESP",
    Callback = function()
        for _, plr in pairs(game.Players:GetPlayers()) do
            if plr ~= game.Players.LocalPlayer and plr.Character and plr.Character:FindFirstChild("Head") then
                local esp = Instance.new("BoxHandleAdornment", plr.Character.Head)
                esp.Size = Vector3.new(2, 2, 1)
                esp.Color3 = Color3.fromRGB(255, 0, 0)
                esp.Transparency = 0.5
                esp.AlwaysOnTop = true
                esp.Adornee = plr.Character.Head
            end
        end
    end
})

------------------------------------------------------
-- ABA: CONFIGURAÇÕES
------------------------------------------------------
ConfigTab:AddToggle({
    Name = "Modo Noturno",
    Callback = function(v)
        if v then
            game.Lighting.Brightness = 0
        else
            game.Lighting.Brightness = 2
        end
    end
})

ConfigTab:AddButton({
    Name = "Reiniciar Personagem",
    Callback = function()
        game.Players.LocalPlayer.Character:BreakJoints()
    end
})
