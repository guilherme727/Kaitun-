# Kaitun-
-- Configurações
getgenv().nomeScript = "Gui Hub Farm Bot"
getgenv().fruitParaFarmar = "Light Fruit"
getgenv().tempoDeAtaque = 0.1
getgenv().distanciaDeAtaque = 15
getgenv().levelMinimo = 100
getgenv().paused = true

-- Criação da janela
local gui = Instance.new("ScreenGui")
gui.Name = getgenv().nomeScript
gui.Parent = game.StarterGui

local frame = Instance.new("Frame")
frame.Name = "Config"
frame.Size = UDim2.new(0, 200, 0, 100)
frame.Position = UDim2.new(0.5, -100, 0.5, -50)
frame.BackgroundTransparency = 0.5
frame.Parent = gui

local texto = Instance.new("TextLabel")
texto.Name = "Titulo"
texto.Size = UDim2.new(1, 0, 0, 20)
texto.Text = getgenv().nomeScript
texto.Font = Enum.Font.SourceSansBold
texto.TextColor3 = Color3.new(1, 1, 1)
texto.BackgroundTransparency = 1
texto.Parent = frame

local botao = Instance.new("TextButton")
botao.Name = "Ativar"
botao.Size = UDim2.new(1, 0, 0, 30)
botao.Text = "Ativar"
botao.Font = Enum.Font.SourceSans
botao.TextColor3 = Color3.new(1, 1, 1)
botao.BackgroundTransparency = 0.5
botao.Parent = frame

-- Função para ativar/desativar o script
local function ativarDesativar()
    getgenv().paused = not getgenv().paused
    if getgenv().paused then
        botao.Text = "Ativar"
    else
        botao.Text = "Desativar"
    end
end

-- Conectar função ao botão
botao.MouseButton1Click:Connect(ativarDesativar)

-- Farm Loop
while true do
    if not getgenv().paused then
        local fruits = game:GetService("Workspace"):GetDescendants()
        local fruitMaisProximo = nil
        local distanciaMaisProxima = math.huge

        -- Encontra o fruit mais próximo
        for _, objeto in pairs(fruits) do
            if objeto ~= nil
