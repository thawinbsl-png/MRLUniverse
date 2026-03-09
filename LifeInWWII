--// SERVICES
local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")

local player = Players.LocalPlayer

--// POSITIONS

local SELL = Vector3.new(-259.824921,2.47018886,-3657.97339)

local FARM_POINTS = {
    Vector3.new(-607.62085,-3.59309411,-3982.94995),
    Vector3.new(-611.602905,-3.59309411,-3887.68799),
    Vector3.new(-569.229858,-3.59309411,-3885.91699),
    Vector3.new(-527.336426,-3.59309411,-3979.59448),
    Vector3.new(-495.552612,-3.59309411,-3882.83716),
    Vector3.new(-456.17691,-3.59309411,-3976.61987)
}

--// STATE
local running = false
local farming = true

--// CHARACTER
local function getHRP()
    local char = player.Character or player.CharacterAdded:Wait()
    return char:WaitForChild("HumanoidRootPart")
end

--// TELEPORT
local function tp(pos)
    getHRP().CFrame = CFrame.new(pos)
end

--// EQUIP TOOL
local function equip(name)

    local char = player.Character or player.CharacterAdded:Wait()
    local humanoid = char:WaitForChild("Humanoid")

    for _,v in pairs(player.Backpack:GetChildren()) do
        if v:IsA("Tool") and v.Name == name then
            humanoid:EquipTool(v)
        end
    end

end

local function farmPoint(pos)

    equip("Pitchfork")

    tp(pos)
    task.wait(0.6)

end

--// AUTO PROMPT
task.spawn(function()

    while true do
        task.wait(0.1)

        if running and farming then

            local hrp = getHRP()

            for _,obj in ipairs(workspace:GetPartBoundsInRadius(hrp.Position,10)) do

                local prompt = obj:FindFirstChildOfClass("ProximityPrompt")

                if prompt and prompt.Enabled then
                    fireproximityprompt(prompt)
                end

            end

        end

    end

end)

--// MAIN LOOP
task.spawn(function()

    while true do
        task.wait(0.2)

        if running then

            farming = true

            for i,pos in ipairs(FARM_POINTS) do

                farmPoint(pos)

                -- ทุก 2 จุดให้ไปขาย
                if i % 1 == 0 then

                    tp(SELL)
                    task.wait(0.3)

                    equip("Wheat")
                    task.wait(0.1)
                    equip("Wheat")
                    task.wait(0.1)

                end

            end

            farming = false
            print("Waiting rice respawn...")

            task.wait(30)

        end

    end

end)


--// KEYBIND
UIS.InputBegan:Connect(function(input,gp)

    if gp then return end

    if input.KeyCode == Enum.KeyCode.P then
        running = not running
        print("SCRIPT:", running and "ON" or "OFF")
    end

end)
