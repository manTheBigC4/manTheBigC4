
getgenv().debounce = true
local rs = game:GetService("RunService")
local UIS = game:GetService("UserInputService")
local keybind = Enum.KeyCode.LeftControl
local Config = {
    WindowName = "Bing Chilling",
	Color = Color3.fromRGB(255,128,64),
	Keybind = Enum.KeyCode.H
}
repeat wait() until game:IsLoaded() wait()
game:GetService("Players").LocalPlayer.Idled:connect(function()
game:GetService("VirtualUser"):ClickButton2(Vector2.new())
end)

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/1201for/V.G-Hub/main/im-retarded-3"))()
getgenv().Window = Library:CreateWindow(Config, game:GetService("CoreGui"))

UIS.InputBegan:Connect(function (input,bool)
    if bool then return end
    if input.KeyCode == Enum.KeyCode.F then
        if getgenv().debounce == true then 
            getgenv().debounce = false
            getgenv().Window:Toggle(false)
        else
            getgenv().debounce = true
            getgenv().Window:Toggle(true)
        end
    end
end)

local Tab1 = getgenv().Window:CreateTab("The CraftWars")
local Tab2 = getgenv().Window:CreateTab("UI Settings")

local Section1 = Tab1:CreateSection("Test")
local Section2 = Tab1:CreateSection("")
local Section3 = Tab2:CreateSection("Menu")
local Section4 = Tab2:CreateSection("Background")


local Toggle1 = Section1:CreateToggle("IFrame",nil,function (state)
    getgenv().toggle = state
    while toggle do
        local plr = game:GetService("Players")
        plr.LocalPlayer.Character.HumanoidRootPart.CFrame = plr:FindFirstChild("LoucasTitan").Character.HumanoidRootPart.CFrame
        wait()
    end
end)

local Toggle2 = Section1:CreateToggle("Freeze(All, Ping Spiker)",nil, function (state)
    getgenv().check = state
    if getgenv().check == true then
        getgenv().fastafloop = rs.RenderStepped:Connect(function()
            for i, v in next, workspace:GetChildren() do
                if v.ClassName == "Model" and v:FindFirstChildOfClass("Humanoid") then  
            
                    local args = {
                        [1] = "inserteffect",
                        [2] = v
                    }

                    game:GetService("Players").LocalPlayer.Character:FindFirstChild("Freeze Ray").RemoteFunction:InvokeServer(unpack(args))
                end
            end
        end)
    else
        getgenv().fastafloop:Disconnect()
    end
end)


local Toggle3 = Section1:CreateToggle("Bubbles",nil,function (state)
    getgenv().bubblecheck = state
    if getgenv().bubblecheck == true then
        getgenv().realfastloop = rs.RenderStepped:Connect(function ()
            for i, v in next, workspace:GetChildren() do
                if v.ClassName == "Model" and v:FindFirstChild("Humanoid") then

                    local args = {
                        [1] = "missile",
                        [2] = {
                            [1] = 200,
                            [2] = v.Head
                        }
                    }

                    game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ocean Spellbook").RemoteFunction:InvokeServer(unpack(args))

                end
            end
        end) 
    else
        getgenv().realfastloop:Disconnect()
    end
end)

local Toggle4 = Section1:CreateToggle("Kill Others",nil,function (state)
    getgenv().Killcheck = state
    if getgenv().Killcheck == true then
        getgenv().killloop = rs.RenderStepped:Connect(function ()

            for i, v in next, workspace:GetChildren() do

                if v.ClassName == "Model" and v:FindFirstChild("Humanoid") and v.Name ~= "UnrealDirt" and v.Name ~= "LoucasTitan" then

                    local args = {
                        [1] = "hit",
                        [2] = {
                            [1] = v.Humanoid,
                            [2] = v.Humanoid.Health
                        }
                    }

                    game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice Hammer").RemoteFunction:InvokeServer(unpack(args))

                end

            end

        end)
    else
        getgenv().killloop:Disconnect()
    end
end)

local Textbox1 = Section1:CreateTextBox("Give Tool","ID(Must be a Number)",true, function(num)
    local ss = tonumber(num)
    local args = {
        [1] = {
            ["command"] = "givetool",
            ["id"] = ss
        }
    }
    
    game:GetService("ReplicatedStorage").MainControl:InvokeServer(unpack(args))    
end)
