--abaixo estara lib da nossa ui       

local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

local UI = Lib:Create{
   Theme = "Dark", -- or any other theme
   Size = UDim2.new(0, 555, 0, 400) -- default
}

local Main = UI:Tab{
   Name = "inicio"
}

local Divider = Main:Divider{
   Name = "inicio shit"
}

local QuitDivider = Main:Divider{
   Name = "sair"
}

-- Arsenal Aimbot with ESP
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera
local Mouse = LocalPlayer:GetMouse()

local function GetClosestPlayer()
    local ClosestPlayer = nil
    local ShortestDistance = math.huge

    for _, Player in pairs(Players:GetPlayers()) do
        if Player ~= LocalPlayer and Player.Character and Player.Character:FindFirstChild("Head") and Player.Character:FindFirstChild("Humanoid") and Player.Character.Humanoid.Health > 0 then
            local Distance = (Player.Character.Head.Position - Camera.CFrame.p).Magnitude
            if Distance < ShortestDistance then
                ClosestPlayer = Player
                ShortestDistance = Distance
            end
        end
    end

    return ClosestPlayer
end

local function ESP(Player)
    local Box = Drawing.new("Quad")
    Box.Visible = false
    Box.PointA = Vector2.new(0, 0)
    Box.PointB = Vector2.new(0, 0)
    Box.PointC = Vector2.new(0, 0)
    Box.PointD = Vector2.new(0, 0)
    Box.Color = Color3.fromRGB(255, 255, 255)
    Box.Thickness = 2
    Box.Transparency = 1
    Box.Filled = false
    Box.Visible = true

    game:GetService("RunService").RenderStepped:Connect(function()
        if Player.Character and Player.Character:FindFirstChild("Head") and Player.Character:FindFirstChild("Humanoid") and Player.Character.Humanoid.Health > 0 then
            local Position, OnScreen = Camera:WorldToViewportPoint(Player.Character.Head.Position)
            if OnScreen then
                local Size = math.clamp(2000 / (Player.Character.Head.Position - Camera.CFrame.p).Magnitude, 2, 20)
                Box.PointA = Vector2.new(Position.X - Size, Position.Y - Size)
                Box.PointB = Vector2.new(Position.X + Size, Position.Y - Size)
                Box.PointC = Vector2.new(Position.X + Size, Position.Y + Size)
                Box.PointD = Vector2.new(Position.X - Size, Position.Y + Size)
                Box.Visible = true
            else
                Box.Visible = false
            end
        else
            Box.Visible = false
        end
    end)
end

local function Aimbot()
    local ClosestPlayer = GetClosestPlayer()
    if ClosestPlayer then
        local Position = Camera:WorldToScreenPoint(ClosestPlayer.Character.Head.Position)
        mousemoverel((Position.X - Mouse.X), (Position.Y - Mouse.Y))
    end
end

game:GetService("RunService").RenderStepped:Connect(function()
    Aimbot()
    for _, Player in pairs(Players:GetPlayers()) do
        ESP(Player)
    end
end)
