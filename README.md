
-- Referências para o objeto da arma
local tool = script.Parent
local handle = tool:WaitForChild("Handle") -- A parte física da arma (handle) 
local player = game.Players.LocalPlayer -- O jogador que está segurando a arma

-- Propriedades do projétil
local projectileSpeed = 100 -- Velocidade do projétil
local projectileLifetime = 5 -- Tempo de vida do projétil (em segundos)

-- Função para disparar o projétil
local function fireProjectile()
    -- Cria um projétil (pode ser uma esfera ou outra parte)
    local projectile = Instance.new("Part")
    projectile.Size = Vector3.new(1, 1, 3)
    projectile.Shape = Enum.PartType.Block
    projectile.Anchored = false
    projectile.CanCollide = true
    projectile.Position = handle.Position + handle.CFrame.LookVector * 2
    projectile.Parent = game.Workspace
    projectile.BrickColor = BrickColor.new("Bright red")

    -- Definir a velocidade do projétil
    local velocity = Instance.new("BodyVelocity")
    velocity.MaxForce = Vector3.new(4000, 4000, 4000) -- Força máxima para o projétil
    velocity.Velocity = handle.CFrame.LookVector * projectileSpeed
    velocity.Parent = projectile

    -- Após um tempo, destrua o projétil
    game:GetService("Debris"):AddItem(projectile, projectileLifetime)
end

-- Função para o que acontece quando o jogador clica
local function onActivated()
    fireProjectile()
end

-- Conectar a função ao evento de ativação da ferramenta
tool.Activated:Connect(onActivated)
