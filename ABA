local Config = {
    WindowName = "V.G Hub",
	Color = Color3.fromRGB(255,128,64),
	Keybind = Enum.KeyCode.RightControl
}
repeat wait() until game:IsLoaded() wait()
game:GetService("Players").LocalPlayer.Idled:connect(function()
game:GetService("VirtualUser"):ClickButton2(Vector2.new())
end)

for i, v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
    if v:IsA("RemoteFunction") then
        local OldNameCall = nil
        OldNameCall =
            hookmetamethod(
            game,
            "__namecall",
            function(self, ...)
                local Args = {...}
                if self.Name == v.Name then
                    return nil
                end
                return OldNameCall(self, unpack(Args))
            end
        )
    end
end


local Circle = Drawing.new("Circle")
Circle.Color =  Color3.fromRGB(22, 13, 56)
Circle.Thickness = 1
Circle.Radius = 250
Circle.Visible = false
Circle.NumSides = 1000
Circle.Filled = false
Circle.Transparency = 1

game:GetService("RunService").RenderStepped:Connect(function()
    local Mouse = game:GetService("UserInputService"):GetMouseLocation()
    Circle.Position = Vector2.new(Mouse.X, Mouse.Y)
end)

getgenv().AimBot = {
FreeForAll= false,
WallCheck = false,
Enabled = false,
FOV = 250,
}
local Shoot = false

function FreeForAll(v)
    if getgenv().AimBot.FreeForAll == false or getgenv().TriggerBot.FreeForAll == false then
        if game.Players.LocalPlayer.Team == v.Team then return false
        else return true end
    else return true end
end

function NotObstructing(i, v)
    if getgenv().AimBot.WallCheck then
        c = workspace.CurrentCamera.CFrame.p
        a = Ray.new(c, i- c)
        f = workspace:FindPartOnRayWithIgnoreList(a, v)
        return f == nil
    else
        return true
    end
end
game:GetService("UserInputService").InputBegan:Connect(function(v)
    if v.UserInputType == Enum.UserInputType.MouseButton2 then
        Shoot = true
    end
end)

game:GetService("UserInputService").InputEnded:Connect(function(v)
    if v.UserInputType == Enum.UserInputType.MouseButton2 then
        Shoot = false
    end
end)


function GetClosestToCuror()
    Closest = math.huge
    Target = nil
    for _,v in pairs(game:GetService("Players"):GetPlayers()) do
        if FreeForAll(v) then
            if v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("HumanoidRootPart") and v.Character:FindFirstChild("Humanoid") and v.Character.Humanoid.Health ~= 0  then
                Point,OnScreen = workspace.CurrentCamera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
                if OnScreen and NotObstructing(v.Character.HumanoidRootPart.Position,{game.Players.LocalPlayer.Character,v.Character}) then
                    Distance = (Vector2.new(Point.X,Point.Y) - Vector2.new(game.Players.LocalPlayer:GetMouse().X, game.Players.LocalPlayer:GetMouse().Y)).magnitude
                      if Distance <= getgenv().AimBot.FOV then
                          Closest = Distance
                       Target = v
                     end
                  end
               end
            end
         end
    return Target
end 

game:GetService('RunService').Stepped:connect(function()
pcall(function()
    if getgenv().AimBot.Enabled == false or Shoot == false then return end
    ClosestPlayer = GetClosestToCuror()
    if ClosestPlayer then
     workspace.CurrentCamera.CFrame = CFrame.new(workspace.CurrentCamera.CFrame.p,ClosestPlayer.Character[getgenv().AimPart].CFrame.p)
    end 
end)
end)
getgenv().TriggerBot = {
   TeamCheck = false;
   Delay = 0.01;
   Enabled = false;
}

local Aim = false
game:GetService("UserInputService").InputBegan:connect(function(v)
   if v.UserInputType  == Enum.UserInputType.MouseButton2 and getgenv().TriggerBot.Enabled then
       Aim = true
       while Aim do wait()
           if game:GetService("Players").LocalPlayer:GetMouse().Target and game:GetService("Players"):FindFirstChild(game:GetService("Players").LocalPlayer:GetMouse().Target.Parent.Name) then
            local Person = game:GetService("Players"):FindFirstChild(game:GetService("Players").LocalPlayer:GetMouse().Target.Parent.Name)
               if Person.Team ~= game:GetService("Players").LocalPlayer.Team or not getgenv().TriggerBot.TeamCheck then
                   if getgenv().TriggerBot.Delay > 0 then wait(getgenv().TriggerBot.Delay) end
                   mouse1press(); wait(); mouse1release()
               end
           end
           if not getgenv().TriggerBot.Enabled then break end
       end
   end
end)

game:GetService("UserInputService").InputEnded:connect(function(v)
   if v.KeyCode == Enum.UserInputType.MouseButton2 and getgenv().TriggerBot.Enabled then
       Aim = false
   end
end)

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/1201for/V.G-Hub/main/test"))()
local Window = Library:CreateWindow(Config, game:GetService("CoreGui"))

local Tab1 = Window:CreateTab("ANIME BATTLE ARENA")
local Tab2 = Window:CreateTab("UI Settings")

local Section1 = Tab1:CreateSection("")
local Section2 = Tab1:CreateSection("")
local Section5 = Tab1:CreateSection("")
local Section3 = Tab2:CreateSection("Menu")
local Section4 = Tab2:CreateSection("Background")

local Toggle1 = Section1:CreateToggle("Aimbot", nil, function(State)
    getgenv().AimBot.Enabled = State
end)


local Dropdown1 = Section1:CreateDropdown("HitPart", {"HumanoidRootPart","Head","UpperTorso","LowerTorso","Random"}, function(String)
	getgenv().AimPart = String
end)
Dropdown1:AddToolTip("Select AimPart")
Dropdown1:SetOption("HumanoidRootPart")


local Toggle1 = Section1:CreateToggle("FreeForAll", nil, function(State)
    getgenv().AimBot.FreeForAll = State
    getgenv().TriggerBot.TeamCheck = State
end)

local Toggle1 = Section1:CreateToggle("TriggerBot", nil, function(State)
    getgenv().TriggerBot.Enabled = State
end)

local Toggle1 = Section1:CreateToggle("WallCheck", nil, function(State)
    getgenv().AimBot.WallCheck = State
end)

local Slider2 = Section1:CreateSlider("Aimbot Radius", 0,1000,nil,false, function(Value)
    getgenv().AimBot.FOV = Value
    Circle.Radius = Value
end)

local Toggle1 = Section1:CreateToggle("Circle Visible", nil, function(State)
   Circle.Visible = State
end)

local Colorpicker3 = Section1:CreateColorpicker("Circle Color", function(Color)
    Circle.Color = Color
end)


local Toggle1 = Section1:CreateToggle("SilentAim", nil, function(State)
getgenv().Player = State

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
function ClosestPlayerToCurser()
    local MaxDistance, Closest = math.huge
    for i, v in pairs(Players.GetPlayers(Players)) do
        if v ~= LocalPlayer and v.Character then
            local H = v.Character.FindFirstChild(v.Character, "Head")
            if H then
                local Pos, Vis = workspace.CurrentCamera.WorldToScreenPoint(workspace.CurrentCamera, H.Position)
                if Vis then
                    local A1, A2 = Vector2.new(Mouse.X, Mouse.Y), Vector2.new(Pos.X, Pos.Y)
                    local Dist = (A2 - A1).Magnitude
                    if Dist < MaxDistance and Dist <= math.huge then
                        MaxDistance = Dist
                        Closest = v
                    end
                end
            end
        end
    end
    return Closest
end


local OldIndex = nil
OldIndex =
    hookmetamethod(
    game,
    "__index",
    function(self, v, ...)
        if self == Mouse and (v == "Hit" or v == "Target") then
            if ClosestPlayerToCurser() and getgenv().Player then
                return ((v == "Hit" and ((ClosestPlayerToCurser().Character.Head.CFrame) or (ClosestPlayerToCurser().Character.Head.CFrame + (ClosestPlayerToCurser().Character.Head.Velocity)))) or
                    (v == "Target" and ClosestPlayerToCurser().Character.Head))
            end
        end

        return OldIndex(self, v)
    end
)end)




local ESP = loadstring(game:HttpGet("https://raw.githubusercontent.com/1201for/V.G-Hub/main/Karrot-Esp"))()

local Toggle1 = Section1:CreateToggle("Player Esp", nil, function(State)
ESP:Toggle(State)
end)

local Toggle1 = Section1:CreateToggle("Tracers Esp", nil, function(State)
ESP.Tracers = State
end)

local Toggle1 = Section1:CreateToggle("Name Esp", nil, function(State)
ESP.Names = State
end)

local Toggle1 = Section1:CreateToggle("Boxes Esp", nil, function(State)
ESP.Boxes = State
end)


local Toggle1 = Section1:CreateToggle("BHop", nil, function(State)
BHop = State
while wait() and BHop do
    game.Players.LocalPlayer.Character.Humanoid.Jump = true
end
end)

local Button1 = Section2:CreateButton("Lag Switch F3", function()
local ass = false
local bitch = settings()

game:service "UserInputService".InputEnded:connect(
    function(i)
        if i.KeyCode == Enum.KeyCode.F3 then
            ass = not ass
            bitch.Network.IncomingReplicationLag = ass and 10 or 0
        end
    end
)
 end) 
local Button1 = Section2:CreateButton("ServerHop", function()
local PlaceID = game.PlaceId
local AllIDs = {}
local foundAnything = ""
local actualHour = os.date("!*t").hour
local Deleted = false
local File = pcall(function()
    AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
end)
if not File then
    table.insert(AllIDs, actualHour)
    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
end
function TPReturner()
    local Site;
    if foundAnything == "" then
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
    else
        Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
    end
    local ID = ""
    if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
        foundAnything = Site.nextPageCursor
    end
    local num = 0;
    for i,v in pairs(Site.data) do
        local Possible = true
        ID = tostring(v.id)
        if tonumber(v.maxPlayers) > tonumber(v.playing) then
            for _,Existing in pairs(AllIDs) do
                if num ~= 0 then
                    if ID == tostring(Existing) then
                        Possible = false
                    end
                else
                    if tonumber(actualHour) ~= tonumber(Existing) then
                        local delFile = pcall(function()
                            delfile("NotSameServers.json")
                            AllIDs = {}
                            table.insert(AllIDs, actualHour)
                        end)
                    end
                end
                num = num + 1
            end
            if Possible == true then
                table.insert(AllIDs, ID)
                wait()
                pcall(function()
                    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                    wait()
                    game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
                end)
                wait(4)
            end
        end
    end
end

function Teleport()
    while wait() do
        pcall(function()
            TPReturner()
            if foundAnything ~= "" then
                TPReturner()
            end
        end)
    end
end

-- If you'd like to use a script before server hopping (Like a Automatic Chest collector you can put the Teleport() after it collected everything.
Teleport() 
end)
local Button1 = Section2:CreateButton("Rejoin", function()
game:GetService("TeleportService"):Teleport(game.PlaceId, game:GetService("Players").LocalPlayer) end)




local Toggle3 = Section3:CreateToggle("UI Toggle", nil, function(State)
	Window:Toggle(State)
end)
Toggle3:CreateKeybind(tostring(Config.Keybind):gsub("Enum.KeyCode.", ""), function(Key)
	Config.Keybind = Enum.KeyCode[Key]
end)
Toggle3:SetState(true)
Section3:CreateLabel("Credits DekuDimz#7960")
Section3:CreateLabel("Credits AlexR32#3232 Ui")
Section3:CreateLabel("Credits The3Bakers")
local Colorpicker3 = Section3:CreateColorpicker("UI Color", function(Color)
	Window:ChangeColor(Color)
end)
Colorpicker3:UpdateColor(Config.Color)

-- credits to jan for patterns
local Dropdown3 = Section4:CreateDropdown("Image", {"Default","Hearts","Abstract","Hexagon","Circles","Lace With Flowers","Floral"}, function(Name)
	if Name == "Default" then
		Window:SetBackground("2151741365")
	elseif Name == "Hearts" then
		Window:SetBackground("6073763717")
	elseif Name == "Abstract" then
		Window:SetBackground("6073743871")
	elseif Name == "Hexagon" then
		Window:SetBackground("6073628839")
	elseif Name == "Circles" then
		Window:SetBackground("6071579801")
	elseif Name == "Lace With Flowers" then
		Window:SetBackground("6071575925")
	elseif Name == "Floral" then
		Window:SetBackground("5553946656")
	end
end)
Dropdown3:SetOption("Default")

local Colorpicker4 = Section4:CreateColorpicker("Color", function(Color)
	Window:SetBackgroundColor(Color)
end)
Colorpicker4:UpdateColor(Color3.new(1,1,1))

local Slider3 = Section4:CreateSlider("Transparency",0,1,nil,false, function(Value)
	Window:SetBackgroundTransparency(Value)
end)
Slider3:SetValue(0)

local Slider4 = Section4:CreateSlider("Tile Scale",0,1,nil,false, function(Value)
	Window:SetTileScale(Value)
end)
Slider4:SetValue(0.5)
