local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait() -- Ensure character is loaded
local backpack = player:WaitForChild("Backpack") -- Player's inventory
local workspace = game.Workspace

-- Function to "collect" a tool
local function collectTool(tool)
    if tool:IsA("Tool") then
        print("Collecting tool: " .. tool.Name)
        tool.Parent = backpack -- Move the tool to the player's inventory
    end
end

-- Listen for tools spawning in the workspace
workspace.ChildAdded:Connect(function(child)
    if child:IsA("Tool") then
        collectTool(child)
    end
end)

-- Optionally, check for existing tools in the workspace when the script starts
for _, child in ipairs(workspace:GetChildren()) do
    if child:IsA("Tool") then
        collectTool(child)
    end
end
