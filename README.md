-------------------------------------------------
-- 📱 MOBILE QUEST BUTTON (by samucaGENEZZ)
-------------------------------------------------

local player = game:GetService("Players").LocalPlayer
local TweenService = game:GetService("TweenService")

-- criar gui
local gui = Instance.new("ScreenGui")
gui.Name = "MobileQuestGui"
gui.ResetOnSpawn = false
gui.Parent = player.PlayerGui

-- botão grande mobile
local button = Instance.new("TextButton")
button.Parent = gui
button.Size = UDim2.new(0.35,0,0.09,0)
button.Position = UDim2.new(0.325,0,0.87,0)
button.BackgroundColor3 = Color3.fromRGB(20,20,20)
button.TextColor3 = Color3.fromRGB(255,255,255)
button.TextScaled = true
button.Text = "📱 QUEST"
button.BorderSizePixel = 0
button.AutoButtonColor = true

Instance.new("UICorner",button).CornerRadius = UDim.new(0,25)

-------------------------------------------------
-- função pegar quest
-------------------------------------------------

local function DoQuest()

    CheckQuest() -- usa SUA função original

    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")

    if hrp and CFrameQuest then
        hrp.CFrame = CFrameQuest + Vector3.new(0,3,0)
    end

    task.wait(0.3)

    -- tenta iniciar quest automaticamente
    pcall(function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(
            "StartQuest",
            NameQuest,
            LevelQuest
        )
    end)

    task.wait(0.3)

    if hrp and CFrameMon then
        hrp.CFrame = CFrameMon + Vector3.new(0,3,0)
    end
end

-------------------------------------------------
-- animação clique
-------------------------------------------------

button.MouseButton1Click:Connect(function()

    local tween = TweenService:Create(button,
        TweenInfo.new(0.1),
        {Size = UDim2.new(0.32,0,0.085,0)}
    )
    tween:Play()

    DoQuest()

    task.wait(0.1)

    TweenService:Create(button,
        TweenInfo.new(0.1),
        {Size = UDim2.new(0.35,0,0.09,0)}
    ):Play()
end)
