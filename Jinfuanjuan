local player = game.Players.LocalPlayer
local vim = game:GetService("VirtualInputManager")

-- 🖥️ Tạo GUI
local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.Name = "AutoGUI"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 250, 0, 300)
frame.Position = UDim2.new(0.5, -125, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 2

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 30)
title.Text = "Auto Tycoon ARK"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundColor3 = Color3.fromRGB(50, 50, 50)

local function createButton(text, position)
    local button = Instance.new("TextButton", frame)
    button.Size = UDim2.new(1, -10, 0, 40)
    button.Position = UDim2.new(0, 5, 0, position)
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
    return button
end

local buildButton = createButton("Auto Build: OFF", 40)
local summonButton = createButton("Auto Summon: OFF", 90)
local dumpButton = createButton("Dump Source", 140)

-- 🏷️ TextBox nhập số
local delayLabel = Instance.new("TextLabel", frame)
delayLabel.Size = UDim2.new(1, 0, 0, 20)
delayLabel.Position = UDim2.new(0, 0, 0, 190)
delayLabel.Text = "Nhập số 1 để kích hoạt"
delayLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
delayLabel.BackgroundColor3 = Color3.fromRGB(50, 50, 50)

local inputBox = Instance.new("TextBox", frame)
inputBox.Size = UDim2.new(1, -10, 0, 30)
inputBox.Position = UDim2.new(0, 5, 0, 215)
inputBox.Text = ""
inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
inputBox.BackgroundColor3 = Color3.fromRGB(90, 90, 90)

-- 🛠️ Auto Build
local autoBuild = false
local function buildLoop()
    while autoBuild do
        for _, v in ipairs(workspace:GetDescendants()) do
            if v:IsA("ClickDetector") then
                fireclickdetector(v)
                task.wait(0.5)
            elseif v:IsA("ProximityPrompt") then
                fireproximityprompt(v)
                task.wait(0.5)
            end
        end
        task.wait(2)
    end
end

buildButton.MouseButton1Click:Connect(function()
    if inputBox.Text == "1" then
        autoBuild = not autoBuild
        buildButton.Text = autoBuild and "Auto Build: ON" or "Auto Build: OFF"
        if autoBuild then
            task.spawn(buildLoop)
        end
    else
        print("❌ Bạn phải nhập số 1 để kích hoạt Auto Build!")
    end
end)

-- 🔹 Auto Summon (Touch Nút Xanh)
local autoSummon = false
local function summonLoop()
    while autoSummon do
        for _, v in ipairs(workspace:GetDescendants()) do
            if v:IsA("Part") or v:IsA("MeshPart") then
                if v.BrickColor == BrickColor.new("Bright green") then
                    vim:SendMouseButtonEvent(0, 0, 0, true, v, 1)
                    task.wait(0.5)
                end
            end
        end
        task.wait(2)
    end
end

summonButton.MouseButton1Click:Connect(function()
    if inputBox.Text == "1" then
        autoSummon = not autoSummon
        summonButton.Text = autoSummon and "Auto Summon: ON" or "Auto Summon: OFF"
        if autoSummon then
            task.spawn(summonLoop)
        end
    else
        print("❌ Bạn phải nhập số 1 để kích hoạt Auto Summon!")
    end
end)

-- 📝 Dump Source (Lấy mã nguồn game)
dumpButton.MouseButton1Click:Connect(function()
    if inputBox.Text == "1" then
        for _, v in ipairs(getnilinstances()) do
            if v:IsA("LocalScript") or v:IsA("ModuleScript") then
                print("📝 Mã nguồn:", v:GetFullName())
                print(decompile(v))
            end
        end
    else
        print("❌ Bạn phải nhập số 1 để Dump Source!")
    end
end)
