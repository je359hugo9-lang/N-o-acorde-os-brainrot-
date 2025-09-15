-- Variáveis para armazenar a posição salva
local savedPosition = nil

-- Função para salvar a posição atual do jogador
function salvarPosicao()
    local player = game.Players.LocalPlayer
    if player and player.Character then
        local character = player.Character
        savedPosition = character.HumanoidRootPart.Position
        print("Posição salva com sucesso: " .. tostring(savedPosition))
    else
        print("Erro: Jogador ou personagem não encontrado!")
    end
end

-- Função para teleportar o jogador para a posição salva
function teleportar()
    local player = game.Players.LocalPlayer
    if savedPosition then
        if player and player.Character then
            local character = player.Character
            -- Teleporta o jogador para a posição salva
            character:SetPrimaryPartCFrame(CFrame.new(savedPosition))
            print("Teleportado para a posição salva!")
        else
            print("Erro: Jogador ou personagem não encontrado!")
        end
    else
        print("Erro: Nenhuma posição salva encontrada!")
    end
end

-- Exemplo de como você pode associar essas funções a botões no seu mod menu:
-- (Lembre-se que esses são apenas exemplos e podem ser ajustados conforme sua necessidade)

-- Criar o botão "Salvar Posição"
local salvarButton = Instance.new("TextButton")
salvarButton.Text = "Salvar Posição"
salvarButton.Size = UDim2.new(0, 200, 0, 50)
salvarButton.Position = UDim2.new(0, 0, 0, 0)
salvarButton.Parent = game.Players.LocalPlayer.PlayerGui:WaitForChild("ScreenGui")  -- Certifique-se de ter uma ScreenGui no seu PlayerGui

salvarButton.MouseButton1Click:Connect(function()
    salvarPosicao()
end)

-- Criar o botão "Teleportar"
local teleportarButton = Instance.new("TextButton")
teleportarButton.Text = "Teleportar"
teleportarButton.Size = UDim2.new(0, 200, 0, 50)
teleportarButton.Position = UDim2.new(0, 0, 0, 60)  -- Mudando a posição do botão para não sobrepor o outro
teleportarButton.Parent = game.Players.LocalPlayer.PlayerGui:WaitForChild("ScreenGui")

teleportarButton.MouseButton1Click:Connect(function()
    teleportar()
end)

-- Instruções:
-- 1. Sempre que clicar em "Salvar Posição", o script salvará a posição atual do jogador.
-- 2. Sempre que clicar em "Teleportar", o jogador será teleportado para a posição salva.
