
local resources = workspace.Resources

-- Función para teletransportar al jugador encima de un nodo específico y hacerlo dar vueltas alrededor del nodo a una distancia
local function teleportAndCircleAroundNode(node, distance, height, duration)
    if node and node:IsA("Model") and node.Name == "Gold Node" then
        local primaryPart = node:FindFirstChild("Reference")
        if primaryPart then
            local playerCharacter = player.Character
            local startTime = tick()
            while tick() - startTime < duration do
                local circlePosition = primaryPart.Position + Vector3.new(distance * math.cos(tick()), height, distance * math.sin(tick())) -- Ajusta la altura y distancia
                playerCharacter:SetPrimaryPartCFrame(CFrame.new(circlePosition, primaryPart.Position))
                wait(0) -- Teletransportación instantánea (sin espera)
            end
        end
    end
end

-- Bucle para teletransportar al jugador encima de cada "Gold Node" y hacerlo dar vueltas alrededor de cada uno durante 20 segundos
while true do
    for _, node in pairs(resources:GetChildren()) do
        local distance = 1 -- Ajusta la distancia desde el nodo según sea necesario
        local height = 2 -- Ajusta la altura según sea necesario
        local duration = 18 -- Duración en segundos en cada nodo
        teleportAndCircleAroundNode(node, distance, height, duration)
    end
end
