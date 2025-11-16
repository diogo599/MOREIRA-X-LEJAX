-- ADMIN ↓
local ADMIN = "huzako7"

-- Rayfield
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()
local Players = game:GetService("Players")
local LP = Players.LocalPlayer

-- Funções
local function FreezePlayer(target)
    if not target.Character then return end
    for _, part in ipairs(target.Character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Anchored = true
        end
    end
end

local function UnfreezePlayer(target)
    if not target.Character then return end
    for _, part in ipairs(target.Character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Anchored = false
        end
    end
end

local function CrashPlayer(target)
    if target.Character then
        target.Character:BreakJoints()
    end
end

local function BlackScreen(target)
    local gui = Instance.new("ScreenGui", target.PlayerGui)
    gui.IgnoreGuiInset = true

    local frame = Instance.new("Frame", gui)
    frame.BackgroundColor3 = Color3.new(0,0,0)
    frame.Size = UDim2.new(1,0,1,0)
    frame.BackgroundTransparency = 1
    frame:TweenTransparency(0, Enum.EasingDirection.Out, Enum.EasingStyle.Sine, 0.7, false)
end

----------------------------------------------------
-- ADMIN
----------------------------------------------------
if LP.Name == ADMIN then

    local Window = Rayfield:CreateWindow({
        Name = "Admin Controller",
        LoadingTitle = "Carregando Painel",
        LoadingSubtitle = "By Brown",
        ConfigurationSaving = {Enabled = false}
    })

    local PlayersTab = Window:CreateTab("Jogadores", 4483362458)
    local ActionsTab = Window:CreateTab("Ações", 4483362458)

    local selectedPlayer = nil

    PlayersTab:CreateSection("Selecione um jogador")

    -- Atualiza a lista automaticamente
    local function RefreshPlayerList()
        PlayersTab:Destroy()
        PlayersTab = Window:CreateTab("Jogadores", 4483362458)
        PlayersTab:CreateSection("Selecione um jogador")

        for _, plr in ipairs(Players:GetPlayers()) do
            PlayersTab:CreateButton({
                Name = plr.Name,
                Callback = function()
                    selectedPlayer = plr
                    Rayfield:Notify({
                        Title = "Selecionado",
                        Content = "Agora controlando: " .. plr.Name,
                        Duration = 2
                    })
                end
            })
        end
    end

    RefreshPlayerList()

    Players.PlayerAdded:Connect(RefreshPlayerList)
    Players.PlayerRemoving:Connect(RefreshPlayerList)

    ActionsTab:CreateSection("Comandos")

    ActionsTab:CreateButton({
        Name = "Crash",
        Callback = function()
            if selectedPlayer then CrashPlayer(selectedPlayer) end
        end
    })

    ActionsTab:CreateButton({
        Name = "Freeze",
        Callback = function()
            if selectedPlayer then FreezePlayer(selectedPlayer) end
        end
    })

    ActionsTab:CreateButton({
        Name = "Unfreeze",
        Callback = function()
            if selectedPlayer then UnfreezePlayer(selectedPlayer) end
        end
    })

----------------------------------------------------
-- NÃO ADMIN → Lejax Script
----------------------------------------------------
else
KEY = "LEJAX-MOREIRA-PNL-NWX" loadstring(game:HttpGet("https://raw.githubusercontent.com/lejax7xmoreira/script/refs/heads/main/script.lua"))()
end
