local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local mouse = player:GetMouse()

-- 1. Criando a interface principal
local sg = Instance.new("ScreenGui")
sg.Name = "PainelPro"
sg.ResetOnSpawn = false
sg.Parent = player:WaitForChild("PlayerGui")

------------------------------------------------------------------
-- TELA DE LOGIN (FUNDO PRETO)
------------------------------------------------------------------
local LoginFrame = Instance.new("Frame")
LoginFrame.Size = UDim2.new(1, 0, 1, 0)
LoginFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
LoginFrame.ZIndex = 10
LoginFrame.Parent = sg

local LoginTitle = Instance.new("TextLabel")
LoginTitle.Size = UDim2.new(0, 200, 0, 50)
LoginTitle.Position = UDim2.new(0.5, -100, 0.2, 0)
LoginTitle.Text = "SISTEMA DE ACESSO"
LoginTitle.TextColor3 = Color3.new(1, 1, 1)
LoginTitle.Font = Enum.Font.GothamBold
LoginTitle.TextSize = 25
LoginTitle.BackgroundTransparency = 1
LoginTitle.ZIndex = 11
LoginTitle.Parent = LoginFrame

local KeyInput = Instance.new("TextBox")
KeyInput.Size = UDim2.new(0, 250, 0, 45)
KeyInput.Position = UDim2.new(0.5, -125, 0.4, 0)
KeyInput.PlaceholderText = "Key here"
KeyInput.Text = ""
KeyInput.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
KeyInput.TextColor3 = Color3.new(1, 1, 1)
KeyInput.ZIndex = 11
KeyInput.Parent = LoginFrame

local CheckBtn = Instance.new("TextButton")
CheckBtn.Size = UDim2.new(0, 250, 0, 45)
CheckBtn.Position = UDim2.new(0.5, -125, 0.5, 5)
CheckBtn.Text = "Check Key"
CheckBtn.BackgroundColor3 = Color3.fromRGB(0, 170, 100)
CheckBtn.TextColor3 = Color3.new(1, 1, 1)
CheckBtn.ZIndex = 11
CheckBtn.Parent = LoginFrame

local CopyBtn = Instance.new("TextButton")
CopyBtn.Size = UDim2.new(0, 250, 0, 45)
CopyBtn.Position = UDim2.new(0.5, -125, 0.6, 10)
CopyBtn.Text = "Link Key(Click to copy)"
CopyBtn.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
CopyBtn.TextColor3 = Color3.new(1, 1, 1)
CopyBtn.ZIndex = 11
CopyBtn.Parent = LoginFrame

local NotifyLabel = Instance.new("TextLabel")
NotifyLabel.Size = UDim2.new(0, 200, 0, 30)
NotifyLabel.Position = UDim2.new(0.5, -100, 0.7, 15)
NotifyLabel.Text = "Key copied!"
NotifyLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
NotifyLabel.BackgroundTransparency = 1
NotifyLabel.Visible = false
NotifyLabel.ZIndex = 11
NotifyLabel.Parent = LoginFrame

------------------------------------------------------------------
-- BOLA FLUTUANTE E MENU (INVISÍVEIS ATÉ O LOGIN)
------------------------------------------------------------------
local Ball = Instance.new("Frame")
Ball.Size = UDim2.new(0, 55, 0, 55)
Ball.Position = UDim2.new(0, 20, 0.5, 0)
Ball.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Ball.BackgroundTransparency = 0.4
Ball.Visible = false -- Escondida
Ball.Active = true
Ball.Parent = sg

local BallCorner = Instance.new("UICorner")
BallCorner.CornerRadius = UDim.new(1, 0)
BallCorner.Parent = Ball

local BallBtn = Instance.new("TextButton")
BallBtn.Size = UDim2.new(1, 0, 1, 0)
BallBtn.BackgroundTransparency = 1
BallBtn.Text = "🔥"
BallBtn.Parent = Ball

local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 220, 0, 320)
Main.Position = UDim2.new(0.5, -110, 0.5, -160)
Main.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Main.Visible = false -- Menu também escondido
Main.Parent = sg
Instance.new("UICorner").Parent = Main

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "HUB DE FUNÇÕES"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.GothamBold
Title.BackgroundTransparency = 1
Title.Parent = Main

------------------------------------------------------------------
-- FUNÇÃO PARA CRIAR OS BOTÕES DO MENU
------------------------------------------------------------------
local function createButton(text, pos, color, func)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.8, 0, 0, 40)
    btn.Position = pos
    btn.Text = text
    btn.BackgroundColor3 = color
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Font = Enum.Font.Gotham
    btn.Parent = Main
    
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 8)
    c.Parent = btn
    
    btn.MouseButton1Click:Connect(func)
    return btn
end

-- Criando as opções que você pediu:
createButton("🚀 FPS BOOST", UDim2.new(0.1, 0, 0.2, 0), Color3.fromRGB(50, 120, 200), function()
    for _, v in pairs(game:GetDescendants()) do
        if v:IsA("Texture") or v:IsA("Decal") then v.Transparency = 1
        elseif v:IsA("PostProcessEffect") then v.Enabled = false end
    end
end)

createButton("⚡ VELOCIDADE (20)", UDim2.new(0.1, 0, 0.4, 0), Color3.fromRGB(200, 150, 0), function()
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.WalkSpeed = 25
    end
end)

createButton("📍 TOOL TELEPORTE", UDim2.new(0.1, 0, 0.6, 0), Color3.fromRGB(150, 50, 200), function()
    local tool = Instance.new("Tool")
    tool.Name = "Clique Teleport"
    tool.RequiresHandle = false
    tool.Parent = player.Backpack
    tool.Activated:Connect(function()
        if mouse.Target then player.Character:SetPrimaryPartCFrame(CFrame.new(mouse.Hit.Position + Vector3.new(0, 3, 0))) end
    end)
end)

createButton("☠️ RESETAR", UDim2.new(0.1, 0, 0.8, 0), Color3.fromRGB(180, 40, 40), function()
    if player.Character then player.Character:BreakJoints() end
end)

------------------------------------------------------------------
-- SISTEMA DE LOGIN E DRAG
------------------------------------------------------------------

CheckBtn.MouseButton1Click:Connect(function()
    if KeyInput.Text == "FREE_KEY-=838IsnZxb@#iei8/)(udi.jeu~~♪†aBoS3amuxaGENE,ZEJ83jshs?$+72sup7" then
        LoginFrame.Visible = false
        Ball.Visible = true -- Libera a bolinha!
    else
        CheckBtn.Text = "ERRADO!"
        task.wait(1)
        CheckBtn.Text = "CHECK NÚMERO"
    end
end)

CopyBtn.MouseButton1Click:Connect(function()
    if setclipboard then setclipboard("https://roblox-script-4b50ck.lumi.ing") end
    NotifyLabel.Visible = true
    task.wait(1.5)
    NotifyLabel.Visible = false
end)

-- Arrastar a bolinha
local dragging, dragStart, startPos
BallBtn.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = Ball.Position
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        Ball.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

UserInputService.InputEnded:Connect(function(input) dragging = false end)

BallBtn.MouseButton1Click:Connect(function()
    Main.Visible = not Main.Visible
end)
