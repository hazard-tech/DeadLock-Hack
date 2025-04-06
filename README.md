local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Encrypted Hub | SW2 | FREE",
   Icon = 0,
   LoadingTitle = "Hold on..",
   LoadingSubtitle = "Made By Kryptic",
   Theme = "DarkBlue", 

   DisableRayfieldPrompts = true,
   DisableBuildWarnings = true, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "KZHUB.txt"
   },

   Discord = {
      Enabled = true, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "hF8AjBDtY6", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },

   KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "Untitled",
      Subtitle = "Key System",
      Note = "No method of obtaining the key is provided", -- Use this to tell the user how to get a key
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
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

-- Textbox for Duplication Amount
MainTab:CreateInput({
    Name = "Enter Card Dupe Amount (doesnt work Atm)",
    PlaceholderText = "10",
    RemoveTextAfterFocusLost = false,
    Flag = "DupeAmount",
    Callback = function(value)
        dupeAmount = tonumber(value) or 10
        if dupeAmount <= 0 then
            dupeAmount = 10  -- Fallback value
            StatusLabel.Text = "Invalid amount, defaulting to 10."
        end
    end
})

-- Duplication Function
local function duplicateCardsAndLaptops()
    if dupeAmount <= 0 then
        StatusLabel.Text = "Invalid amount!"
        return
    end

    StatusLabel.Text = "Buying cards & laptops..."

    -- Open Dealer UI
    fireclickdetector(game.Workspace["Streetz War"].Anonymous.ClickDetector)
    wait(2) -- Wait to ensure the UI is open
    player.PlayerGui:WaitForChild("DealerGui")
    local shopGui = player.PlayerGui.DealerGui.ShopFrame
    shopGui.Visible = true
    player.PlayerGui.DealerGui.Frame.Visible = false
    game:GetService("RunService"):Set3dRenderingEnabled(false)

    -- Position player correctly
    repeat wait() until player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    player.Character.HumanoidRootPart.CFrame = CFrame.new(-55, 4.5, 170)

    wait(0.5)

    -- Click buttons for purchasing
    local cardButton = shopGui["Blank Card"]
    local laptopButton = shopGui["laptop"]

    for i = 1, dupeAmount do
        task.wait()
        -- Click the card button
        if cardButton.Visible then
            local cardPos = cardButton.AbsolutePosition
            VirtualInputManager:SendMouseButtonEvent(cardPos.X + 150, cardPos.Y + 60, 0, true, game, 0)
            task.wait(0.1)
            VirtualInputManager:SendMouseButtonEvent(cardPos.X + 150, cardPos.Y + 60, 0, false, game, 0)
        end

        task.wait(0.1)

        -- Click the laptop button
        if laptopButton.Visible then
            local laptopPos = laptopButton.AbsolutePosition
            VirtualInputManager:SendMouseButtonEvent(laptopPos.X + 150, laptopPos.Y + 60, 0, true, game, 0)
            task.wait(0.1)
            VirtualInputManager:SendMouseButtonEvent(laptopPos.X + 150, laptopPos.Y + 60, 0, false, game, 0)
        end
    end

    game:GetService("RunService"):Set3dRenderingEnabled(true)

    -- Close the UI
    local exitButton = shopGui.exit
    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, true, game, 0)
    wait()
    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, false, game, 0)

    -- Move player to next step
    player.Character.HumanoidRootPart.CFrame = CFrame.new(954, 4.7, -61)
    wait(4)

    -- Process Laptops
    StatusLabel.Text = "Processing laptops..."
    local laptopCount = 0
    for _, v in pairs(player.Backpack:GetChildren()) do
        if v.Name == "Laptop" then
            laptopCount = laptopCount + 1
        end
    end

    for i = 1, laptopCount - 1 do
        spawn(function()
            local args = { true, "NEW123" }
            ReplicatedStorage.Assets.Other.GiverPunchmade:InvokeServer(unpack(args))
        end)
    end

    wait(4)
    player.Backpack.Laptop.Parent = player.Character
    wait(4)

    -- Process Cards
    StatusLabel.Text = "Processing cards..."
    local cardCount = 0
    for _, v in pairs(player.Backpack:GetChildren()) do
        if v.Name == "Loaded Card" then
            cardCount = cardCount + 1
        end
    end

    for i = 1, cardCount do
        spawn(function()
            local args = { false, "NEW123" }
            ReplicatedStorage.Assets.Other.GiverPunchmade:InvokeServer(unpack(args))
        end)
    end

    wait(1)
    StatusLabel.Text = "Duplication Complete!"
    player.Character.Humanoid:UnequipTools()
end

-- Button for Duplication
MainTab:CreateButton({
    Name = "Start Card Duplication",
    Callback = function()
        duplicateCardsAndLaptops()
    
        end
})

local PlayerTab = Window:CreateTab("Player", 4483362458) -- Title, Image
local PlayerSection = PlayerTab:CreateSection("Simple Hacks")

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

local Slider = PlayerTab:CreateSlider({
   Name = "JumpHeight",
   Range = {0, 300},
   Increment = 1,
   Suffix = "Height",
   CurrentValue = 16,
   Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = (Value)
   end,
})

local PlayerSection = PlayerTab:CreateSection("Button Hacks")

local Button = PlayerTab:CreateButton({
   Name = "Fly",
   Callback = function()
       loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
   end
})

local Button = PlayerTab:CreateButton({
   Name = "Infinite Jump",
   Callback = function()
 local InfiniteJumpEnabled = true
game:GetService("UserInputService").JumpRequest:connect(function()
if InfiniteJumpEnabled then
game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")
end
end)
   end,
})

local Button = PlayerTab:CreateButton({
   Name = "Infinite Yeild",
   Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Infinte-yeild-29250"))()
   end,
})

local AimbotTab = Window:CreateTab("AimBot", 4483362458) -- Title, Image
local AimbotSection = AimbotTab:CreateSection("AimBot Features")

local Button = AimbotTab:CreateButton({
   Name = "Aimbot",
   Callback = function()
   local Camera = workspace.CurrentCamera
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer
local Holding = false

_G.AimbotEnabled = true
_G.TeamCheck = false -- If set to true then the script would only lock your aim at enemy team members.
_G.AimPart = "Head" -- Where the aimbot script would lock at.
_G.Sensitivity = 0 -- How many seconds it takes for the aimbot script to officially lock onto the target's aimpart.

local function GetClosestPlayer()
	local MaximumDistance = math.huge
	local Target = nil
  
  	coroutine.wrap(function()
    		wait(20); MaximumDistance = math.huge -- Reset the MaximumDistance so that the Aimbot doesn't remember it as a very small variable and stop capturing players...
  	end)()

	for _, v in next, Players:GetPlayers() do
		if v.Name ~= LocalPlayer.Name then
			if _G.TeamCheck == true then
				if v.Team ~= LocalPlayer.Team then
					if v.Character ~= nil then
						if v.Character:FindFirstChild("HumanoidRootPart") ~= nil then
							if v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("Humanoid").Health ~= 0 then
								local ScreenPoint = Camera:WorldToScreenPoint(v.Character:WaitForChild("HumanoidRootPart", math.huge).Position)
								local VectorDistance = (Vector2.new(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y) - Vector2.new(ScreenPoint.X, ScreenPoint.Y)).Magnitude
								
								if VectorDistance < MaximumDistance then
									Target = v
                  							MaximumDistance = VectorDistance
								end
							end
						end
					end
				end
			else
				if v.Character ~= nil then
					if v.Character:FindFirstChild("HumanoidRootPart") ~= nil then
						if v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("Humanoid").Health ~= 0 then
							local ScreenPoint = Camera:WorldToScreenPoint(v.Character:WaitForChild("HumanoidRootPart", math.huge).Position)
							local VectorDistance = (Vector2.new(UserInputService:GetMouseLocation().X, UserInputService:GetMouseLocation().Y) - Vector2.new(ScreenPoint.X, ScreenPoint.Y)).Magnitude
							
							if VectorDistance < MaximumDistance then
								Target = v
               							MaximumDistance = VectorDistance
							end
						end
					end
				end
			end
		end
	end

	return Target
end

UserInputService.InputBegan:Connect(function(Input)
    if Input.UserInputType == Enum.UserInputType.MouseButton2 then
        Holding = true
    end
end)

UserInputService.InputEnded:Connect(function(Input)
    if Input.UserInputType == Enum.UserInputType.MouseButton2 then
        Holding = false
    end
end)

RunService.RenderStepped:Connect(function()
    if Holding == true and _G.AimbotEnabled == true then
        TweenService:Create(Camera, TweenInfo.new(_G.Sensitivity, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {CFrame = CFrame.new(Camera.CFrame.Position, GetClosestPlayer().Character[_G.AimPart].Position)}):Play()
    end
end)
   end,
})

local Button = AimbotTab:CreateButton({
   Name = "Silent Aim",
   Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Stefanuk12/Aiming/main/Examples/UniversalSilentAim.lua",true))()
        end
})

-- Initialize ESP Color if not set
if not espColor then
    espColor = Color3.fromRGB(255, 0, 0) -- Default to red
end

local espBoxes = {} -- Store ESP boxes for each player
local espConnection -- Store RenderStepped connection

local function createESPBox(player)
    if player == game.Players.LocalPlayer then return end -- Don't show ESP on yourself
    if espBoxes[player] then return end -- Prevent duplicate ESP boxes

    local espBox = Drawing.new("Square")
    espBox.Visible = false
    espBox.Color = espColor
    espBox.Thickness = 2
    espBox.Filled = false
    espBoxes[player] = espBox
end

local function removeESP()
    if espConnection then
        espConnection:Disconnect()
        espConnection = nil
    end
    for _, box in pairs(espBoxes) do
        box:Remove()
    end
    espBoxes = {}
end

local function updateESP()
    if not _G.espEnabled then
        removeESP()
        return
    end

    for _, player in pairs(game:GetService("Players"):GetPlayers()) do
        if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            createESPBox(player) -- Ensure ESP box exists

            local rootPart = player.Character.HumanoidRootPart
            local screenPosition, onScreen = game.Workspace.CurrentCamera:WorldToViewportPoint(rootPart.Position)

            local espBox = espBoxes[player]
            if espBox then
                if onScreen then
                    espBox.Size = Vector2.new(50, 100)
                    espBox.Position = Vector2.new(screenPosition.X - 25, screenPosition.Y - 50)
                    espBox.Color = espColor
                    espBox.Visible = true
                else
                    espBox.Visible = false
                end
            end
        elseif espBoxes[player] then
            espBoxes[player].Visible = false
        end
    end
end

local Toggle = AimbotTab:CreateToggle({
    Name = "Esp",
    CurrentValue = false,
    Flag = "ESPToggle",
    Callback = function(state)
        _G.espEnabled = state

        if _G.espEnabled then
            -- Ensure ESP exists for all players
            for _, player in pairs(game:GetService("Players"):GetPlayers()) do
                createESPBox(player)
            end

            -- Start updating ESP
            if not espConnection then
                espConnection = game:GetService("RunService").RenderStepped:Connect(updateESP)
            end
        else
            removeESP()
        end
    end
})

local ColorPicker = AimbotTab:CreateColorPicker({
    Name = "Esp Color",
    Color = espColor,
    Flag = "ESPColorPicker",
    Callback = function(color)
        espColor = color
        -- Update ESP colors dynamically
        for _, box in pairs(espBoxes) do
            box.Color = espColor
        end
    end
})

-- Ensure new players get ESP when they join
game:GetService("Players").PlayerAdded:Connect(function(player)
    if _G.espEnabled then
        task.wait(1) -- Wait a moment for character to load
        createESPBox(player)
    end
end)

-- Clean up ESP when players leave
game:GetService("Players").PlayerRemoving:Connect(function(player)
    if espBoxes[player] then
        espBoxes[player]:Remove()
        espBoxes[player] = nil
    end
end)

local GunTab = Window:CreateTab("Gun", 4483362458) -- Title, Image
local GunSection = GunTab:CreateSection("Weapon Features")

local Toggle = GunTab:CreateToggle({
    Name = "Infinite Ammo",
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

local Toggle = GunTab:CreateToggle({
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

local Toggle = GunTab:CreateToggle({
   Name = "Dupe Gun",
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

local Toggle = GunTab:CreateToggle({
   Name = "One Punch",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)

   end,
})


local Button = PlayerTab:CreateButton({
   Name = "No Clip",
   Callback = function()
                _G.noclip = v
        
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
    end
})

local Button = PlayerTab:CreateButton({
    Name = "Disable Jump Cooldown",
    Callback = function()
        local playerGui = game:GetService("Players").LocalPlayer:FindFirstChild("PlayerGui")
        if playerGui and playerGui:FindFirstChild("JumpCooldown") then
            playerGui.JumpCooldown.Enabled = false
            Rayfield:Notify({
                Title = "Success",
                Content = "Jump cooldown disabled!",
                Duration = 4,
                Image = 4483362458,
                Actions = {}
            })
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "Jump cooldown not found!",
                Duration = 4,
                Image = 4483362458,
                Actions = {}
            })
        end
    end
})

local Button = PlayerTab:CreateButton({
   Name = "Instant Prompt",
   Callback = function()
        --[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]
for i,v in ipairs(game:GetService("Workspace"):GetDescendants()) do
 if v.ClassName == "ProximityPrompt" then
  v.HoldDuration = 0
 end
end
      end
    })

local TeleportsTab = Window:CreateTab("Teleports", 4483362458) -- Title, Image

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

local QuickbuyTab = Window:CreateTab("quick buy", 4483362458) -- Title, Image
local QuickbuySection = QuickbuyTab:CreateSection("Quick Buy")

local SelectedGun

-- Dropdown menu with gun names
local Dropdown = QuickbuyTab:CreateDropdown({
    Name = "Quick Buy",
    Options = {'Sawnoff','Glock Drum','Walther PPK','Survival Knife','Revolver',
               'Mac','Tec9','Knife','ZombieKnife','Bullets','Extended','Shotgun',
               'Mag','Drum','AR-15','Vector','Thompson','Skorpion','MiniDraco',
               'Glock 17 Ext','Glock 17 switch'},
    Callback = function(Value)
        SelectedGun = Value
    end
})

-- Function to teleport and buy the gun
local function TeleportAndBuy()
    if not SelectedGun then
        Rayfield:Notify({
            Title = "Error",
            Content = "You need to select a gun first!",
            Duration = 2,
            Type = "Error"
        })
        return
    end

    -- Find the gun in the GunShop
    local gunLocation
    for _, v in pairs(game.Workspace.GunShop.Slots:GetDescendants()) do
        if v:IsA("Model") and v.Name == SelectedGun then
            gunLocation = v.Parent.MainPart
            break
        end
    end

    if not gunLocation then
        Rayfield:Notify({
            Title = "Error",
            Content = "Gun not found in shop!",
            Duration = 2,
            Type = "Error"
        })
        return
    end

    -- Save original position
    local player = game.Players.LocalPlayer
    local oldPos = player.Character.HumanoidRootPart.CFrame

    -- Teleport to the gun's location
    player.Character.HumanoidRootPart.CFrame = gunLocation.CFrame + Vector3.new(0, 2, 0)
    wait(0.2)

    -- Adjust proximity settings to ensure the purchase works
    gunLocation.ProximityPrompt.MaxActivationDistance = 10
    gunLocation.ProximityPrompt.RequiresLineOfSight = false

    -- Interact with ProximityPrompt to buy the gun
    fireproximityprompt(gunLocation.ProximityPrompt, gunLocation.ProximityPrompt.HoldDuration + 0.2)
    wait(gunLocation.ProximityPrompt.HoldDuration + 0.2)

    -- Restore original position
    player.Character.HumanoidRootPart.CFrame = oldPos

    Rayfield:Notify({
        Title = "Purchase Complete",
        Content = SelectedGun .. " has been bought!",
        Duration = 3,
        Type = "Success"
    })
end

-- Buy Button
local Button = QuickbuyTab:CreateButton({
    Name = "Buy Selected Gun",
    Callback = function()
        TeleportAndBuy()
    end
})

local SpoofTab = Window:CreateTab("Spoof", 4483362458) -- Title, Image
local SpoofSection = SpoofTab:CreateSection("Spoofer")

local Button = SpoofTab:CreateButton({
   Name = "Hide Name",
   Callback = function()
       for _, player in pairs(game.Players:GetPlayers()) do
    local character = player.Character
    if character and character:FindFirstChild("Head") then
        local nameGui = character.Head:FindFirstChild("NameGui")
        if nameGui and nameGui:FindFirstChild("Main") then
            local nameLabel = nameGui.Main:FindFirstChild("Name")
            if nameLabel then
                nameLabel.Text = "Raqrude"  -- change this with the name you want
                nameLabel.TextColor3 = Color3.fromRGB(255, 0, 0)  -- Sets the text color to red
            end
        end
    end
end
  end
    })

local Button = SpoofTab:CreateButton({
   Name = "Hide Level",
   Callback = function()
       for _, player in pairs(game.Players:GetPlayers()) do
    local character = player.Character
    if character and character:FindFirstChild("Head") then
        local nameGui = character.Head:FindFirstChild("NameGui")
        if nameGui and nameGui:FindFirstChild("Main") then
            local levelLabel = nameGui.Main:FindFirstChild("Level")
            if levelLabel then
                levelLabel.Text = "lvl 100000000000000000000"  -- This is the level changer :p
                levelLabel.TextColor3 = Color3.fromRGB(255, 0, 0)  -- Makes the text red
            end
        end
    end
end        
 end,
    
})
