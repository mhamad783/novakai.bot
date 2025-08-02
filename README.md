-- doors hack v3 - working version
print("=== DOORS HACK STARTING ===")

local plr = game.Players.LocalPlayer
local rs = game:GetService("RunService")
local uis = game:GetService("UserInputService")
local coregui = game:GetService("CoreGui")
local tweens = game:GetService("TweenService")

print("✓ Services loaded")

-- cleanup old stuff
pcall(function()
    if coregui:FindFirstChild("doorshack") then
        coregui.doorshack:Destroy()
        print("✓ Cleaned up old GUI")
    end
end)

-- vars
local espstuff = {}
local textlabels = {}
local dooresp = false
local keyesp = false
local coinesp = false
local bookesp = false
local leversp = false
local noclip = false
local god = false

-- main gui
local sg = Instance.new("ScreenGui")
sg.Name = "doorshack"
sg.ResetOnSpawn = false

-- Try CoreGui first, then PlayerGui
local parentSuccess = false
pcall(function()
    sg.Parent = coregui
    parentSuccess = true
    print("✓ GUI parented to CoreGui")
end)

if not parentSuccess then
    sg.Parent = plr.PlayerGui
    print("✓ GUI parented to PlayerGui")
end

-- check if mobile
local mobile = uis.TouchEnabled and not uis.KeyboardEnabled

-- main frame
local main = Instance.new("Frame")
main.Name = "MainFrame"
main.Size = mobile and UDim2.new(0,300,0,400) or UDim2.new(0,350,0,450)
main.Position = UDim2.new(0.5, mobile and -150 or -175, 0.5, mobile and -200 or -225)
main.BackgroundColor3 = Color3.new(0.1, 0.1, 0.15)
main.BorderSizePixel = 1
main.BorderColor3 = Color3.new(0.3, 0.3, 0.4)
main.Active = true
main.Draggable = true
main.Parent = sg

print("✓ Main frame created")

-- rounded corners
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0,8)
corner.Parent = main

-- header
local header = Instance.new("Frame")
header.Size = UDim2.new(1,0,0,50)
header.BackgroundColor3 = Color3.new(0.2, 0.1, 0.3)
header.BorderSizePixel = 0
header.Parent = main

local headercorner = Instance.new("UICorner")
headercorner.CornerRadius = UDim.new(0,8)
headercorner.Parent = header

-- fix header bottom
local headerfix = Instance.new("Frame")
headerfix.Size = UDim2.new(1,0,0,8)
headerfix.Position = UDim2.new(0,0,1,-8)
headerfix.BackgroundColor3 = Color3.new(0.2, 0.1, 0.3)
headerfix.BorderSizePixel = 0
headerfix.Parent = header

-- title
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1,-60,1,0)
title.Position = UDim2.new(0,10,0,0)
title.BackgroundTransparency = 1
title.Text = "DOORS HACK"
title.TextColor3 = Color3.new(1,1,1)
title.TextSize = 18
title.Font = Enum.Font.SourceSansBold
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = header

-- close button
local closebtn = Instance.new("TextButton")
closebtn.Size = UDim2.new(0,30,0,30)
closebtn.Position = UDim2.new(1,-40,0,10)
closebtn.BackgroundColor3 = Color3.new(0.8, 0.2, 0.2)
closebtn.BorderSizePixel = 0
closebtn.Text = "X"
closebtn.TextColor3 = Color3.new(1,1,1)
closebtn.TextSize = 16
closebtn.Font = Enum.Font.SourceSansBold
closebtn.Parent = header

local closecorner = Instance.new("UICorner")
closecorner.CornerRadius = UDim.new(0,4)
closecorner.Parent = closebtn

-- content frame
local content = Instance.new("Frame")
content.Size = UDim2.new(1,-20,1,-70)
content.Position = UDim2.new(0,10,0,60)
content.BackgroundTransparency = 1
content.Parent = main

print("✓ GUI structure created")

-- simple button maker
local function makeButton(parent, text, ypos, color, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1,0,0,35)
    btn.Position = UDim2.new(0,0,0,ypos)
    btn.BackgroundColor3 = Color3.new(0.15, 0.15, 0.2)
    btn.BorderSizePixel = 1
    btn.BorderColor3 = Color3.new(0.3, 0.3, 0.4)
    btn.Text = text .. ": OFF"
    btn.TextColor3 = Color3.new(0.8,0.8,0.8)
    btn.TextSize = 14
    btn.Font = Enum.Font.SourceSans
    btn.Parent = parent
    
    local btncorner = Instance.new("UICorner")
    btncorner.CornerRadius = UDim.new(0,4)
    btncorner.Parent = btn
    
    local enabled = false
    btn.MouseButton1Click:Connect(function()
        enabled = not enabled
        if enabled then
            btn.Text = text .. ": ON"
            btn.BackgroundColor3 = color
            btn.TextColor3 = Color3.new(1,1,1)
        else
            btn.Text = text .. ": OFF"
            btn.BackgroundColor3 = Color3.new(0.15, 0.15, 0.2)
            btn.TextColor3 = Color3.new(0.8,0.8,0.8)
        end
        callback(enabled)
        print(text, "toggled:", enabled)
    end)
    
    return btn
end

-- create buttons
local espLabel = Instance.new("TextLabel")
espLabel.Size = UDim2.new(1,0,0,25)
espLabel.BackgroundTransparency = 1
espLabel.Text = "ESP Features:"
espLabel.TextColor3 = Color3.new(0.4, 0.8, 1)
espLabel.TextSize = 16
espLabel.Font = Enum.Font.SourceSansBold
espLabel.TextXAlignment = Enum.TextXAlignment.Left
espLabel.Parent = content

makeButton(content, "Door ESP", 30, Color3.new(0, 0.8, 0.4), function(enabled)
    dooresp = enabled
end)

makeButton(content, "Key ESP", 70, Color3.new(1, 0.8, 0), function(enabled)
    keyesp = enabled
end)

makeButton(content, "Gold ESP", 110, Color3.new(1, 0.7, 0.2), function(enabled)
    coinesp = enabled
end)

makeButton(content, "Book ESP", 150, Color3.new(0.5, 0.8, 1), function(enabled)
    bookesp = enabled
end)

makeButton(content, "Lever ESP", 190, Color3.new(0.8, 0.4, 1), function(enabled)
    leversp = enabled
end)

local hackLabel = Instance.new("TextLabel")
hackLabel.Size = UDim2.new(1,0,0,25)
hackLabel.Position = UDim2.new(0,0,0,230)
hackLabel.BackgroundTransparency = 1
hackLabel.Text = "Hacks:"
hackLabel.TextColor3 = Color3.new(1, 0.6, 0.4)
hackLabel.TextSize = 16
hackLabel.Font = Enum.Font.SourceSansBold
hackLabel.TextXAlignment = Enum.TextXAlignment.Left
hackLabel.Parent = content

makeButton(content, "Noclip", 260, Color3.new(0.6, 0.4, 1), function(enabled)
    noclip = enabled
end)

makeButton(content, "Godmode", 300, Color3.new(1, 0.4, 0.4), function(enabled)
    god = enabled
end)

print("✓ Buttons created")

-- close button function
closebtn.MouseButton1Click:Connect(function()
    -- cleanup
    for _, h in pairs(espstuff) do
        pcall(function() h:Destroy() end)
    end
    for _, b in pairs(textlabels) do
        pcall(function() b:Destroy() end)
    end
    
    -- reset character
    local char = plr.Character
    if char then
        local hum = char:FindFirstChild("Humanoid")
        if hum then
            hum.MaxHealth = 100
            hum.Health = 100
        end
        
        for _, part in pairs(char:GetDescendants()) do
            if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
                part.CanCollide = true
            end
        end
    end
    
    sg:Destroy()
    print("✓ GUI closed and cleaned up")
end)

-- esp functions
local function clearESP()
    for _, h in pairs(espstuff) do
        pcall(function() h:Destroy() end)
    end
    for _, b in pairs(textlabels) do
        pcall(function() b:Destroy() end)
    end
    espstuff = {}
    textlabels = {}
end

local function addESP(obj, color, text, showText)
    if not obj or not obj.Parent then return end
    
    -- Add highlight
    local highlight = Instance.new("Highlight")
    highlight.Adornee = obj
    highlight.FillColor = color
    highlight.FillTransparency = 0.5
    highlight.OutlineColor = Color3.new(1, 1, 1)
    highlight.OutlineTransparency = 0
    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
    highlight.Parent = obj
    table.insert(espstuff, highlight)
    
    -- Add text if requested
    if showText then
        local bill = Instance.new("BillboardGui")
        bill.Adornee = obj
        bill.Size = UDim2.new(0, 100, 0, 40)
        bill.AlwaysOnTop = true
        bill.Parent = obj
        
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1, 0, 1, 0)
        label.BackgroundColor3 = Color3.new(0, 0, 0)
        label.BackgroundTransparency = 0.3
        label.BorderSizePixel = 0
        label.Text = text
        label.TextColor3 = color
        label.TextStrokeTransparency = 0
        label.TextStrokeColor3 = Color3.new(0, 0, 0)
        label.TextSize = 14
        label.Font = Enum.Font.SourceSansBold
        label.Parent = bill
        
        local labelcorner = Instance.new("UICorner")
        labelcorner.CornerRadius = UDim.new(0, 4)
        labelcorner.Parent = label
        
        table.insert(textlabels, bill)
    end
end

-- door detection (simplified)
local function isDoorLocked(door, doorFolder)
    -- Check common lock indicators
    if door:GetAttribute("Locked") or doorFolder:GetAttribute("Locked") then
        return true
    end
    
    -- Check for lock objects
    if doorFolder:FindFirstChild("Lock") or door:FindFirstChild("Lock") then
        return true
    end
    
    -- Default to unlocked if we can't determine
    return false
end

-- esp scanning
local function scanForESP()
    if not (dooresp or keyesp or coinesp or bookesp or leversp) then return end
    
    clearESP()
    
    local rooms = workspace:FindFirstChild("CurrentRooms")
    if not rooms then 
        print("No CurrentRooms found")
        return 
    end
    
    for _, room in pairs(rooms:GetChildren()) do
        if tonumber(room.Name) then
            
            -- Door ESP
            if dooresp then
                local doorFolder = room:FindFirstChild("Door")
                if doorFolder then
                    local door = doorFolder:FindFirstChild("Door")
                    if door then
                        local locked = isDoorLocked(door, doorFolder)
                        if locked then
                            addESP(door, Color3.new(1, 0.3, 0.3), "LOCKED", true)
                        else
                            addESP(door, Color3.new(0, 1, 0.4), "DOOR", false)
                        end
                    end
                end
            end
            
            -- Key ESP
            if keyesp then
                local assets = room:FindFirstChild("Assets")
                if assets then
                    for _, obj in pairs(assets:GetDescendants()) do
                        if obj.Name:lower():find("key") and obj:IsA("BasePart") then
                            addESP(obj, Color3.new(1, 0.9, 0), "KEY", true)
                        end
                    end
                end
            end
            
            -- Gold ESP
            if coinesp then
                local assets = room:FindFirstChild("Assets")
                if assets then
                    for _, obj in pairs(assets:GetChildren()) do
                        if obj.Name:lower():find("gold") or obj.Name:lower():find("coin") then
                            addESP(obj, Color3.new(1, 0.8, 0.2), "GOLD", true)
                        end
                    end
                end
            end
            
            -- Book ESP
            if bookesp then
                local assets = room:FindFirstChild("Assets")
                if assets then
                    for _, obj in pairs(assets:GetChildren()) do
                        if obj.Name:lower():find("book") then
                            addESP(obj, Color3.new(0.5, 0.8, 1), "BOOK", true)
                        end
                    end
                end
            end
            
            -- Lever ESP
            if leversp then
                local assets = room:FindFirstChild("Assets")
                if assets then
                    for _, obj in pairs(assets:GetChildren()) do
                        if obj.Name:lower():find("lever") then
                            addESP(obj, Color3.new(0.8, 0.4, 1), "LEVER", true)
                        end
                    end
                end
            end
        end
    end
end

-- main loop
local lastScan = 0
rs.Heartbeat:Connect(function()
    local now = tick()
    
    -- Scan for ESP every 2 seconds
    if now - lastScan > 2 then
        pcall(scanForESP)
        lastScan = now
    end
    
    local char = plr.Character
    if not char then return end
    
    -- Noclip
    if noclip then
        for _, part in pairs(char:GetDescendants()) do
            if part:IsA("BasePart") and part.CanCollide and part.Name ~= "HumanoidRootPart" then
                part.CanCollide = false
            end
        end
    end
    
    -- Godmode
    if god then
        local hum = char:FindFirstChild("Humanoid")
        if hum and hum.Health < hum.MaxHealth then
            hum.Health = hum.MaxHealth
        end
    end
end)

print("✓ Main loop started")
print("=== DOORS HACK LOADED SUCCESSFULLY ===")
print("Look for a dark GUI with DOORS HACK title!")
