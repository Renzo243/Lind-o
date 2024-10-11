
local team = "Pirates" -- Pode ser "Pirates" ou "Marines"
local autoKen = true
local autoBuso = true

-- Função principal
local function autoBounty()
    while true do
        -- Verifica se o jogador está no time correto
        if game.Players.LocalPlayer.Team.Name ~= team then
            game.ReplicatedStorage.Remotes.CommF_:InvokeServer("SetTeam", team)
        end

        -- Ativa Ken Haki automaticamente
        if autoKen and not game.Players.LocalPlayer.Character:FindFirstChild("Ken Haki") then
            game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Ken")
        end

        -- Ativa Buso Haki automaticamente
        if autoBuso and not game.Players.LocalPlayer.Character:FindFirstChild("Buso Haki") then
            game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Buso")
        end

        -- Procura por inimigos e ataca
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Team.Name ~= team and player.Character and player.Character:FindFirstChild("Humanoid") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
                game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Attack", player)
            end
        end

        wait(1) -- Espera 1 segundo antes de repetir
    end
end

-- Inicia o script
autoBounty()
