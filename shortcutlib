local ShortcutLib = {}

function ShortcutLib.newshortcut()
	local screenGui = Instance.new("ScreenGui")
	screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

	local frame = Instance.new("Frame")
	frame.Size = UDim2.new(0.5, 0, 0.5, 0)
	frame.AnchorPoint = Vector2.new(1, 0)
	frame.Position = UDim2.new(1, 0, 0, 0)
	frame.BackgroundTransparency = 1
	frame.Parent = screenGui

	local uiListLayout = Instance.new("UIListLayout")
	uiListLayout.Parent = frame

	local lib = {}

	function lib:NewShortcut(Name, IsEnabled, Call)
		local button = Instance.new("TextButton")
		button.Size = UDim2.new(0, 45, 0, 45)
		button.BackgroundTransparency = 1
		button.Text = ""
		button.Parent = frame

		local uiCorner = Instance.new("UICorner")
		uiCorner.CornerRadius = UDim.new(1, 0)
		uiCorner.Parent = button

		local uiStroke = Instance.new("UIStroke")
		uiStroke.Color = IsEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 0, 0)
		uiStroke.Parent = button

		local dragging = false
		local dragStart
		local startPos

		local function updateDrag(input)
			if dragging then
				local delta = input.Position - dragStart
				button.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
			end
		end

		local function onInputBegan(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				dragStart = input.Position
				startPos = button.Position
				dragging = false
				wait(1.5)
				if dragStart then
					dragging = true
				end
			end
		end

		local function onInputChanged(input)
			if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
				updateDrag(input)
			end
		end

		local function onInputEnded(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				dragging = false
			end
		end

		button.InputBegan:Connect(onInputBegan)
		button.InputChanged:Connect(onInputChanged)
		button.InputEnded:Connect(onInputEnded)

		button.MouseButton1Click:Connect(function()
			IsEnabled = not IsEnabled
			uiStroke.Color = IsEnabled and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 0, 0)
			pcall(Call, IsEnabled)
		end)
	end
	
	return lib
end

return ShortcutLib
