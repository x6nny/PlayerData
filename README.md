# PlayerData
A simple to use ProfileStore wrapper!

>[!NOTE]
>README is not finished. Will add more documentation.

>[!NOTE]
>Grab the RBXM file from the Releases!

# Example usage:
```lua
local Players = game:GetService('Players')
local PlayerData = require(script.PlayerData)

local Store = PlayerData.new('Test_Store', {
	Level = 1,
	XP = 0,

	Gold = 0,
}, false, {
	['Level'] = 'Level',
	['Gold'] = 'Gold'
})


Players.PlayerAdded:Connect(function(player : Player)
	local profile = Store:WaitForProfile(player)
	
	print(`{player.Name}'s profile loaded!\nProfile: `, profile)
end)

local ROBLOXProfile = Store:GetAsync('1')
ROBLOXProfile.Data.Level = 5
ROBLOXProfile:MessageHandler(function(data_to_add)
	for key, addition in pairs(data_to_add) do
		ROBLOXProfile.Data[key] += addition
	end
        return true --> must return a boolean
end)

Store:MessageAsync('1', {['Level'] = 1})

ROBLOXProfile:EndSession()
```
