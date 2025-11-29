--[[
    UFO HUB X • Màn hình tải (Việt Nam 🇻🇳)
    - Hình nền: 130548594326307
    - Tiêu đề "Trung tâm UFO HUB X" hiện từng ký tự ~4 giây
      (Tất cả màu trắng, riêng "HUB X" màu xanh lá)
    - Thanh tải 0 → 100% trong 5 giây
    - Cờ 🇻🇳 lớn hơn thanh, dính ở đầu thanh màu xanh
    - Khi tải xong mọi thứ mờ dần rồi biến mất
]]

local Players      = game:GetService("Players")
local CoreGui      = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")

-- Xóa màn hình cũ nếuมีอยู่ trước đó
local OLD = CoreGui:FindFirstChild("UFOX_DownloadScreen")
if OLD then OLD:Destroy() end

local gui = Instance.new("ScreenGui")
gui.Name = "UFOX_DownloadScreen"
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false
gui.ZIndexBehavior = Enum.ZIndexBehavior.Global
gui.Parent = CoreGui

-- Hình nền full màn
local bg = Instance.new("ImageLabel")
bg.Parent = gui
bg.Size = UDim2.fromScale(1,1)
bg.Position = UDim2.fromScale(0.5,0.5)
bg.AnchorPoint = Vector2.new(0.5,0.5)
bg.BackgroundTransparency = 1
bg.Image = "rbxassetid://130548594326307"
bg.ScaleType = Enum.ScaleType.Crop
bg.ImageTransparency = 0

---------------------------------------------------------------------
-- Tiêu đề "Trung tâm UFO HUB X"
-- Base = trắngทั้งหมด, riêng "HUB X" = xanh lá
-- Hiện từng ký tự trong ~4 giây
---------------------------------------------------------------------
local title = Instance.new("TextLabel")
title.Parent = gui
title.AnchorPoint = Vector2.new(0.5,0.5)
title.Position = UDim2.new(0.5,0,0.32,0)
title.Size = UDim2.new(0.8,0,0,90)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBlack
title.RichText = true
title.TextScaled = true
title.TextColor3 = Color3.new(1,1,1) -- ✅ ให้ base เป็นสีขาว
title.TextStrokeColor3 = Color3.new(0,0,0)
title.TextStrokeTransparency = 0
title.Text = ""

local fullText = "Trung tâm UFO HUB X"
local totalTime = 4
local steps = #fullText
local stepDelay = totalTime / steps

task.spawn(function()
    for i = 1, steps do
        local partial = fullText:sub(1, i)
        local rich = partial

        -- หา substring "HUB X" ในข้อความที่แสดงตอนนี้ แล้วทำให้เป็นสีเขียว
        local s, e = string.find(partial, "HUB X")
        if s then
            local before = partial:sub(1, s - 1)
            local hubx  = partial:sub(s, e)
            local after = partial:sub(e + 1)

            rich = string.format(
                '%s<font color="rgb(25,255,125)">%s</font>%s',
                before, hubx, after
            )
        end

        title.Text = rich
        task.wait(stepDelay)
    end
end)

---------------------------------------------------------------------
-- Khung thanh tải
---------------------------------------------------------------------
local barHolder = Instance.new("Frame")
barHolder.Parent = gui
barHolder.AnchorPoint = Vector2.new(0.5,0.5)
barHolder.Position = UDim2.new(0.5,0,0.55,0)
barHolder.Size = UDim2.new(0.65,0,0,42)
barHolder.BackgroundColor3 = Color3.new(0,0,0)
barHolder.BackgroundTransparency = 0.25
barHolder.ClipsDescendants = false

local corner = Instance.new("UICorner", barHolder)
corner.CornerRadius = UDim.new(0,16)

local stroke = Instance.new("UIStroke", barHolder)
stroke.Thickness = 2
stroke.Color = Color3.new(0,0,0)

-- Thanh màu xanh (progress)
local fill = Instance.new("Frame")
fill.Parent = barHolder
fill.AnchorPoint = Vector2.new(0,0.5)
fill.Position = UDim2.new(0,3,0.5,0)
fill.Size = UDim2.new(0,-6,1,-8)
fill.BackgroundColor3 = Color3.fromRGB(25,255,125)
fill.BackgroundTransparency = 0
fill.ClipsDescendants = false

local fillCorner = Instance.new("UICorner", fill)
fillCorner.CornerRadius = UDim.new(0,14)

-- Cờ Việt Nam 🇻🇳 lớn hơn thanh, dính ở đầu thanh
local flag = Instance.new("TextLabel")
flag.Parent = fill
flag.BackgroundTransparency = 1
flag.AnchorPoint = Vector2.new(0.5,0.5)
flag.Position = UDim2.new(1, 24, 0.5, 0)
flag.Size = UDim2.new(0, 70, 0, 70)
flag.Font = Enum.Font.GothamBold
flag.TextScaled = true
flag.Text = "🇻🇳"
flag.ZIndex = 20

-- Chữ đang tải (tiếng Việt)
local label = Instance.new("TextLabel")
label.Parent = barHolder
label.BackgroundTransparency = 1
label.Size = UDim2.new(1,0,1,0)
label.Font = Enum.Font.GothamBold
label.TextColor3 = Color3.new(1,1,1)
label.TextStrokeColor3 = Color3.new(0,0,0)
label.TextStrokeTransparency = 0
label.TextScaled = false
label.TextSize = 20
label.Text = "Đang tải 0%"
label.ZIndex = 30

---------------------------------------------------------------------
-- Tải 0 → 100 rồi fade out
---------------------------------------------------------------------
local duration = 5
local delayStep = duration / 100

task.spawn(function()
    for i = 0,100 do
        local alpha = i / 100
        fill.Size = UDim2.new(alpha, -6, 1, -8)
        label.Text = ("Đang tải %d%%"):format(i)
        task.wait(delayStep)
    end

    local fade = 0.6
    TweenService:Create(bg, TweenInfo.new(fade), {ImageTransparency = 1}):Play()
    TweenService:Create(title, TweenInfo.new(fade), {TextTransparency = 1}):Play()
    TweenService:Create(label, TweenInfo.new(fade), {TextTransparency = 1}):Play()
    TweenService:Create(barHolder, TweenInfo.new(fade), {BackgroundTransparency = 1}):Play()
    TweenService:Create(fill, TweenInfo.new(fade), {BackgroundTransparency = 1}):Play()

    task.wait(fade + 0.2)
    gui:Destroy()
end)
