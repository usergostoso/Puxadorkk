-- Criação de um script com UI em RGB e com título "Super Parts Puller 🔮 🤝 15M Leaks"

local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player.PlayerGui

-- Criação do Frame principal da UI
local mainFrame = Instance.new("Frame")
mainFrame.Parent = screenGui
mainFrame.Size = UDim2.new(0, 300, 0, 200)
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
mainFrame.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
mainFrame.BorderSizePixel = 0
mainFrame.BackgroundTransparency = 0.3
mainFrame.UICornerRadius = UDim.new(0, 20)

-- Background colorido em RGB
local gradient = Instance.new("UIGradient")
gradient.Parent = mainFrame
gradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 0)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(0, 255, 0)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(0, 0, 255))
}

-- Título da UI
local title = Instance.new("TextLabel")
title.Parent = mainFrame
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.Text = "Super Parts Puller 🔮 🤝 15M Leaks"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.SourceSansBold
title.TextSize = 20
title.TextScaled = true
title.BackgroundTransparency = 1

-- Caixa de entrada para a distância
local distanceInput = Instance.new("TextBox")
distanceInput.Parent = mainFrame
distanceInput.Size = UDim2.new(1, -20, 0, 40)
distanceInput.Position = UDim2.new(0, 10, 0, 50)
distanceInput.Text = "Distância"
distanceInput.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
distanceInput.TextColor3 = Color3.fromRGB(0, 0, 0)
distanceInput.Font = Enum.Font.SourceSans
distanceInput.TextSize = 18
distanceInput.TextScaled = true
distanceInput.UICornerRadius = UDim.new(0, 10)

-- Botão para puxar a parte
local pullButton = Instance.new("TextButton")
pullButton.Parent = mainFrame
pullButton.Size = UDim2.new(1, -20, 0, 40)
pullButton.Position = UDim2.new(0, 10, 0, 100)
pullButton.Text = "Puxar Parte"
pullButton.BackgroundColor3 = Color3.fromRGB(0, 150, 0)
pullButton.TextColor3 = Color3.fromRGB(255, 255, 255)
pullButton.Font = Enum.Font.SourceSans
pullButton.TextSize = 18
pullButton.TextScaled = true
pullButton.UICornerRadius = UDim.new(0, 10)

-- Evento para puxar a parte quando o botão for clicado
local function pullPart(part, distance)
    -- Verifica se a parte é válida
    if part and part:IsA("BasePart") then
        local originalPosition = part.Position
        local direction = (mouse.Hit.p - part.Position).unit
        local newPosition = originalPosition + direction * distance
        part.CFrame = CFrame.new(newPosition)
    end
end

-- Evento de clique do botão
pullButton.MouseButton1Click:Connect(function()
    -- Pega a distância digitada pelo jogador
    local distance = tonumber(distanceInput.Text) or 10 -- Se não digitar nada, distância padrão será 10

    -- Verifica se o jogador está clicando em uma parte
    local targetPart = mouse.Target
    if targetPart then
        pullPart(targetPart, distance)
    end
end)
