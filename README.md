# brainrot-nonclip
Walk through walls
local Players = game:GetService("Players")
local player = Players.LocalPlayer

local function setNoclip(character, state)
	for _, part in ipairs(character:GetDescendants()) do
		if part:IsA("BasePart") then
			part.CanCollide = not state
		end
	end
end

local function onCharacterAdded(character)
	local humanoid = character:WaitForChild("Humanoid")

	character.ChildAdded:Connect(function(child)
		if child:IsA("Tool") and child.Name == "Brainrot" then
			setNoclip(character, true)
		end
	end)

	character.ChildRemoved:Connect(function(child)
		if child:IsA("Tool") and child.Name == "Brainrot" then
			setNoclip(character, false)
		end
	end)
end

if player.Character then
	onCharacterAdded(player.Character)
end

player.CharacterAdded:Connect(onCharacterAdded)
