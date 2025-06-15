local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Função que desenha um ESP (aqui, um rótulo acima da cabeça)
local function drawESP(player)
    if player == LocalPlayer then return end -- ignora si mesmo

    local character = player.Character
    if not character or not character:FindFirstChild("Head") then return end

    -- Checa se são do mesmo time
    if player.Team == LocalPlayer.Team then return end

    -- Cria um BillboardGui acima da cabeça
    local billboard = Instance.new("BillboardGui", character.Head)
    billboard.Name = "ESP"
    billboard.Size = UDim2.new(0, 100, 0, 40)
    billboard.StudsOffset = Vector3.new(0, 2, 0)
    billboard.AlwaysOnTop = true

    local label = Instance.new("TextLabel", billboard)
    label.Size = UDim2.new(1, 0, 1, 0)
    label.BackgroundTransparency = 1
    label.Text = player.Name
    label.TextColor3 = Color3.new(1, 0, 0) -- vermelho
    label.TextStrokeTransparency = 0.5
end

-- Função principal para adicionar ESP a todos os jogadores
local function applyESP()
    for _, player in pairs(Players:GetPlayers()) do
        drawESP(player)
    end

    Players.PlayerAdded:Connect(drawESP)
end

applyESP()
