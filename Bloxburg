local Config = {
    WindowName = "V.G Hub",
    Color = Color3.fromRGB(255, 128, 64),
    Keybind = Enum.KeyCode.RightControl
}
repeat
    wait()
until game:IsLoaded()
wait()
game:GetService("Players").LocalPlayer.Idled:connect(
    function()
        game:GetService("VirtualUser"):ClickButton2(Vector2.new())
    end
)
local Name = "BloxBurg.json"

Des = {}
if makefolder then
    makefolder("V.G Hub")
end
local Games = {4491408735, 185655149}
if not table.find(Games, game.PlaceId) then
    return
end
local Settings

if
    not pcall(
        function()
            readfile("V.G Hub//" .. Name)
        end
    )
 then
    writefile("V.G Hub//" .. Name, game:GetService("HttpService"):JSONEncode(Des))
end

Settings = game:GetService("HttpService"):JSONDecode(readfile("V.G Hub//" .. Name))

local function Save()
    writefile("V.G Hub//" .. Name, game:GetService("HttpService"):JSONEncode(Settings))
end

-- Wait for game to load

local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")

local wait = task.wait
local spawn = task.spawn
local Player = Players.LocalPlayer
local St = ReplicatedStorage.Stats[Player.Name]
local Workstations = Workspace.Environment.Locations
local Da = require(ReplicatedStorage.Modules.DataService)

local Jo = require(Player.PlayerScripts.Modules.JobHandler)

local PathfindingService = game:GetService("PathfindingService")
local Gamei = Workspace["_game"]

local Fire = function(A)
    local O = getfenv(Da.FireServer).i
    getfenv(Da.FireServer).i = function()
    end
    Da:FireServer(A)
    getfenv(Da.FireServer).i = O
end
local Invoke = function(A)
    local O = getfenv(Da.InvokeServer).i
    getfenv(Da.InvokeServer).i = function()
    end
    Da:InvokeServer(A)
    getfenv(Da.InvokeServer).i = O
end
local Invis = function()
    local Clone = Player.Character.LowerTorso.Root:Clone()
    Player.Character.LowerTorso.Root:Destroy()
    Clone.Parent = Player.Character.LowerTorso
end
local F = {}
getgenv().Text = Drawing.new("Text")
Text.Color = Color3.new(0, 1, 1)
Text.Font = 1
Text.Outline = true
Text.OutlineColor = Color3.new(0, 0, 0)
Text.Position = Vector2.new(30, Workspace.CurrentCamera.ViewportSize.Y - 100)
Text.Size = 25
Text.Text = ""
Text.Visible = true

Workspace.CurrentCamera:GetPropertyChangedSignal("ViewportSize"):Connect(
    function()
        Text.Position = Vector2.new(20, Workspace.CurrentCamera.ViewportSize.Y - 100)
    end
)
local Events = {"MouseButton1Down", "MouseButton1Click", "Activated"}
local Click = function()
    for i, v in pairs(Events) do
        for i, v in pairs(getconnections(Player.PlayerGui.MainGUI.InteractIndicator[v])) do
            v:Fire()
        end
        for i, v in pairs(getconnections(Player.PlayerGui.MainGUI.InteractIndicator.TapButton[v])) do
            v:Fire()
        end
    end
end
local Order = function(A)
    if not A or (A and not A:FindFirstChild("Order")) then
        return
    end
    if St.Job.Value == "StylezHairdresser" then
        local B = A.Order:WaitForChild("Style").Value
        local C = A.Order:WaitForChild("Color").Value
        return {B, C}
    elseif St.Job.Value == "BloxyBurgersCashier" then
        local D = A.Order:WaitForChild("Burger").Value
        local F = A.Order:WaitForChild("Fries").Value
        local G = A.Order:WaitForChild("Cola").Value
        return {D, F, G}
    end
end
local function Tween(A, B, C)
    if A then
        local Time = (B - A.Position).magnitude / C
        local Info = TweenInfo.new(Time, Enum.EasingStyle.Linear)
        local Tween = game:GetService("TweenService"):Create(A, Info, {CFrame = CFrame.new(B)})
        Tween:Play()
    end
end
Player.PlayerGui.DescendantAdded:Connect(
    function(v)
        if v.Name == "MessageBox" then
            v:WaitForChild("Event"):Fire()
        end
    end
)

local PathService = game:GetService("PathfindingService")
local path = PathfindingService:CreatePath()

local function TweenTo(i, v)
    if
        game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") and
            game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").SeatPart
     then
        game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").Sit = false
        wait(.1)
    end
    s = true
    repeat
        wait()
        local success, response =
            pcall(
            function()
                path:ComputeAsync(i.Position, v)
                local waypoints = path:GetWaypoints()
                local distance
                for waypointIndex, waypoint in pairs(waypoints) do
                    local waypointPosition = waypoint.Position
                    Tween(i, waypointPosition, 15)
                    repeat
                        distance = (waypointPosition - i.PrimaryPart.Position).magnitude
                        wait()
                    until distance <= 10
                end
            end
        )
        if not success then
            Tween(i, v, 15)
        end
    until (v - i.Position).magnitude < 10 or s == false
end

local function WalkTo(v)
    if
        game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") and
            game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").SeatPart
     then
        game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").Sit = false
        wait(.1)
    end
    s = true
    repeat
        wait()
        local success, response =
            pcall(
            function()
                path:ComputeAsync(game.Players.LocalPlayer.Character.HumanoidRootPart.Position, v)
                local waypoints = path:GetWaypoints()
                local distance
                for waypointIndex, waypoint in pairs(waypoints) do
                    local waypointPosition = waypoint.Position
                    game.Players.LocalPlayer.Character.Humanoid:MoveTo(waypointPosition)
                    repeat
                        distance =
                            (waypointPosition -
                            game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").Parent.PrimaryPart.Position).magnitude
                        wait()
                    until distance <= 10
                end
            end
        )
        if not success then
            game.Players.LocalPlayer.Character.Humanoid:MoveTo(v.Position)
        end
    until (v - game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid").Parent.PrimaryPart.Position).magnitude <
        10 or s == false
end

local function getNearestCleaner()
    local TargetDistance = math.huge
    local Target
    for i, v in pairs(Gamei.SpawnedCharacters:GetChildren()) do
        if
            v:FindFirstChildWhichIsA("BasePart") and v.Name == "WallSpawn" or
                v:FindFirstChildWhichIsA("Model") and v.Name == "GroundSpawn"
         then
            local Mag = (v.Position - Player.Character.HumanoidRootPart.Position).Magnitude
            if Mag < TargetDistance then
                TargetDistance = Mag
                Target = v
            end
        end
    end
    return Target
end

function lookAt(A, B)
    local Straight = (B - A).Unit
    local Up = Vector3.new(0, 1, 0)
    local Right = Straight:Cross(Up)
    local Up2 = Right:Cross(Straight)

    return CFrame.fromMatrix(B, Right, Up2)
end
local function getNearestTree()
    local TargetDistance = math.huge
    local Target
    for i, v in pairs(game:GetService("Workspace").Environment.Trees:GetChildren()) do
        if
            v:IsA("Model") and v:FindFirstChildWhichIsA("BasePart") and
                v:FindFirstChildWhichIsA("BasePart").Position.Y > 0
         then
            local Mag = (v:GetModelCFrame().Position - Player.Character.HumanoidRootPart.Position).Magnitude
            if Mag < TargetDistance then
                TargetDistance = Mag
                Target = v
            end
        end
    end
    return Target
end

for i, v in pairs(getconnections(game:GetService("ScriptContext").Error)) do
    v:Disable()
    game:GetService("ScriptContext").Error:Connect(
        function(...)
            local Args = {...}
            local i, v =
                pcall(
                function()
                    return Args[3].Name
                end
            )
            if i == false then
                return
            end
            v:Fire(...)
        end
    )
end

local function getNearestMine()
    local TargetDistance = math.huge
    local Target
    for i, v in pairs(Workspace.Environment.Locations["Static_MinerCave"].Folder:GetChildren()) do
        if
            v:IsA("Model") and v:FindFirstChildWhichIsA("BasePart") and
                v:FindFirstChildWhichIsA("BasePart").BrickColor.Name ~= "Bright red"
         then
            local Mag = (v:GetModelCFrame().Position - Player.Character.HumanoidRootPart.Position).Magnitude
            if Mag < TargetDistance then
                TargetDistance = Mag
                Target = v
            end
        elseif
            v:IsA("Model") and v:FindFirstChildWhichIsA("BasePart") and
                v:FindFirstChildWhichIsA("BasePart").BrickColor.Name == "Bright red"
         then
            v:Destroy()
        end
    end
    return Target
end
spawn(
    function()
        while wait() do
            pcall(
                function()
                    if Settings.PizzaPlanetBaker then
                        if (St.Job.Value ~= "PizzaPlanetBaker") then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("PizzaPlanetBaker") --> TP to job
                        end

                        repeat
                            wait()
                        until St.Job.Value == "PizzaPlanetBaker"

                        for i, v in pairs(
                            game:GetService("Workspace").Environment.Locations.PizzaPlanet.BakerWorkstations:GetChildren(

                            )
                        ) do
                            if v.Name == "Workstation" then
                                local Workstation = v
                                if Workstation.Order.IngredientsLeft.Value < 1 then
                                    Tween(
                                        Player.Character.HumanoidRootPart,
                                        game:GetService("Workspace").Environment.Locations.PizzaPlanet.IngredientCrates:FindFirstChild(
                                            "Crate"
                                        ).Position,
                                        15
                                    )
                                    repeat
                                        wait()
                                    until Player:DistanceFromCharacter(
                                        game:GetService("Workspace").Environment.Locations.PizzaPlanet.IngredientCrates:FindFirstChild(
                                            "Crate"
                                        ).Position
                                    ) < 5
                                    while not Player.Character:FindFirstChild("Ingredient Crate") do
                                        Fire(
                                            {
                                                Type = "TakeIngredientCrate",
                                                Object = game:GetService("Workspace").Environment.Locations.PizzaPlanet.IngredientCrates:FindFirstChild(
                                            "Crate"
                                        )
                                            }
                                        )
                                        wait(1)
                                    end
                                    Tween(Player.Character.HumanoidRootPart, Workstation.PrimaryPart.Position, 15)
                                    while Player.Character:FindFirstChild("Ingredient Crate") do
                                        Fire(
                                            {
                                                Type = "RestockIngredients",
                                                Workstation = Workstation
                                            }
                                        )
                                        wait(1)
                                    end
                                    return
                                end

                                    Tween(Player.Character.HumanoidRootPart, Workstation.PrimaryPart.Position, 15)
                                    wait()
                                    repeat
                                        wait()
                                    until Player:DistanceFromCharacter(Workstation.PrimaryPart.Position) < 5
                                    Fire({
								Type = "UseWorkstation", 
								Workstation = Workstation
							});
                                    if Workstation.OrderDisplay.DisplayMain:FindFirstChild("BakerGUI") and wait(2) then
                                        Fire(
                                            {
                                                Type = "JobCompleted",
                                                Workstation = Workstation,
                                                Order = {true,true,true,Workstation.Order.Value}
                                            }
                                        )
                                    end
                                    if
                                        tonumber(
                                            Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                                        ) >= 1000
                                     then
                                        Jo:StopWorking()
                                        Text.Text = "Status: Quiting"
                                        wait(10)
                                    end
                            end
                        end
                    end

                    if Settings.MikesMechanic then
                        if (St.Job.Value ~= "MikesMechanic") then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("MikesMechanic") --> TP to job
                        end

                        repeat
                            wait()
                        until St.Job.Value == "MikesMechanic"

                        for a, b in pairs(workspace["_game"].SpawnedCharacters:GetChildren()) do
                            if b.Name == "MikesMotorsCustomer" then
                                if not b:FindFirstChild("HumanoidRootPart") then
                                    return
                                end
                                if b:FindFirstChild("HumanoidRootPart"):FindFirstChild("AttachWeld") then
                                    local c = b:WaitForChild("HumanoidRootPart"):FindFirstChild("AttachWeld")
                                    if c.Part1 then
                                        if c.Part1.Name == "CustomerTarget" and c.Part1.Parent.Name == "Workstation" then
                                            local d = b
                                            local e = c.Part1.Parent
                                            if Player:DistanceFromCharacter(e.PrimaryPart.Position) < 15 then
                                                if d:FindFirstChildOfClass("CFrameValue") then
                                                    return
                                                end
                                                Instance.new("CFrameValue", d)
                                                local f = d:WaitForChild("Order")
                                                local g = f.Vehicle.Value
                                                local h
                                                if f:FindFirstChild("Color") then
                                                    h = "Color"
                                                elseif f:FindFirstChild("Wheels") then
                                                    h = "Wheels"
                                                elseif f:FindFirstChild("Oil") then
                                                    h = "Oil"
                                                end
                                                if h == "Color" then
                                                    local i = f.Color.Value
                                                    local j =
                                                        workspace.Environment.Locations.MikesMotors.PaintingEquipment:FindFirstChild(
                                                        i
                                                    )
                                                    Tween(Player.Character.HumanoidRootPart, j.Can.Position, 15)
                                                    wait(2)
                                                    while not Player.Character:FindFirstChild("Spray Painter") do
                                                        Fire({Type = "TakePainter", Object = j})
                                                        wait()
                                                    end
                                                    Tween(
                                                        Player.Character.HumanoidRootPart,
                                                        d.Vehicle.Body.Position,
                                                        15
                                                    )
                                                    wait(2)
                                                    while Player.Character:FindFirstChild("Spray Painter") do
                                                        Fire({Type = "FixBike", Workstation = e})
                                                        wait()
                                                    end
                                                    Fire({Type = "JobCompleted", Workstation = e})
                                                elseif h == "Wheels" then
                                                    local k = f.Wheels.Value
                                                    local l =
                                                        workspace.Environment.Locations.MikesMotors.TireRacks:FindFirstChild(
                                                        k
                                                    )
                                                    Tween(Player.Character.HumanoidRootPart, l.Part.Position, 15)
                                                    wait(2)
                                                    while not Player.Character:FindFirstChild("Motorcycle Wheel") do
                                                        Fire({Type = "TakeWheel", Object = l})
                                                        wait()
                                                    end
                                                    Tween(
                                                        Player.Character.HumanoidRootPart,
                                                        d.Vehicle.Body.Position,
                                                        15
                                                    )
                                                    wait(2)
                                                    while Player.Character:FindFirstChild("Motorcycle Wheel") do
                                                        Fire({Type = "FixBike", Workstation = e})
                                                        wait()
                                                    end
                                                    Tween(Player.Character.HumanoidRootPart, l.Part.Position, 15)
                                                    wait(2)
                                                    while not Player.Character:FindFirstChild("Motorcycle Wheel") do
                                                        Fire({Type = "TakeWheel", Object = l})
                                                        wait()
                                                    end
                                                    Tween(
                                                        Player.Character.HumanoidRootPart,
                                                        d.Vehicle.Body.Position,
                                                        15
                                                    )
                                                    wait(2)
                                                    while Player.Character:FindFirstChild("Motorcycle Wheel") do
                                                        Fire({Type = "FixBike", Workstation = e, Front = true})
                                                        wait()
                                                    end
                                                    Fire({Type = "JobCompleted", Workstation = e})
                                                elseif h == "Oil" then
                                                    local m =
                                                        workspace.Environment.Locations.MikesMotors.OilCans:FindFirstChild(
                                                        "Can"
                                                    )
                                                    Tween(Player.Character.HumanoidRootPart, m.Body.Position, 15)
                                                    wait(2)
                                                    while not Player.Character:FindFirstChild("Oil Can") do
                                                        Fire({Type = "TakeOil", Object = m})
                                                        wait()
                                                    end
                                                    Tween(
                                                        Player.Character.HumanoidRootPart,
                                                        d.Vehicle.Body.Position,
                                                        15
                                                    )
                                                    wait(2)
                                                    while Player.Character:FindFirstChild("Oil Can") do
                                                        Fire({Type = "FixBike", Workstation = e})
                                                        wait()
                                                    end
                                                    Fire({Type = "JobCompleted", Workstation = e})
                                                end
                                            end
                                        end
                                        if
                                            tonumber(
                                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                                            ) >= 1000
                                         then
                                            Tween(Player.Character.HumanoidRootPart, Vector3.new(409, 8, 815), 15)
                                            Jo:StopWorking()
                                            Text.Text = "Status: Quiting"
                                            wait(10)
                                        end
                                    end
                                end
                            end
                        end
                    end
                    if Settings.CaveMiner then
                        if (St.Job.Value ~= "CaveMiner") then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("CaveMiner") --> TP to job
                        end

                        repeat
                            wait()
                        until St.Job.Value == "CaveMiner"
                        if getNearestMine() then
                            Tween(
                                Player.Character.HumanoidRootPart,
                                getNearestMine():GetModelCFrame().Position + Vector3.new(0, 5, 0),
                                15
                            )
                            Workspace.Camera.CFrame =
                                CFrame.new(
                                350.404419,
                                20.3447189,
                                783.925537,
                                1,
                                2.76919254e-05,
                                -4.8828133e-06,
                                0,
                                0.173647493,
                                0.984807909,
                                2.81191133e-05,
                                -0.984807909,
                                0.173647493
                            )
                            wait(1)
                            Text.Text = "Status: Mining"
                            Click()
                        end
                        if
                            tonumber(
                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                            ) >= 1000
                         then
                            Tween(Player.Character.HumanoidRootPart, Vector3.new(409, 8, 815), 15)
                            Jo:StopWorking()
                            Text.Text = "Status: Quiting"
                            wait(10)
                        end
                    end
                    if Settings.LumberWoodcutter then
                        if (St.Job.Value ~= "LumberWoodcutter") and wait(2) then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("LumberWoodcutter") --> TP to job
                            Tween(Player.Character.HumanoidRootPart, Vector3.new(631, 14, 818), 15)
                            Tween(Player.Character.HumanoidRootPart, Vector3.new(614, 15, 822), 15)
                        end

                        repeat
                            wait()
                        until St.Job.Value == "LumberWoodcutter" and Player.Character:FindFirstChild("Hatchet") and
                            wait(1)
                        if getNearestTree() and Player.Character:FindFirstChild("Hatchet") then
                            Tween(
                                Player.Character.HumanoidRootPart,
                                getNearestTree():GetModelCFrame().Position + Vector3.new(0, 0, 3),
                                15
                            )
                            wait(1)
                            if
                                (Player.Character.HumanoidRootPart.Position - getNearestTree():GetModelCFrame().Position).Magnitude <
                                    15
                             then
                                Text.Text = "Status: Choping"
                                Fire(
                                    {
                                        Tree = getNearestTree(),
                                        Type = "UseHatchet"
                                    }
                                )
                            end
                        end
                        if
                            tonumber(
                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                            ) >= 1000
                         then
                            Jo:StopWorking()
                            Text.Text = "Status: Quiting"
                            wait(10)
                        end
                    end

                    if Settings.Stylish then
                        if (St.Job.Value ~= "StylezHairdresser") then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("StylezHairdresser") --> TP to job
                        end

                        repeat
                            wait()
                        until St.Job.Value == "StylezHairdresser"
                        for i, v in pairs(
                            Workspace.Environment.Locations.StylezHairStudio.HairdresserWorkstations:GetChildren()
                        ) do
                            if v.InUse.Value == nil or v.InUse.Value == Player.Name then
                                Player.Character:WaitForChild("Humanoid"):MoveTo(v.Stool:GetModelCFrame().Position)
                                Text.Text = "Status: WalkingToPoint"
                            end
                            Fire(
                                {
                                    Type = "FinishOrder",
                                    Workstation = v,
                                    Order = Order(v.Occupied.Value)
                                }
                            )
                        end
                        Text.Text = "Status: Bypassing"
                        wait(math.random(5, 10))
                        Text.Text = "Status: Done"
                        wait(1)
                        if
                            tonumber(
                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                            ) >= 1000
                         then
                            Jo:StopWorking()
                            Text.Text = "Status: Quiting"
                            wait(10)
                        end
                    end
                    if Settings.SupermarketStocker then
                        if (St.Job.Value ~= "SupermarketStocker") then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("SupermarketStocker") --> TP to job
                        end

                        repeat
                            wait()
                        until St.Job.Value == "SupermarketStocker"
                        for i, v in pairs(
                            game:GetService("Workspace").Environment.Locations.Supermarket.Crates:GetChildren()
                        ) do
                            if
                                not Player.Character:FindFirstChild("Food Crate") and
                                    not v:FindFirstChildWhichIsA("Decal")
                             then
                                Text.Text = "Status: Grabbing Crate"

                                repeat
                                    wait()
                                    TweenTo(Player.Character.HumanoidRootPart, v.Position)
                                until (Player.Character.HumanoidRootPart.Position - v.Position).magnitude <= 10 or
                                    Player.Character:FindFirstChild("Food Crate") or
                                    not Settings.SupermarketStocker and wait(1)
                                Fire(
                                    {
                                        Type = "TakeFoodCrate",
                                        Object = v
                                    }
                                )
                                wait(1)
                            end
                        end
                        for i, v in pairs(
                            game:GetService("Workspace").Environment.Locations.Supermarket.Shelves:GetChildren()
                        ) do
                            if
                                v:FindFirstChild("IsEmpty") and v.IsEmpty.Value == true and
                                    Player.Character:FindFirstChild("Food Crate")
                             then
                                Text.Text = "Status: Going to Said Empty Slot"
                                repeat
                                    wait()
                                    TweenTo(Player.Character.HumanoidRootPart, v:GetModelCFrame().Position)
                                until (Player.Character.HumanoidRootPart.Position - v:GetModelCFrame().Position).magnitude <=
                                    10 and wait(2)
                                Fire(
                                    {
                                        Type = "RestockShelf",
                                        Shelf = v
                                    }
                                )
                                wait(1)
                            end
                        end
                        if
                            tonumber(
                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                            ) >= 1000
                         then
                            Jo:StopWorking()
                            Text.Text = "Status: Quiting"
                            wait(10)
                        end
                    end
                    if Settings.Burger then
                        if (St.Job.Value ~= "BloxyBurgersCashier") then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("BloxyBurgersCashier") --> TP to job
                        end

                        repeat
                            wait()
                        until St.Job.Value == "BloxyBurgersCashier"
                        for i, v in pairs(
                            game:GetService("Workspace").Environment.Locations.BloxyBurgers.CashierWorkstations:GetChildren(

                            )
                        ) do
                            if v.InUse.Value == nil or v.InUse.Value == Player.Name then
                                Text.Text = "Status: WalkingToPoint"
                                Player.Character:WaitForChild("Humanoid"):MoveTo(
                                    v.OrderDisplay:GetModelCFrame().Position
                                )
                            end
                            Fire(
                                {
                                    Type = "FinishOrder",
                                    Workstation = v,
                                    Order = Order(v.Occupied.Value)
                                }
                            )
                        end
                        Text.Text = "Status: Bypassing"
                        wait(math.random(5, 10))
                        Text.Text = "Status: Done"
                        wait(1)
                        if
                            tonumber(
                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                            ) >= 1000
                         then
                            Jo:StopWorking()
                            Text.Text = "Status: Quiting"
                            wait(10)
                        end
                    end
                    if Settings.SupermarketCashier then
                        if (St.Job.Value ~= "SupermarketCashier") then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("SupermarketCashier") --> TP to job
                        end

                        repeat
                            wait()
                        until St.Job.Value == "SupermarketCashier" or wait(10)
                        for i, v in pairs(Workspace.Environment.Locations.Supermarket.CashierWorkstations:GetChildren()) do
                            if v.Name == "Workstation" then
                                if v.Occupied.Value == nil then
                                    return
                                end
                                local A = v.Occupied.Value
                                if Player:DistanceFromCharacter(v.PrimaryPart.Position) < 8 then
                                    local Weld = A:WaitForChild("HumanoidRootPart"):WaitForChild("Motor6D")
                                    local Scanned = 0
                                    while (Weld.Part1.Name == "CustomerTarget_1") and Weld.Parent do
                                        wait(2)
                                        if v.BagsLeft.Value < 1 then
                                            TweenTo(
                                                Player.Character.HumanoidRootPart,
                                                Workspace.Environment.Locations.Supermarket.Crates:FindFirstChild(
                                                    "BagCrate"
                                                ).Position
                                            )
                                            Text.Text = "Status: Restocking Bags"
                                            while not Player.Character:FindFirstChild("BFF Bags") do
                                                Fire(
                                                    {
                                                        Type = "TakeNewBags",
                                                        Object = Workspace.Environment.Locations.Supermarket.Crates:FindFirstChild(
                                                            "BagCrate"
                                                        )
                                                    }
                                                )
                                                wait(1)
                                            end
                                            TweenTo(Player.Character.HumanoidRootPart, v.PrimaryPart.Position)
                                            while Player.Character:FindFirstChild("BFF Bags") do
                                                Fire(
                                                    {
                                                        Type = "RestockBags",
                                                        Workstation = v
                                                    }
                                                )
                                                Text.Text = "Status: RestockedBags"
                                                wait(1)
                                            end
                                        end
                                        repeat
                                            wait()
                                            if v.DroppedFood:FindFirstChildWhichIsA("BasePart") then
                                                if Scanned == 3 then
                                                    Scanned = 0
                                                    Fire(
                                                        {
                                                            Type = "TakeNewBag",
                                                            Workstation = v
                                                        }
                                                    )
                                                    Text.Text = "Status: NewBag"
                                                    wait(1)
                                                end

                                                Fire(
                                                    {
                                                        Type = "ScanDroppedItem",
                                                        Item = v.DroppedFood:FindFirstChildWhichIsA("BasePart")
                                                    }
                                                )
                                                Text.Text = "Status: Scanned item" .. " " .. Scanned
                                                Scanned = Scanned + 1
                                                wait(1)
                                            end
                                        until not v.DroppedFood:FindFirstChildWhichIsA("BasePart") and wait(1) or
                                            v.BagsLeft.Value < 1
                                        if not v.DroppedFood:FindFirstChildWhichIsA("BasePart") then
                                            wait(2)
                                            Fire(
                                                {
                                                    Type = "JobCompleted",
                                                    Workstation = v
                                                }
                                            )
                                        end
                                        if
                                            tonumber(
                                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                                            ) >= 1000
                                         then
                                            Jo:StopWorking()
                                            Text.Text = "Status: Quiting"
                                            wait(10)
                                        end
                                    end
                                end
                            end
                        end
                        wait(1)
                    end
                    if Settings.CleanJanitor then
                        if St.Job.Value ~= "CleanJanitor" then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("CleanJanitor")
                        end
                        repeat
                            wait()
                        until St.Job.Value == "CleanJanitor"

                        for i, v in pairs(Workspace.Environment.Locations.GreenClean.Spawns:GetChildren()) do
                            if v:FindFirstChild("Object") then
                                table.insert(F, v)
                            end
                        end
                        table.sort(
                            F,
                            function(A, B)
                                return Player:DistanceFromCharacter(A.Position) <
                                    Player:DistanceFromCharacter(B.Position)
                            end
                        )
                        Text.Text = "Status: Fucking around"
                        if #F > 1 then
                            local A = F[1]
                            local P
                            if A:FindFirstChild("Object"):IsA("Part") then
                                P = A:FindFirstChild("Object").CFrame.Position + Vector3.new(0, 5, 0)
                            else
                                P = A:FindFirstChild("Object").PrimaryPart.CFrame.Position + Vector3.new(0, 5, 0)
                            end
                            Text.Text = "Status: Tweening to Object"
                            TweenTo(Player.Character.HumanoidRootPart, P)
                            wait(3)
                            Invoke(
                                {
                                    Type = "CleanJanitorObject",
                                    Spawn = A
                                }
                            )
                            Text.Text = "Status: Rember to give DekuDimz#3809 free hentai when you see him!"
                        end
                        if
                            tonumber(
                                Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                            ) >= 1000
                         then
                            Jo:StopWorking()
                            Text.Text = "Status: Quiting"
                            wait(10)
                        end
                    end

                    if Settings.BensIceCreamSeller then
                        if St.Job.Value ~= "BensIceCreamSeller" then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("BensIceCreamSeller")
                        end
                        repeat
                            wait()
                        until St.Job.Value == "BensIceCreamSeller"
                        for i, v in pairs(Gamei.SpawnedCharacters:GetChildren()) do
                            if v.Name == "BensIceCreamCustomer" then
                                if not v:FindFirstChild("HumanoidRootPart") then
                                    return
                                end
                                if v:FindFirstChild("HumanoidRootPart"):FindFirstChild("Motor6D") then
                                    if v:WaitForChild("HumanoidRootPart"):FindFirstChild("Motor6D").Part1 then
                                        if
                                            (v:WaitForChild("HumanoidRootPart"):FindFirstChild("Motor6D").Part1.Name ==
                                                "CustomerTarget")
                                         then
                                            Text.Text = "Status: Repeat"
                                            local Order = v:FindFirstChild("Order")
                                            if not Order then
                                                return
                                            end
                                            if v:FindFirstChildOfClass("CFrameValue") then
                                                return
                                            end
                                            Instance.new("CFrameValue", v)
                                            Player.Character.Humanoid:MoveTo(
                                                Vector3.new(
                                                    929.095337,
                                                    13.7269897,
                                                    1049.63477,
                                                    -0.842953146,
                                                    1.25050681e-08,
                                                    0.537986934,
                                                    3.88757222e-08,
                                                    1,
                                                    3.7668844e-08,
                                                    -0.537986934,
                                                    5.26677013e-08,
                                                    -0.842953146
                                                )
                                            )
                                            Player.Character.Humanoid.MoveToFinished:Wait()
                                            Fire(
                                                {
                                                    Type = "TakeIceCreamCup"
                                                }
                                            )
                                            Text.Text = "Took Cup Bypassing"
                                            while not Player.Character:FindFirstChild("Ice Cream Cup") do
                                                wait(2)
                                            end
                                            Fire(
                                                {
                                                    Ball = Player.Character:FindFirstChild("Ice Cream Cup"):WaitForChild(
                                                        "Ball1"
                                                    ),
                                                    Type = "AddIceCreamScoop",
                                                    Taste = Order:FindFirstChild("Flavor1").Value
                                                }
                                            )
                                            Text.Text = "Status: Topping 1 added"
                                            wait(1)
                                            Fire(
                                                {
                                                    Ball = Player.Character:FindFirstChild("Ice Cream Cup"):WaitForChild(
                                                        "Ball2"
                                                    ),
                                                    Type = "AddIceCreamScoop",
                                                    Taste = Order:FindFirstChild("Flavor2").Value
                                                }
                                            )
                                            Text.Text = "Status: Topping 2 added"
                                            wait(1)
                                            Fire(
                                                {
                                                    Type = "AddIceCreamTopping",
                                                    Taste = Order:FindFirstChild("Topping").Value
                                                }
                                            )
                                            Player.Character.Humanoid:MoveTo(
                                                v:WaitForChild("HumanoidRootPart").Position + Vector3.new(0, 0, 0)
                                            )
                                            Text.Text = "Status: Moving to retard"
                                            Player.Character.Humanoid.MoveToFinished:Wait()
                                            wait()
                                            Fire(
                                                {
                                                    Type = "JobCompleted",
                                                    Workstation = v:WaitForChild("HumanoidRootPart"):FindFirstChild(
                                                        "Motor6D"
                                                    ).Part1
                                                }
                                            )
                                            Text.Text = "Done"
                                            wait(2)
                                            if
                                                tonumber(
                                                    Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                                                ) >= 1000
                                             then
                                                Jo:StopWorking()
                                                Text.Text = "Status: Quiting"
                                                wait(10)
                                            end
                                        end
                                    end
                                end
                            end
                        end
                    end
                    if Settings.PizzaPlanetDelivery then
                        if St.Job.Value ~= "PizzaPlanetDelivery" then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("PizzaPlanetDelivery")
                        end
                        repeat
                            wait()
                        until St.Job.Value == "PizzaPlanetDelivery"
                        if
                            not Player.Character:FindFirstChild("Pizza Box") and
                                not Player.Character:FindFirstChild("Vehicle_Delivery Moped")
                         then
                            Tween(Player.Character.HumanoidRootPart, Vector3.new(1176, 14, 284), 15)
                            Text.Text = "Status: Getting Moped"
                            if (Player.Character.HumanoidRootPart.Position - Vector3.new(1176, 14, 284)).magnitude < 5 then
                                Click()
                                Text.Text = "Status: Click"
                            end
                        end
                        if
                            Player.Character:FindFirstChild("Vehicle_Delivery Moped") and
                                not Player.Character:FindFirstChild("Pizza Box")
                         then
                            Tween(
                                Player.Character:FindFirstChild("Vehicle_Delivery Moped").Body,
                                Vector3.new(1166, 15, 272),
                                20
                            )
                            Text.Text = "Status:  Getting Pizza!"
                            if (Player.Character.HumanoidRootPart.Position - Vector3.new(1166, 15, 272)).magnitude < 5 then
                                Workspace.Camera.CFrame =
                                    CFrame.new(
                                    1165.80823,
                                    17.5511112,
                                    286.201172,
                                    0.999919415,
                                    -0.000955291034,
                                    0.012666015,
                                    -5.82076748e-11,
                                    0.997167885,
                                    0.0752079785,
                                    -0.012701991,
                                    -0.0752019212,
                                    0.997087359
                                )
                                Click()
                                Text.Text = "Status: Click"
                            end
                        end
                        if
                            Player.Character:FindFirstChild("Pizza Box") and
                                Player.Character:FindFirstChild("Vehicle_Delivery Moped")
                         then
                            local P
                            if Gamei.SpawnedCharacters:FindFirstChild("PizzaPlanetDeliveryCustomer") then
                                P =
                                    Gamei.SpawnedCharacters:FindFirstChild("PizzaPlanetDeliveryCustomer"):GetModelCFrame(

                                ).Position.Y
                            else
                                P = 15
                            end
                            Text.Text = "Status: Tweening to Retard"
                            Tween(
                                Player.Character:FindFirstChild("Vehicle_Delivery Moped").Body,
                                Vector3.new(
                                    game:GetService("Workspace").MouseIgnore.DeliveryArrow.Position.X,
                                    P,
                                    game:GetService("Workspace").MouseIgnore.DeliveryArrow.Position.Z
                                ),
                                20
                            )
                            if
                                (Player.Character.HumanoidRootPart.Position -
                                    Gamei.SpawnedCharacters:FindFirstChild("PizzaPlanetDeliveryCustomer"):GetModelCFrame(

                                    ).Position).magnitude < 5
                             then
                                Click()
                                Text.Text = "Status: Click"
                            end
                            if
                                tonumber(
                                    Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                                ) >= 5000
                             then
                                Jo:StopWorking()
                                Text.Text = "Status: Quiting"
                                wait(10)
                            end
                        end
                    end
                    if Settings.HutFisherman then
                        if St.Job.Value ~= "HutFisherman" then
                            Text.Text = "Status: Teleporting"
                            Jo:GoToWork("HutFisherman")
                        end
                        repeat
                            wait()
                        until St.Job.Value == "HutFisherman"
                        if Player.Character:FindFirstChild("Fishing Rod") then
                            local Done = false
                            spawn(
                                function()
                                    repeat
                                        wait()
                                        Text.Text = "Status: Waiting For Fishing Rod"
                                        if not Player.Character:FindFirstChild("Fishing Rod") then
                                            break
                                        end
                                    until Player.Character:FindFirstChild("Fishing Rod"):FindFirstChild("Bobber").CFrame.Y <
                                        6
                                    Done = true
                                end
                            )
                            Player.Character.Humanoid:MoveTo(Vector3.new(1053, 10, 1099))
                            local time = tick()
                            Text.Text = "Status: Waiting for Fish"
                            Fire(
                                {
                                    State = true,
                                    Type = "UseFishingRod",
                                    Pos = Vector3.new(1032, 6, 1107)
                                }
                            )
                            repeat
                                wait()
                            until Done
                            Text.Text = "Status: Catching Fish"
                            Fire(
                                {
                                    State = false,
                                    Type = "UseFishingRod",
                                    Time = tick() - time
                                }
                            )
                            if
                                tonumber(
                                    Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text
                                ) >= 1000
                             then
                                Jo:StopWorking()
                                Text.Text = "Status: Quiting"
                                wait(10)
                            end
                        end
                    end
                    Text.Text = ""
                end
            )
        end
    end
)

spawn(
    function()
        while wait() do
            wait()
            pcall(
                function()
                    Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text =
                        string.gsub(
                        Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text,
                        "$ ",
                        ""
                    )
                    Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text =
                        string.gsub(
                        Player.PlayerGui.MainGUI.Bar.CharMenu.WorkFrame.WorkFrame.EarningsLabel.TextLabel.Text,
                        " ",
                        ""
                    )
                end
            )
        end
    end
)


local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/1201for/V.G-Hub/main/test"))()
local Window = Library:CreateWindow(Config, game:GetService("CoreGui"))

local Tab1 = Window:CreateTab("Anime Rifts")
local Tab2 = Window:CreateTab("UI Settings")

local Section1 = Tab1:CreateSection("")
local Section2 = Tab1:CreateSection("")
local Section3 = Tab2:CreateSection("Menu")
local Section4 = Tab2:CreateSection("Background")


local Toggle1 = Section1:CreateToggle("StylezHairdresser", Settings.Stylish, function(State)
    Settings.Stylish = State 
end)

local Toggle1 = Section1:CreateToggle("BloxyBurgersCashier", Settings.Burger, function(State)
    Settings.Burger = State 
end)
local Toggle1 = Section1:CreateToggle("CaveMiner", Settings.CaveMiner, function(State)
    Settings.CaveMiner = State 
end)


local Toggle1 = Section1:CreateToggle("BensIceCreamSeller", Settings.BensIceCreamSeller, function(State)
    Settings.BensIceCreamSeller = State 
end)


local Toggle1 = Section1:CreateToggle("PizzaPlanetBaker", Settings.PizzaPlanetBaker, function(State)
    Settings.PizzaPlanetBaker = State 
    RunService.Stepped:connect(function()
        if Settings.PizzaPlanetBaker then
            for i,v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end 
            end 
        end 
    end)
end)


local Toggle1 = Section1:CreateToggle("Invis", Settings.Invis, function(State)
Settings.Invis = State
spawn(function()
    while wait() and Settings.Invis do 
        Invis()
        wait(3)
    end 
end)
end)
local Toggle1 = Section1:CreateToggle("LumberWoodcutter", Settings.LumberWoodcutter, function(State)
    Settings.LumberWoodcutter = State 
    RunService.Stepped:connect(function()
        if Settings.LumberWoodcutter then
            for i,v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                    v.Velocity = Vector3.new(0,0,0)
                end 
            end 
        end 
    end)
end)



local Toggle1 = Section1:CreateToggle("CleanJanitor", Settings.CleanJanitor, function(State)
    Settings.CleanJanitor = State 
    RunService.Stepped:connect(function()
        if Settings.CleanJanitor then
            for i,v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end 
            end 
        end 
    end)
end)

local Toggle1 = Section1:CreateToggle("MikesMechanic", Settings.MikesMechanic, function(State)
    Settings.MikesMechanic = State 
    RunService.Stepped:connect(function()
        if Settings.MikesMechanic then
            for i,v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end 
            end 
        end 
    end)
end)



local Toggle1 = Section1:CreateToggle("HutFisherman", Settings.HutFisherman, function(State)
    Settings.HutFisherman = State 
    RunService.Stepped:connect(function()
        if Settings.HutFisherman then
            for i,v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end 
            end 
        end 
    end)
end)
local Toggle1 = Section1:CreateToggle("SupermarketCashier", Settings.SupermarketCashier, function(State)
    Settings.SupermarketCashier = State
    RunService.Stepped:connect(function()
        if Settings.SupermarketCashier then
            for i,v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end 
            end 
        end 
    end)
end)

local Toggle1 = Section1:CreateToggle("SupermarketStocker", Settings.SupermarketStocker, function(State)
    Settings.SupermarketStocker = State 
    RunService.Stepped:connect(function()
        if Settings.SupermarketStocker then
            for i,v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                end 
            end 
        end 
    end)
end)

local Toggle1 = Section1:CreateToggle("PizzaPlanetDelivery", Settings.PizzaPlanetDelivery, function(State)
    Settings.PizzaPlanetDelivery = State 
    RunService.Stepped:connect(function()
        if Settings.PizzaPlanetDelivery then
            for i,v in pairs(Player.Character:GetDescendants()) do
                if v:IsA("BasePart") then
                    v.CanCollide = false
                    v.Velocity = Vector3.new(0,0,0)
                end 
            end 
        end 
    end)
end)


local ESP = loadstring(game:HttpGet("https://raw.githubusercontent.com/1201for/V.G-Hub/main/Karrot-Esp"))()

local Toggle1 = Section1:CreateToggle("Enable Esp", Settings.Esp, function(State)
    Settings.Esp = State
    ESP:Toggle(Settings.Esp)
end)

local Toggle1 = Section1:CreateToggle("Player Esp", Settings.PlayerEsp, function(State)
    Settings.PlayerEsp = State
    ESP.Players = Settings.PlayerEsp
end)
local Toggle1 = Section1:CreateToggle("Tracers Esp", Settings.Tracers, function(State)
    Settings.Tracers = State
    ESP.Tracers = Settings.Tracers
end)
local Toggle1 = Section1:CreateToggle("Name Esp", Settings.EspNames, function(State)
    ESP.Names = Settings.EspNames
    Settings.EspNames = State
end)
local Toggle1 = Section1:CreateToggle("Boxes Esp", Settings.Boxes, function(State)
    Settings.Boxes = State
    ESP.Boxes = Settings.Boxes
end)

local Toggle1 = Section2:CreateToggle("Invisicam", Settings.Sorry, function(State)
Settings.Sorry = State
if Settings.Sorry then
    Player.DevCameraOcclusionMode = "Invisicam"
else
    Player.DevCameraOcclusionMode = "Zoom"
end
end)

local Toggle1 = Section2:CreateToggle("N Noclip", Settings.Sex1, function(State)
noclips = false
Settings.Sex1 = State
Player:GetMouse().KeyDown:connect(
    function(v)
        if v == "n" then
            if Settings.Sex1 then
                noclips = not noclips
                for i, v in pairs(Player.Character:GetChildren()) do
                    if v:IsA("BasePart") then
                        pcall(function()
                        v.CanCollide = false
                        end)
                    end
                end
            end
        end
    end
)
RunService.Stepped:connect(
    function()
        if noclips then
            for i, v in pairs(Player.Character:GetChildren()) do
                if v:IsA("BasePart") then
                    pcall(function()
                    v.CanCollide = false
                    end)
                end
            end
        end
    end
)

end)

local Toggle1 = Section2:CreateToggle("G Noclip", Settings.Sex, function(State)
Settings.Sex = State
noclip = false
RunService.Stepped:connect(
    function()
        if noclip then
            Player.Character:FindFirstChildWhichIsA("Humanoid"):ChangeState(11)
        end
    end
)
mouse = Player:GetMouse()
Player:GetMouse().KeyDown:connect(
    function(v)
        if v == "g" then
            if Settings.Sex then
                noclip = not noclip
                Player.Character:FindFirstChildWhichIsA("Humanoid"):ChangeState(11)
            end
        end
    end
)
end)

local Button1 = Section2:CreateButton("Anti Lag", function()
for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
    if v:IsA("BasePart") and not v.Parent:FindFirstChild("Humanoid") then
        v.Material = Enum.Material.SmoothPlastic
        if v:IsA("Texture") then
            v:Destroy()
        end
    end
end
end)

local Button1 = Section2:CreateButton("Lag Switch F3", function()
local ass = false
local bitch = settings()

game:GetService("UserInputService").InputEnded:connect(
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
                wait(getgenv().delay2)
                pcall(function()
                    writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                    wait(getgenv().delay2)
                    game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, Player)
                end)
                wait(4)
            end
        end
    end
end

function Teleport()
    while wait(getgenv().delay2) do
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
game:GetService("TeleportService"):Teleport(game.PlaceId, Player) end)



local Toggle3 = Section3:CreateToggle("UI Toggle", nil, function(State)
	Window:Toggle(State)
end)
Toggle3:CreateKeybind(tostring(Config.Keybind):gsub("Enum.KeyCode.", ""), function(Key)
	Config.Keybind = Enum.KeyCode[Key]
end)
Toggle3:SetState(true)
Section3:CreateLabel("Credits DekuDimz#7960")
Section3:CreateLabel("Credits AlexR32#3232 Ui")
Section3:CreateLabel("Credits inverevt")
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
spawn(function()
while wait() do
Save()
end end)
