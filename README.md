pcall(function()
	if game.CoreGui.FummyKawaii then
		game.CoreGui.FummyKawaii:Destroy()
	end
end)
local MAP = workspace.Map
local Env: table = {}

local TweenService: TweenService = game:GetService("TweenService")
local UserInputService: UserInputService = game:GetService("UserInputService")

local function GetIcon(i)
	if type(i) == 'string' and not i:find('rbxassetid://') then
		return "rbxassetid://".. i
	elseif type(i) == 'number' then
		return "rbxassetid://".. i
	else
		return i
	end
end

tw = function(info)
	return TweenService:Create(info.v, TweenInfo.new(info.t, Enum.EasingStyle[info.s], Enum.EasingDirection[info.d]), info.g)
end

lak = function(a)
	local Dragging = nil
	local DragInput = nil
	local DragStart = nil
	local StartPosition = nil

	local function Update(input)
		local Delta = input.Position - DragStart
		local pos = UDim2.new(StartPosition.X.Scale, StartPosition.X.Offset + Delta.X, StartPosition.Y.Scale, StartPosition.Y.Offset + Delta.Y)
		local Tween = game:GetService("TweenService"):Create(a, TweenInfo.new(0.3), {Position = pos})
		Tween:Play()
	end

	a.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			Dragging = true
			DragStart = input.Position
			StartPosition = a.Position

			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					Dragging = false
				end
			end)
		end
	end)

	a.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			DragInput = input
		end
	end)

	game:GetService("UserInputService").InputChanged:Connect(function(input)
		if input == DragInput and Dragging then
			Update(input)
		end
	end)
end

click = function(p)
	local Click = Instance.new("TextButton")

	Click.Name = "Click"
	Click.Parent = p
	Click.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Click.BackgroundTransparency = 1.000
	Click.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Click.BorderSizePixel = 0
	Click.Size = UDim2.new(1, 0, 1, 0)
	Click.Font = Enum.Font.SourceSans
	Click.Text = ""
	Click.TextColor3 = Color3.fromRGB(0, 0, 0)
	Click.TextSize = 14.000

	return Click
end

EffectClick = function(c, p)
	local Mouse = game.Players.LocalPlayer:GetMouse()

	local relativeX = Mouse.X - c.AbsolutePosition.X
	local relativeY = Mouse.Y - c.AbsolutePosition.Y

	if relativeX < 0 or relativeY < 0 or relativeX > c.AbsoluteSize.X or relativeY > c.AbsoluteSize.Y then
		return
	end

	local ClickButtonCircle = Instance.new("Frame")
	ClickButtonCircle.Parent = p
	ClickButtonCircle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ClickButtonCircle.BackgroundTransparency = 0.5
	ClickButtonCircle.BorderSizePixel = 0
	ClickButtonCircle.AnchorPoint = Vector2.new(0.5, 0.5)
	ClickButtonCircle.Position = UDim2.new(0, relativeX, 0, relativeY)
	ClickButtonCircle.Size = UDim2.new(0, 0, 0, 0)
	ClickButtonCircle.ZIndex = p.ZIndex

	local UICorner = Instance.new("UICorner")
	UICorner.CornerRadius = UDim.new(1, 0)
	UICorner.Parent = ClickButtonCircle

	local tweenInfo = TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)

	local goal = {
		Size = UDim2.new(0, c.AbsoluteSize.X * 1.5, 0, c.AbsoluteSize.X * 1.5),
		BackgroundTransparency = 1
	}

	local expandTween = TweenService:Create(ClickButtonCircle, tweenInfo, goal)

	expandTween.Completed:Connect(function()
		ClickButtonCircle:Destroy()
	end)

	expandTween:Play()
end

local FummyKawaii = Instance.new("ScreenGui")
FummyKawaii.Name = "FummyKawaii"
FummyKawaii.Parent = not game:GetService("RunService"):IsStudio() and game:GetService("CoreGui") or game:GetService("Players").LocalPlayer.PlayerGui
FummyKawaii.ResetOnSpawn = false
FummyKawaii.ZIndexBehavior = Enum.ZIndexBehavior.Global
FummyKawaii.IgnoreGuiInset = true




function Env:Window(meta)

	local Banner = meta.Banner or 88995666059544
	local Bind = meta.Bind or Enum.KeyCode.LeftControl
	local Logo = meta.Logo or 0
	local Theme = {
		[1] = meta.Color[1] or Color3.fromRGB(0, 255, 127);
		[2] = meta.Color[2] or Color3.fromRGB(0, 170, 255);
		[3] = meta.Color[3] or Color3.fromRGB(85, 85, 255);
	}

	local GetColor = function()
		return ColorSequence.new{ColorSequenceKeypoint.new(0, Theme[1]), ColorSequenceKeypoint.new(0.482699, Theme[2]), ColorSequenceKeypoint.new(1, Theme[3])}
	end

	local layer = function(a)

		a.ClipsDescendants = true

		local ImageLabel = Instance.new("ImageLabel")
		local UIGradient_1 = Instance.new("UIGradient")

		ImageLabel.Parent = a
		ImageLabel.AnchorPoint = Vector2.new(0.5, 0.5)
		ImageLabel.BackgroundColor3 = Color3.fromRGB(255,255,255)
		ImageLabel.BackgroundTransparency = 1
		ImageLabel.BorderColor3 = Color3.fromRGB(0,0,0)
		ImageLabel.BorderSizePixel = 0
		ImageLabel.Position = UDim2.new(0.5, 0,0.5, 0)
		ImageLabel.Size = UDim2.new(1, 50,1, 0)
		ImageLabel.Image = "rbxassetid://72380279434385"
		ImageLabel.ImageTransparency = 0.95
		ImageLabel.ScaleType = Enum.ScaleType.Crop

		UIGradient_1.Parent = ImageLabel
		UIGradient_1.Color = GetColor()

		local ImageLabelc = Instance.new("ImageLabel")
		local UIGradient_1c = Instance.new("UIGradient")

		ImageLabelc.Parent = a
		ImageLabelc.AnchorPoint = Vector2.new(0.5, 0.5)
		ImageLabelc.BackgroundColor3 = Color3.fromRGB(255,255,255)
		ImageLabelc.BackgroundTransparency = 1
		ImageLabelc.BorderColor3 = Color3.fromRGB(0,0,0)
		ImageLabelc.BorderSizePixel = 0
		ImageLabelc.Position = UDim2.new(0.5, 0,0.5, 0)
		ImageLabelc.Size = UDim2.new(1, 0,1, 0)
		ImageLabelc.Image = "rbxassetid://300134974"
		ImageLabelc.ImageTransparency = 0.9
		ImageLabelc.ScaleType = Enum.ScaleType.Tile
		ImageLabelc.TileSize = UDim2.new(0.3, 0,1, 0)


		UIGradient_1c.Parent = ImageLabelc
		UIGradient_1c.Color = GetColor()
	end

	local EffectClick2 = function(c, p)
		local Mouse = game.Players.LocalPlayer:GetMouse()

		local relativeX = Mouse.X - c.AbsolutePosition.X
		local relativeY = Mouse.Y - c.AbsolutePosition.Y

		if relativeX < 0 or relativeY < 0 or relativeX > c.AbsoluteSize.X or relativeY > c.AbsoluteSize.Y then
			return
		end

		local ClickButtonCircle = Instance.new("Frame")
		ClickButtonCircle.Parent = p
		ClickButtonCircle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		ClickButtonCircle.BackgroundTransparency = 0.5
		ClickButtonCircle.BorderSizePixel = 0
		ClickButtonCircle.AnchorPoint = Vector2.new(0.5, 0.5)
		ClickButtonCircle.Position = UDim2.new(0, relativeX, 0, relativeY)
		ClickButtonCircle.Size = UDim2.new(0, 0, 0, 0)
		ClickButtonCircle.ZIndex = 10

		local UIGradient_2 = Instance.new("UIGradient")
		UIGradient_2.Parent = ClickButtonCircle
		UIGradient_2.Color = GetColor()
		UIGradient_2.Rotation = 48

		local UICorner = Instance.new("UICorner")
		UICorner.CornerRadius = UDim.new(1, 0)
		UICorner.Parent = ClickButtonCircle

		local tweenInfo = TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)

		local goal = {
			Size = UDim2.new(0, c.AbsoluteSize.X * 1.5, 0, c.AbsoluteSize.X * 1.5),
			BackgroundTransparency = 1
		}

		local expandTween = TweenService:Create(ClickButtonCircle, tweenInfo, goal)

		expandTween.Completed:Connect(function()
			ClickButtonCircle:Destroy()
		end)

		expandTween:Play()
	end

	local Effectx = Instance.new("Frame")
	local ImageLabel_1x = Instance.new("ImageLabel")
	local UIGradient_1x = Instance.new("UIGradient")

	Effectx.Name = "Effect"
	Effectx.Parent = FummyKawaii
	Effectx.AnchorPoint = Vector2.new(0.5, 0.5)
	Effectx.BackgroundColor3 = Color3.fromRGB(0,0,0)
	Effectx.BackgroundTransparency = 1
	Effectx.BorderColor3 = Color3.fromRGB(0,0,0)
	Effectx.BorderSizePixel = 0
	Effectx.Position = UDim2.new(0.5, 0,0.5, 0)
	Effectx.Size = UDim2.new(1, 0,1, 0)
	Effectx.ZIndex = -99

	ImageLabel_1x.Parent = Effectx
	ImageLabel_1x.AnchorPoint = Vector2.new(0.5, 0.5)
	ImageLabel_1x.BackgroundColor3 = Color3.fromRGB(255,255,255)
	ImageLabel_1x.BackgroundTransparency = 1
	ImageLabel_1x.BorderColor3 = Color3.fromRGB(0,0,0)
	ImageLabel_1x.BorderSizePixel = 0
	ImageLabel_1x.Position = UDim2.new(0.5, 0,0.5, 0)
	ImageLabel_1x.Size = UDim2.new(1, 0,1, 0)
	ImageLabel_1x.ZIndex = -90
	ImageLabel_1x.Image = "rbxassetid://84172340211125"
	ImageLabel_1x.ImageTransparency = 1

	UIGradient_1x.Parent = ImageLabel_1x
	UIGradient_1x.Color = ColorSequence.new{ColorSequenceKeypoint.new(0, Theme[1]), ColorSequenceKeypoint.new(0.482699, Theme[2]), ColorSequenceKeypoint.new(1, Theme[1])}
	UIGradient_1x.Rotation = 90

	local Background_1 = Instance.new("Frame")
	local DropShadow_1 = Instance.new("ImageLabel")
	local UIGradient_1 = Instance.new("UIGradient")
	local Pattern_1 = Instance.new("ImageLabel")
	local UIGradient_2 = Instance.new("UIGradient")
	local UIStroke_1 = Instance.new("UIStroke")

	Background_1.Name = "Background"
	Background_1.Parent = FummyKawaii
	Background_1.AnchorPoint = Vector2.new(0.5, 0.5)
	Background_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
	Background_1.BorderColor3 = Color3.fromRGB(0,0,0)
	Background_1.BorderSizePixel = 0
	Background_1.Position = UDim2.new(0.5, 0,0.5, 0)
	Background_1.Size = UDim2.new(0, 0,0, 0)
	do
		lak(Background_1)
		tw({v = Background_1,t = 1,s = "Bounce",d = "Out",g = {Size = UDim2.new(0, 574,0, 365)}}):Play()
		tw({v = ImageLabel_1x,t = 1,s = "Back",d = "Out",g = {ImageTransparency = 0}}):Play()
	end
	
	DropShadow_1.Name = "DropShadow"
	DropShadow_1.Parent = Background_1
	DropShadow_1.AnchorPoint = Vector2.new(0.5, 0.5)
	DropShadow_1.BackgroundColor3 = Color3.fromRGB(28,28,30)
	DropShadow_1.BackgroundTransparency = 1
	DropShadow_1.BorderColor3 = Color3.fromRGB(0,0,0)
	DropShadow_1.BorderSizePixel = 0
	DropShadow_1.Position = UDim2.new(0.5, 0,0.5, 0)
	DropShadow_1.Size = UDim2.new(1, 120,1, 120)
	DropShadow_1.ZIndex = 0
	DropShadow_1.Image = "rbxassetid://8992230677"
	DropShadow_1.ImageTransparency = 0.30000001192092896
	DropShadow_1.ScaleType = Enum.ScaleType.Slice
	DropShadow_1.SliceCenter = Rect.new(99, 99, 99, 99)

	UIGradient_1.Parent = DropShadow_1
	UIGradient_1.Color = GetColor()
	UIGradient_1.Rotation = 90

	Pattern_1.Name = "Pattern"
	Pattern_1.Parent = Background_1
	Pattern_1.AnchorPoint = Vector2.new(0.5, 0.5)
	Pattern_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
	Pattern_1.BackgroundTransparency = 1
	Pattern_1.BorderColor3 = Color3.fromRGB(0,0,0)
	Pattern_1.BorderSizePixel = 0
	Pattern_1.Position = UDim2.new(0.5, 0,0.5, 0)
	Pattern_1.Size = UDim2.new(1, 0,1, 0)
	Pattern_1.Image = "rbxassetid://102561425705322"
	Pattern_1.ScaleType = Enum.ScaleType.Crop

	UIGradient_2.Parent = Pattern_1
	UIGradient_2.Color = GetColor()
	UIGradient_2.Rotation = 90

	UIStroke_1.Parent = Background_1
	UIStroke_1.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	UIStroke_1.Thickness = 2

	local InsideBG_1 = Instance.new("Frame")
	local Banner_1 = Instance.new("Frame")
	local RealBanner_1 = Instance.new("ImageLabel")
	local UIStroke_2 = Instance.new("UIStroke")
	local Tab_1 = Instance.new("Frame")
	local ScrollingFrame_1 = Instance.new("ScrollingFrame")
	local UIListLayout_1 = Instance.new("UIListLayout")
	local UIListLayout_2 = Instance.new("UIListLayout")

	InsideBG_1.Name = "InsideBG"
	InsideBG_1.Parent = Background_1
	InsideBG_1.AnchorPoint = Vector2.new(0.5, 0.5)
	InsideBG_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
	InsideBG_1.BackgroundTransparency = 1
	InsideBG_1.BorderColor3 = Color3.fromRGB(0,0,0)
	InsideBG_1.BorderSizePixel = 0
	InsideBG_1.Position = UDim2.new(0.5, 0,0.5, 0)
	InsideBG_1.Size = UDim2.new(1, 0,1, 0)

	UIListLayout_2.Parent = InsideBG_1
	UIListLayout_2.Padding = UDim.new(0,7)
	UIListLayout_2.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout_2.VerticalAlignment = Enum.VerticalAlignment.Center

	Banner_1.Name = "Banner"
	Banner_1.Parent = InsideBG_1
	Banner_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
	Banner_1.BackgroundTransparency = 1
	Banner_1.BorderColor3 = Color3.fromRGB(0,0,0)
	Banner_1.BorderSizePixel = 0
	Banner_1.Position = UDim2.new(0.0209059231, 0,0.0246575344, 0)
	Banner_1.Size = UDim2.new(0.963414609, 0,0.461643845, 0)

	RealBanner_1.Name = "RealBanner"
	RealBanner_1.Parent = Banner_1
	RealBanner_1.AnchorPoint = Vector2.new(0.5, 0.5)
	RealBanner_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
	RealBanner_1.BackgroundTransparency = 1
	RealBanner_1.BorderColor3 = Color3.fromRGB(0,0,0)
	RealBanner_1.BorderSizePixel = 0
	RealBanner_1.Position = UDim2.new(0.5, 0,0.5, 0)
	RealBanner_1.Size = UDim2.new(1, 0,1, 0)
	RealBanner_1.Image = GetIcon(Banner)
	RealBanner_1.ScaleType = Enum.ScaleType.Crop

	UIStroke_2.Parent = RealBanner_1
	UIStroke_2.Thickness = 1

	Tab_1.Name = "Tab"
	Tab_1.Parent = InsideBG_1
	Tab_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
	Tab_1.BackgroundTransparency = 0.30000001192092896
	Tab_1.BorderColor3 = Color3.fromRGB(0,0,0)
	Tab_1.BorderSizePixel = 0
	Tab_1.Position = UDim2.new(0.0209059231, 0,0.504109561, 0)
	Tab_1.Size = UDim2.new(0.963414609, 0,0.472602725, 0)

	ScrollingFrame_1.Name = "ScrollingFrame"
	ScrollingFrame_1.Parent = Tab_1
	ScrollingFrame_1.Active = true
	ScrollingFrame_1.AnchorPoint = Vector2.new(0.5, 0.5)
	ScrollingFrame_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
	ScrollingFrame_1.BackgroundTransparency = 1
	ScrollingFrame_1.BorderColor3 = Color3.fromRGB(0,0,0)
	ScrollingFrame_1.BorderSizePixel = 0
	ScrollingFrame_1.Position = UDim2.new(0.5, 0,0.5, 0)
	ScrollingFrame_1.Size = UDim2.new(0.970000029, 0,0.899999976, 0)
	ScrollingFrame_1.ClipsDescendants = true
	ScrollingFrame_1.AutomaticCanvasSize = Enum.AutomaticSize.None
	ScrollingFrame_1.BottomImage = "rbxasset://textures/ui/Scroll/scroll-bottom.png"
	ScrollingFrame_1.CanvasPosition = Vector2.new(0, 0)
	ScrollingFrame_1.CanvasSize = UDim2.new(0, 0,0, 0)
	ScrollingFrame_1.ElasticBehavior = Enum.ElasticBehavior.WhenScrollable
	ScrollingFrame_1.HorizontalScrollBarInset = Enum.ScrollBarInset.None
	ScrollingFrame_1.MidImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
	ScrollingFrame_1.ScrollBarImageColor3 = Color3.fromRGB(0,0,0)
	ScrollingFrame_1.ScrollBarImageTransparency = 1
	ScrollingFrame_1.ScrollBarThickness = 0
	ScrollingFrame_1.ScrollingDirection = Enum.ScrollingDirection.XY
	ScrollingFrame_1.TopImage = "rbxasset://textures/ui/Scroll/scroll-top.png"
	ScrollingFrame_1.VerticalScrollBarInset = Enum.ScrollBarInset.None
	ScrollingFrame_1.VerticalScrollBarPosition = Enum.VerticalScrollBarPosition.Right

	UIListLayout_1.Parent = ScrollingFrame_1
	UIListLayout_1.Padding = UDim.new(0,10)
	UIListLayout_1.FillDirection = Enum.FillDirection.Horizontal
	UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder

    UIListLayout_1:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
        UIListLayout_1.CanvasSize = UDim2.new(0, UIListLayout_1.AbsoluteContentSize.X + 20, 0, 0)
    end)

	local CloseUI = Instance.new("TextButton")
	local UICorner_1z = Instance.new("UICorner")
	local Icon_1 = Instance.new("Frame")
	local ImageLabel = Instance.new("ImageLabel")


	CloseUI.Name = "CloseUI"
	CloseUI.Parent = FummyKawaii
	CloseUI.AnchorPoint = Vector2.new(0, 1)
	CloseUI.BackgroundColor3 = Color3.fromRGB(0,0,0)
	CloseUI.BorderColor3 = Color3.fromRGB(0,0,0)
	CloseUI.BorderSizePixel = 0
	CloseUI.Position = UDim2.new(0.5, 0,0.1, 0)
	CloseUI.Size = UDim2.new(0, 50,0, 50)
	CloseUI.BackgroundTransparency = 0.35
	CloseUI.Text = ""

	lak(CloseUI)

	UICorner_1z.Parent = CloseUI
	UICorner_1z.CornerRadius = UDim.new(0,5)

	Icon_1.Name = "Icon"
	Icon_1.Parent = CloseUI
	Icon_1.BackgroundColor3 = Color3.fromRGB(22,22,22)
	Icon_1.BorderColor3 = Color3.fromRGB(0,0,0)
	Icon_1.BorderSizePixel = 0
	Icon_1.Size = UDim2.new(0, 50,0, 50)
	Icon_1.BackgroundTransparency = 1

	ImageLabel.Parent = Icon_1
	ImageLabel.AnchorPoint = Vector2.new(0.5, 0.5)
	ImageLabel.BackgroundColor3 = Color3.fromRGB(255,255,255)
	ImageLabel.BackgroundTransparency = 1
	ImageLabel.BorderColor3 = Color3.fromRGB(0,0,0)
	ImageLabel.BorderSizePixel = 0
	ImageLabel.Position = UDim2.new(0.5, 0,0.5, 0)
	ImageLabel.Size = UDim2.new(0, 45,0, 45)
	ImageLabel.Image = GetIcon(Logo)
	ImageLabel.ImageTransparency = 0

	local function closeopenui()
		task.spawn(function()
			tw({
				v = ImageLabel,
				t = 0.2,
				s = "Back",
				d = "Out",
				g = {Size = UDim2.new(0, 35, 0, 35)}
			}):Play()
			task.wait(0.016) 
			tw({
				v = ImageLabel,
				t = 0.2,
				s = "Back",
				d = "Out",
				g = {Size = UDim2.new(0, 45, 0, 45)}
			}):Play()
		end)
		Background_1.Visible = not Background_1.Visible
	end

	local On = true

	CloseUI.MouseButton1Click:Connect(function()
		closeopenui()
		On = not On
		if On then
			tw({v = ImageLabel_1x, t = 1, s = "Back", d = "Out", g = {ImageTransparency = 0}}):Play()
		else
			tw({v = ImageLabel_1x, t = 1, s = "Back", d = "Out", g = {ImageTransparency = 1}}):Play()
		end
	end)

	UserInputService.InputBegan:Connect(function(input, gameProcessed)
		if not gameProcessed and input.KeyCode == Bind then
			closeopenui()
			On = not On
			if On then
				tw({v = ImageLabel_1x, t = 1, s = "Back", d = "Out", g = {ImageTransparency = 0}}):Play()
			else
				tw({v = ImageLabel_1x, t = 1, s = "Back", d = "Out", g = {ImageTransparency = 1}}):Play()
			end
			print("Cloase")
		end
	end)

	local Return_1 = Instance.new("Frame")
	local Close_1 = Instance.new("ImageLabel")
	local UIGradient_4 = Instance.new("UIGradient")
	local TextLabel_1 = Instance.new("TextLabel")
	local UIStroke_3 = Instance.new("UIStroke")

	Env.Tabs = {}

	function Env.Tabs:Tab(meta)
		local Title = meta.Title or "You forgot Title"
		local Desc = meta.Desc or "You forgot Desc"
		local Icon = meta.Icon or 0

		local Addtab_1 = Instance.new("Frame")
		local TabImage_1 = Instance.new("ImageLabel")
		local UIGradient_3 = Instance.new("UIGradient")
		local Icon_1 = Instance.new("ImageLabel")
		local ClickTab = click(Addtab_1)

		Addtab_1.Name = "Addtab"
		Addtab_1.Parent = ScrollingFrame_1
		Addtab_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
		Addtab_1.BackgroundTransparency = 0.5
		Addtab_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Addtab_1.BorderSizePixel = 0
		Addtab_1.Position = UDim2.new(5.54562583e-08, 0,0, 0)
		Addtab_1.Size = UDim2.new(0, 100,1, 0)

		TabImage_1.Name = "TabImage"
		TabImage_1.Parent = Addtab_1
		TabImage_1.AnchorPoint = Vector2.new(0.5, 0.5)
		TabImage_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		TabImage_1.BackgroundTransparency = 1
		TabImage_1.BorderColor3 = Color3.fromRGB(0,0,0)
		TabImage_1.BorderSizePixel = 0
		TabImage_1.Position = UDim2.new(0.5, 0,0.5, 0)
		TabImage_1.Size = UDim2.new(1, 0,1, 0)
		TabImage_1.Image = "rbxassetid://119836447849309"
		TabImage_1.ImageTransparency = 0.20000000298023224
		TabImage_1.ScaleType = Enum.ScaleType.Crop

		UIGradient_3.Parent = TabImage_1
		UIGradient_3.Color = GetColor()
		UIGradient_3.Rotation = 90

		Icon_1.Name = "Icon"
		Icon_1.Parent = TabImage_1
		Icon_1.AnchorPoint = Vector2.new(0.5, 0.5)
		Icon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Icon_1.BackgroundTransparency = 1
		Icon_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Icon_1.BorderSizePixel = 0
		Icon_1.Position = UDim2.new(0.5, 0,0.5, 0)
		Icon_1.Size = UDim2.new(0, 50,0, 50)
		Icon_1.Image = GetIcon(Icon)

		local Pages_1 = Instance.new("Frame")
		local Header_1 = Instance.new("Frame")
		local UIListLayout_3 = Instance.new("UIListLayout")
		local Icon_2 = Instance.new("Frame")
		local RealIcon_1 = Instance.new("ImageLabel")
		local Text_1 = Instance.new("Frame")
		local Title_1 = Instance.new("TextLabel")
		local Desc_1 = Instance.new("TextLabel")
		local UIListLayout_4 = Instance.new("UIListLayout")

		Header_1.Name = "Header"
		Header_1.Parent = Pages_1
		Header_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
		Header_1.BackgroundTransparency = 0.30000001192092896
		Header_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Header_1.BorderSizePixel = 0
		Header_1.Position = UDim2.new(0.0182926822, 0,0.0287671238, 0)
		Header_1.Size = UDim2.new(0.963414609, 0,0.168493152, 0)

		UIListLayout_3.Parent = Header_1
		UIListLayout_3.FillDirection = Enum.FillDirection.Horizontal
		UIListLayout_3.SortOrder = Enum.SortOrder.LayoutOrder

		Icon_2.Name = "Icon"
		Icon_2.Parent = Header_1
		Icon_2.AnchorPoint = Vector2.new(0.5, 0.5)
		Icon_2.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Icon_2.BackgroundTransparency = 1
		Icon_2.BorderColor3 = Color3.fromRGB(0,0,0)
		Icon_2.BorderSizePixel = 0
		Icon_2.Position = UDim2.new(0.0524412282, 0,0.5, 0)
		Icon_2.Size = UDim2.new(0, 59,0, 59)
		Icon_2.LayoutOrder = -3

		RealIcon_1.Name = "RealIcon"
		RealIcon_1.Parent = Icon_2
		RealIcon_1.AnchorPoint = Vector2.new(0.5, 0.5)
		RealIcon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		RealIcon_1.BackgroundTransparency = 1
		RealIcon_1.BorderColor3 = Color3.fromRGB(0,0,0)
		RealIcon_1.BorderSizePixel = 0
		RealIcon_1.Position = UDim2.new(0.5, 0,0.5, 0)
		RealIcon_1.Size = UDim2.new(0, 35,0, 35)
		RealIcon_1.Image = GetIcon(Icon)
		RealIcon_1.ScaleType = Enum.ScaleType.Crop

		Text_1.Name = "Text"
		Text_1.Parent = Header_1
		Text_1.AnchorPoint = Vector2.new(0.5, 0.5)
		Text_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Text_1.BackgroundTransparency = 1
		Text_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Text_1.BorderSizePixel = 0
		Text_1.Position = UDim2.new(0.42766726, 0,0.49999997, 0)
		Text_1.Size = UDim2.new(0.641952991, 0,0.99999994, 0)
		Text_1.LayoutOrder = -2

		Title_1.Name = "Title"
		Title_1.Parent = Text_1
		Title_1.AnchorPoint = Vector2.new(0.5, 0.5)
		Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Title_1.BackgroundTransparency = 1
		Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Title_1.BorderSizePixel = 0
		Title_1.Position = UDim2.new(0.5, 0,0.357895315, 0)
		Title_1.Size = UDim2.new(1, 0,-0.133745581, 20)
		Title_1.Font = Enum.Font.GothamBold
		Title_1.RichText = true
		Title_1.LayoutOrder = -1
		Title_1.Text = Title
		Title_1.TextColor3 = Color3.fromRGB(255,255,255)
		Title_1.TextSize = 18
		Title_1.TextXAlignment = Enum.TextXAlignment.Left

		Desc_1.Name = "Desc"
		Desc_1.Parent = Text_1
		Desc_1.AnchorPoint = Vector2.new(0.5, 0.5)
		Desc_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Desc_1.BackgroundTransparency = 1
		Desc_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Desc_1.BorderSizePixel = 0
		Desc_1.Position = UDim2.new(0.5, 0,0.608049929, 0)
		Desc_1.Size = UDim2.new(1, 0,-0.183900163, 20)
		Desc_1.Font = Enum.Font.GothamMedium
		Desc_1.RichText = true
		Desc_1.Text = Desc
		Desc_1.TextColor3 = Color3.fromRGB(255,255,255)
		Desc_1.TextSize = 13
		Desc_1.TextTransparency = 0.5
		Desc_1.TextXAlignment = Enum.TextXAlignment.Left

		UIListLayout_4.Parent = Text_1
		UIListLayout_4.Padding = UDim.new(0,5)
		UIListLayout_4.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout_4.VerticalAlignment = Enum.VerticalAlignment.Center

		local Return_1 = Instance.new("Frame")
		local Close_1 = Instance.new("ImageLabel")
		local UIGradient_4 = Instance.new("UIGradient")
		local TextLabel_1 = Instance.new("TextLabel")
		local UIStroke_3 = Instance.new("UIStroke")
		local ClickBack = click(Return_1)

		ClickBack.MouseButton1Click:Connect(function()
			tw({
				v = Return_1,
				t = 0.03,
				s = "Bounce",
				d = "Out",
				g = {Size = UDim2.new(0.20, 0,0.90, 0)}
			}):Play()
			delay(0.05, function()
				tw({
					v = Return_1,
					t = 0.03,
					s = "Bounce",
					d = "Out",
					g = {Size = UDim2.new(0.251140952, 0,0.99999994, 0)}
				}):Play()
			end)
			task.wait(0.1)
			Return_1.Visible = false
			InsideBG_1.Size = UDim2.new(0, 0,0, 0)
			InsideBG_1.Visible = true
			tw({
				v = InsideBG_1,
				t = 0.3,
				s = "Back",
				d = "Out",
				g = {Size = UDim2.new(1, 0,1, 0)}
			}):Play()
			for _, v in pairs(Background_1:GetChildren()) do
				if v.Name == "Pages" then
					v.Visible = false
				end
			end
		end)


		Return_1.Name = "Return"
		Return_1.Parent = Header_1
		Return_1.AnchorPoint = Vector2.new(0.5, 0.5)
		Return_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Return_1.BackgroundTransparency = 1
		Return_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Return_1.BorderSizePixel = 0
		Return_1.Position = UDim2.new(0.874214292, 0,0.49999997, 0)
		Return_1.Size = UDim2.new(0.251140952, 0,0.99999994, 0)
		Return_1.Visible = false

		Close_1.Name = "Close"
		Close_1.Parent = Return_1
		Close_1.AnchorPoint = Vector2.new(0.5, 0.5)
		Close_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Close_1.BackgroundTransparency = 1
		Close_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Close_1.BorderSizePixel = 0
		Close_1.Position = UDim2.new(0.5, 0,0.5, 0)
		Close_1.Size = UDim2.new(0.800000012, 0,0.699999988, 0)
		Close_1.Image = "rbxassetid://107541348612338"

		UIGradient_4.Parent = Close_1
		UIGradient_4.Color = GetColor()
		UIGradient_4.Rotation = -29

		TextLabel_1.Parent = Close_1
		TextLabel_1.AnchorPoint = Vector2.new(0.5, 0.5)
		TextLabel_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		TextLabel_1.BackgroundTransparency = 1
		TextLabel_1.BorderColor3 = Color3.fromRGB(0,0,0)
		TextLabel_1.BorderSizePixel = 0
		TextLabel_1.Position = UDim2.new(0.5, 0,0.5, 0)
		TextLabel_1.Size = UDim2.new(1, 0,1, 0)
		TextLabel_1.Font = Enum.Font.GothamBold
		TextLabel_1.Text = "Return"
		TextLabel_1.TextColor3 = Color3.fromRGB(255,255,255)
		TextLabel_1.TextSize = 17

		UIStroke_3.Parent = TextLabel_1
		UIStroke_3.Color = Color3.fromRGB(63,63,63)
		UIStroke_3.Thickness = 1

		local UIListLayout_5 = Instance.new("UIListLayout")
		local RealPages_1 = Instance.new("Frame")
		local Left_1 = Instance.new("ScrollingFrame")
		local UIListLayout_6 = Instance.new("UIListLayout")
		local Right_1 = Instance.new("ScrollingFrame")
		local UIListLayout_7 = Instance.new("UIListLayout")
		local UIListLayout_8 = Instance.new("UIListLayout")
		local UIPadding_1 = Instance.new("UIPadding")

		Pages_1.Name = "Pages"
		Pages_1.Parent = Background_1
		Pages_1.AnchorPoint = Vector2.new(0.5, 0.5)
		Pages_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Pages_1.BackgroundTransparency = 1
		Pages_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Pages_1.BorderSizePixel = 0
		Pages_1.Position = UDim2.new(0.5, 0,0.5, 0)
		Pages_1.Size = UDim2.new(1, 0,1, 0)
		Pages_1.Visible = false

		ClickTab.MouseButton1Click:Connect(function()
			Return_1.Visible = true
			Pages_1.Visible = true
			Pages_1.Size = UDim2.new(0, 0,0, 0)
			tw({
				v = Pages_1,
				t = 0.3,
				s = "Back",
				d = "Out",
				g = {Size = UDim2.new(1, 0,1, 0)}
			}):Play()
			InsideBG_1.Visible = false
		end)

		UIListLayout_5.Parent = Pages_1
		UIListLayout_5.Padding = UDim.new(0,4)
		UIListLayout_5.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout_5.SortOrder = Enum.SortOrder.LayoutOrder

		RealPages_1.Name = "RealPages"
		RealPages_1.Parent = Pages_1
		RealPages_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
		RealPages_1.BackgroundTransparency = 0.30000001192092896
		RealPages_1.BorderColor3 = Color3.fromRGB(0,0,0)
		RealPages_1.BorderSizePixel = 0
		RealPages_1.Position = UDim2.new(0.0182926822, 0,0.188211441, 0)
		RealPages_1.Size = UDim2.new(0.963, 0,0.800000012, 0)

		Left_1.Name = "Left"
		Left_1.Parent = RealPages_1
		Left_1.Active = true
		Left_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Left_1.BackgroundTransparency = 1
		Left_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Left_1.BorderSizePixel = 0
		Left_1.Size = UDim2.new(0, 275,1, 0)
		Left_1.ClipsDescendants = true
		Left_1.AutomaticCanvasSize = Enum.AutomaticSize.None
		Left_1.BottomImage = "rbxasset://textures/ui/Scroll/scroll-bottom.png"
		Left_1.CanvasPosition = Vector2.new(0, 0)
		Left_1.CanvasSize = UDim2.new(0, 0,0, 339)
		Left_1.ElasticBehavior = Enum.ElasticBehavior.WhenScrollable
		Left_1.HorizontalScrollBarInset = Enum.ScrollBarInset.None
		Left_1.MidImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
		Left_1.ScrollBarImageColor3 = Color3.fromRGB(0,0,0)
		Left_1.ScrollBarImageTransparency = 1
		Left_1.ScrollBarThickness = 0
		Left_1.ScrollingDirection = Enum.ScrollingDirection.XY
		Left_1.TopImage = "rbxasset://textures/ui/Scroll/scroll-top.png"
		Left_1.VerticalScrollBarInset = Enum.ScrollBarInset.None
		Left_1.VerticalScrollBarPosition = Enum.VerticalScrollBarPosition.Right

		local UIPaddingl = Instance.new("UIPadding")
		UIPaddingl.Parent = Left_1
		UIPaddingl.PaddingTop = UDim.new(0,7)

		UIListLayout_6.Parent = Left_1
		UIListLayout_6.Padding = UDim.new(0,7)
		UIListLayout_6.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout_6.HorizontalAlignment = Enum.HorizontalAlignment.Center

		Right_1.Name = "Right"
		Right_1.Parent = RealPages_1
		Right_1.Active = true
		Right_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
		Right_1.BackgroundTransparency = 1
		Right_1.BorderColor3 = Color3.fromRGB(0,0,0)
		Right_1.BorderSizePixel = 0
		Right_1.Size = UDim2.new(0, 275,1, 0)
		Right_1.ClipsDescendants = true
		Right_1.AutomaticCanvasSize = Enum.AutomaticSize.None
		Right_1.BottomImage = "rbxasset://textures/ui/Scroll/scroll-bottom.png"
		Right_1.CanvasPosition = Vector2.new(0, 0)
		Right_1.CanvasSize = UDim2.new(0, 0,0, 64)
		Right_1.ElasticBehavior = Enum.ElasticBehavior.WhenScrollable
		Right_1.HorizontalScrollBarInset = Enum.ScrollBarInset.None
		Right_1.MidImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
		Right_1.ScrollBarImageColor3 = Color3.fromRGB(0,0,0)
		Right_1.ScrollBarImageTransparency = 1
		Right_1.ScrollBarThickness = 0
		Right_1.ScrollingDirection = Enum.ScrollingDirection.XY
		Right_1.TopImage = "rbxasset://textures/ui/Scroll/scroll-top.png"
		Right_1.VerticalScrollBarInset = Enum.ScrollBarInset.None
		Right_1.VerticalScrollBarPosition = Enum.VerticalScrollBarPosition.Right

		local UIPaddinge = Instance.new("UIPadding")
		UIPaddinge.Parent = Right_1
		UIPaddinge.PaddingTop = UDim.new(0,7)

		UIListLayout_7.Parent = Right_1
		UIListLayout_7.Padding = UDim.new(0,7)
		UIListLayout_7.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout_7.HorizontalAlignment = Enum.HorizontalAlignment.Center

		UIListLayout_8.Parent = RealPages_1
		UIListLayout_8.Padding = UDim.new(0,6)
		UIListLayout_8.FillDirection = Enum.FillDirection.Horizontal
		UIListLayout_8.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout_8.VerticalAlignment = Enum.VerticalAlignment.Center

		UIPadding_1.Parent = Pages_1
		UIPadding_1.PaddingTop = UDim.new(0,10)

		UIListLayout_6:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			Left_1.CanvasSize = UDim2.new(0, 0, 0, UIListLayout_6.AbsoluteContentSize.Y + 20)
		end)

		UIListLayout_7:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			Right_1.CanvasSize = UDim2.new(0, 0, 0, UIListLayout_7.AbsoluteContentSize.Y + 20)
		end)

		Env.Section = {}

		local function GetSide(side)
			if not side then
				return Left_1
			end
			local sideLower = string.lower(tostring(side))
			if sideLower == "r" or sideLower == "right" or side == 2 then
				return Right_1
			elseif sideLower == "l" or sideLower == "left" or side == 1 then
				return Left_1
			else
				return Left_1
			end
		end

		function Env.Section:Section(meta)
			local Title = meta.Title or "You forgot Title"
			local Side = meta.Side or "l"

			local Section = Instance.new("Frame")
			local UIListLayout_1z = Instance.new("UIListLayout")
			local Title_1 = Instance.new("TextLabel")
			local UIPadding_1 = Instance.new("UIPadding")
			local Line_1 = Instance.new("Frame")
			local UIGradient_1 = Instance.new("UIGradient")
			local UIGradient_2 = Instance.new("UIGradient")
			local UIStroke_1 = Instance.new("UIStroke")
			local UIGradient_3 = Instance.new("UIGradient")

			Section.Name = "Section"
			Section.Parent = GetSide(Side)
			Section.BackgroundColor3 = Color3.fromRGB(48,48,48)
			Section.BackgroundTransparency = 0.4000000059604645
			Section.BorderColor3 = Color3.fromRGB(20,20,20)
			Section.BorderSizePixel = 0
			Section.Size = UDim2.new(0.949999988, 0,0, 0)

			UIListLayout_1z.Parent = Section
			UIListLayout_1z.Padding = UDim.new(0,7)
			UIListLayout_1z.HorizontalAlignment = Enum.HorizontalAlignment.Center
			UIListLayout_1z.SortOrder = Enum.SortOrder.LayoutOrder

			print(UIListLayout_1z.AbsoluteContentSize.Y)

			UIListLayout_1z:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
				Section.Size = UDim2.new(0.95, 0, 0, UIListLayout_1z.AbsoluteContentSize.Y + 15)
				print(tostring(UIListLayout_1z.AbsoluteContentSize.Y))
			end)

			Title_1.Name = "Title"
			Title_1.Parent = Section
			Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
			Title_1.BackgroundTransparency = 1
			Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
			Title_1.BorderSizePixel = 0
			Title_1.LayoutOrder = -3
			Title_1.Size = UDim2.new(0.899999976, 0,0, 20)
			Title_1.Font = Enum.Font.GothamBold
			Title_1.Text = Title
			Title_1.TextColor3 = Color3.fromRGB(255,255,255)
			Title_1.TextSize = 15
			Title_1.TextTransparency = 0

			UIPadding_1.Parent = Section
			UIPadding_1.PaddingTop = UDim.new(0,7)

			Line_1.Name = "Line"
			Line_1.Parent = Section
			Line_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
			Line_1.BackgroundTransparency = 0.5
			Line_1.BorderColor3 = Color3.fromRGB(0,0,0)
			Line_1.BorderSizePixel = 0
			Line_1.LayoutOrder = -2
			Line_1.Position = UDim2.new(-0.209090903, 0,0.215053767, 0)
			Line_1.Size = UDim2.new(1, 0,0, 1)

			UIGradient_1.Parent = Line_1
			UIGradient_1.Color = GetColor()

			UIGradient_2.Parent = Section
			UIGradient_2.Color = GetColor()
			UIGradient_2.Rotation = 90

			UIStroke_1.Parent = Section
			UIStroke_1.Color = Color3.fromRGB(255,255,255)
			UIStroke_1.Thickness = 1
			UIStroke_1.Transparency = 0.5

			UIGradient_3.Parent = UIStroke_1
			UIGradient_3.Color = GetColor()
			UIGradient_3.Rotation = 90

			Env.Class = {}

			function Env.Class:Line()
				local Line_1 = Instance.new("Frame")
				local UIGradient_1 = Instance.new("UIGradient")

				Line_1.Name = "Line"
				Line_1.Parent = Section
				Line_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Line_1.BackgroundTransparency = 0.5
				Line_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Line_1.Position = UDim2.new(-0.209090903, 0,0.215053767, 0)
				Line_1.Size = UDim2.new(1, 0,0, 1)

				UIGradient_1.Parent = Line_1
				UIGradient_1.Color = GetColor()
			end

			function Env.Class:Button(meta)
				local Title = meta.Title or "forgot"
				local Callback = meta.Callback or function()end
				local Desc = meta.Desc or false
				local Icon = meta.Icon or false

				if not Icon and not Desc then
					local Button = Instance.new("Frame")
					local ClickButon = click(Button)
					local ImageLabel_1 = Instance.new("ImageLabel")
					local UIGradient_1 = Instance.new("UIGradient")
					local Title_1 = Instance.new("TextLabel")
					local UIStroke_1 = Instance.new("UIStroke")

					Button.Name = "Button"
					Button.Parent = Section
					Button.AnchorPoint = Vector2.new(0.5, 0.5)
					Button.BackgroundColor3 = Color3.fromRGB(0,0,0)
					Button.BackgroundTransparency = 1
					Button.BorderColor3 = Color3.fromRGB(0,0,0)
					Button.BorderSizePixel = 0
					Button.Size = UDim2.new(0.949999988, 0,0, 35)

					ImageLabel_1.Parent = Button
					ImageLabel_1.AnchorPoint = Vector2.new(0.5, 0.5)
					ImageLabel_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					ImageLabel_1.BackgroundTransparency = 1
					ImageLabel_1.BorderColor3 = Color3.fromRGB(0,0,0)
					ImageLabel_1.BorderSizePixel = 0
					ImageLabel_1.Position = UDim2.new(0.5, 0,0.5, 0)
					ImageLabel_1.Size = UDim2.new(1, 0,1, 0)
					ImageLabel_1.Image = "rbxassetid://140569271063085"
					ImageLabel_1.ClipsDescendants = true

					UIGradient_1.Parent = ImageLabel_1
					UIGradient_1.Color = GetColor()
					UIGradient_1.Rotation = 100

					Title_1.Name = "Title"
					Title_1.Parent = ImageLabel_1
					Title_1.AnchorPoint = Vector2.new(0.5, 0.5)
					Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Title_1.BackgroundTransparency = 1
					Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Title_1.BorderSizePixel = 0
					Title_1.Position = UDim2.new(0.5, 0,0.5, 0)
					Title_1.Size = UDim2.new(1, 0,1, 0)
					Title_1.Font = Enum.Font.GothamBold
					Title_1.Text = Title
					Title_1.TextColor3 = Color3.fromRGB(255,255,255)
					Title_1.TextSize = 15

					UIStroke_1.Parent = Title_1
					UIStroke_1.Color = Color3.fromRGB(50,50,50)
					UIStroke_1.Thickness = 1

					ClickButon.MouseButton1Click:Connect(function()
						for _, v in pairs(Background_1:GetChildren()) do
							if v.Name == "Dropdown" and v.Visible then
								return
							end
						end
						Callback()
						tw({
							v = ImageLabel_1,
							t = 0.2,
							s = "Back",
							d = "Out",
							g = {Size = UDim2.new(0.9, 0,0.9, 0)}
						}):Play()
						delay(0.05, function()
							tw({
								v = ImageLabel_1,
								t = 0.2,
								s = "Back",
								d = "Out",
								g = {Size = UDim2.new(1, 0,1, 0)}
							}):Play()
						end)
					end)

					local index = {}

					function index:Title(a)
						Title_1.Text = a
					end

					function index:Visible(a)
						Button.Visible = a
					end

					function index:Callback(a)
						Callback = a
					end

					function index:Fire()
						Callback()
					end

					return index
				else
					local Button = Instance.new("Frame")
					local UIStroke_1 = Instance.new("UIStroke")
					local UIGradient_1 = Instance.new("UIGradient")
					local IN_1 = Instance.new("Frame")
					local UIPadding_1 = Instance.new("UIPadding")
					local UIListLayout_1 = Instance.new("UIListLayout")
					local Text_1 = Instance.new("Frame")
					local UIListLayout_2 = Instance.new("UIListLayout")
					local Title_1 = Instance.new("TextLabel")
					local Next_1 = Instance.new("Frame")
					local nexticon_1 = Instance.new("ImageLabel")
					local UIGradient_2 = Instance.new("UIGradient")
					local ClickButton = click(Button)

					layer(Button)


					Button.Name = "Button"
					Button.Parent = Section
					Button.AnchorPoint = Vector2.new(0.5, 0.5)
					Button.BackgroundColor3 = Color3.fromRGB(0,0,0)
					Button.BackgroundTransparency = 0.5
					Button.BorderColor3 = Color3.fromRGB(0,0,0)
					Button.BorderSizePixel = 0
					Button.Size = UDim2.new(0.949999988, 0,0, 50)
					Button.ClipsDescendants = true

					UIStroke_1.Parent = Button
					UIStroke_1.Color = Color3.fromRGB(255,255,255)
					UIStroke_1.Thickness = 1
					UIStroke_1.Transparency = 0.7

					UIGradient_1.Parent = UIStroke_1
					UIGradient_1.Color = GetColor()
					UIGradient_1.Rotation = 90

					IN_1.Name = "IN"
					IN_1.Parent = Button
					IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
					IN_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					IN_1.BackgroundTransparency = 1
					IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
					IN_1.BorderSizePixel = 0
					IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
					IN_1.Size = UDim2.new(1, 0,1, 0)

					UIPadding_1.Parent = IN_1

					UIListLayout_1.Parent = IN_1
					UIListLayout_1.FillDirection = Enum.FillDirection.Horizontal
					UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder
					UIListLayout_1.VerticalAlignment = Enum.VerticalAlignment.Center


					local Icon_1 = Instance.new("Frame")
					local realicon_1 = Instance.new("ImageLabel")
					if Icon then
						UIPadding_1.PaddingLeft = UDim.new(0,5)
						UIListLayout_1.Padding = UDim.new(0,7)

						Icon_1.Name = "Icon"
						Icon_1.Parent = IN_1
						Icon_1.AnchorPoint = Vector2.new(0.5, 0.5)
						Icon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Icon_1.BackgroundTransparency = 1
						Icon_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Icon_1.BorderSizePixel = 0
						Icon_1.Position = UDim2.new(0.100000001, 0,0.5, 0)
						Icon_1.Size = UDim2.new(0, 40,0, 40)
						Icon_1.ZIndex = -3

						realicon_1.Name = "realicon"
						realicon_1.Parent = Icon_1
						realicon_1.AnchorPoint = Vector2.new(0.5, 0.5)
						realicon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						realicon_1.BackgroundTransparency = 1
						realicon_1.BorderColor3 = Color3.fromRGB(0,0,0)
						realicon_1.BorderSizePixel = 0
						realicon_1.Position = UDim2.new(0.5, 0,0.5, 0)
						realicon_1.Size = UDim2.new(0.899999976, 0,0.899999976, 0)
						realicon_1.Image = "rbxassetid://114522983600169"
					else
						UIPadding_1.PaddingLeft = UDim.new(0,10)
						UIListLayout_1.Padding = UDim.new(0,50)
					end

					Text_1.Name = "Text"
					Text_1.Parent = IN_1
					Text_1.AnchorPoint = Vector2.new(0.5, 0.5)
					Text_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Text_1.BackgroundTransparency = 1
					Text_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Text_1.BorderSizePixel = 0
					Text_1.Position = UDim2.new(0.491390377, 0,0.5, 0)
					Text_1.Size = UDim2.new(0, 145,0, 40)

					UIListLayout_2.Parent = Text_1
					UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
					UIListLayout_2.VerticalAlignment = Enum.VerticalAlignment.Center

					Title_1.Name = "Title"
					Title_1.Parent = Text_1
					Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Title_1.BackgroundTransparency = 1
					Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Title_1.BorderSizePixel = 0
					Title_1.LayoutOrder = -3
					Title_1.Size = UDim2.new(0.899999976, 0,0, 15)
					Title_1.Font = Enum.Font.GothamBold
					Title_1.Text = Title
					Title_1.TextColor3 = Color3.fromRGB(255,255,255)
					Title_1.TextSize = 15
					Title_1.TextXAlignment = Enum.TextXAlignment.Left
					Title_1.RichText = true

					if Desc then
						local Desc_1 = Instance.new("TextLabel")
						Desc_1.Name = "Desc"
						Desc_1.Parent = Text_1
						Desc_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Desc_1.BackgroundTransparency = 1
						Desc_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Desc_1.BorderSizePixel = 0
						Desc_1.LayoutOrder = -3
						Desc_1.Size = UDim2.new(0.899999976, 0,0, 15)
						Desc_1.Font = Enum.Font.GothamMedium
						Desc_1.Text = Desc
						Desc_1.TextColor3 = Color3.fromRGB(255,255,255)
						Desc_1.TextSize = 12
						Desc_1.TextTransparency = 0.5
						Desc_1.TextXAlignment = Enum.TextXAlignment.Left
						Desc_1.RichText = true
					end

					Next_1.Name = "Next"
					Next_1.Parent = IN_1
					Next_1.AnchorPoint = Vector2.new(0.5, 0.5)
					Next_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Next_1.BackgroundTransparency = 1
					Next_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Next_1.BorderSizePixel = 0
					Next_1.Position = UDim2.new(0.911413252, 0,0.5, 0)
					Next_1.Size = UDim2.new(0, 40,0, 40)

					nexticon_1.Name = "nexticon"
					nexticon_1.Parent = Next_1
					nexticon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					nexticon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					nexticon_1.BackgroundTransparency = 1
					nexticon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					nexticon_1.BorderSizePixel = 0
					nexticon_1.Position = UDim2.new(0.5, 0,0.5, 0)
					nexticon_1.Size = UDim2.new(0.5, 0,0.5, 0)
					nexticon_1.Image = "rbxassetid://108028847031522"

					UIGradient_2.Parent = nexticon_1
					UIGradient_2.Color = GetColor()
					UIGradient_2.Rotation = 90	

					ClickButton.MouseButton1Click:Connect(function()
						for _, v in pairs(Background_1:GetChildren()) do
							if v.Name == "Dropdown" and v.Visible then
								return
							end
						end
						Callback()
						EffectClick2(ClickButton, Button)
						tw({
							v = nexticon_1,
							t = 0.2,
							s = "Back",
							d = "Out",
							g = {Size = UDim2.new(0.8, 0,0.8, 0)}
						}):Play()
						delay(0.05, function()
							tw({
								v = nexticon_1,
								t = 0.2,
								s = "Back",
								d = "Out",
								g = {Size = UDim2.new(0.5, 0,0.5, 0)}
							}):Play()
						end)
					end)

					local index = {}

					function index:Title(a)
						Title_1.Text = a
					end

					function index:Desc(a)
						Desc_1.Text = a
					end

					function index:Icon(a)
						realicon_1.Image = GetIcon(a)
					end

					function index:Visible(a)
						Button.Visible = a
					end

					function index:Callback(a)
						Callback = a
					end

					function index:Fire()
						Callback()
					end

					return index
				end
			end

			function Env.Class:Toggle(meta)
				local Title = meta.Title or "for got title?"
				local Desc = meta.Desc or ""
				local Icon = meta.Icon or ""
				local Value = meta.Value or false
				local Callback = meta.Callback or function()end

				local Toggle = Instance.new("Frame")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_1 = Instance.new("UIGradient")
				local IN_1 = Instance.new("Frame")
				local UIPadding_1 = Instance.new("UIPadding")
				local UIListLayout_1 = Instance.new("UIListLayout")
				local Icon_1 = Instance.new("Frame")
				local realicon_1 = Instance.new("ImageLabel")
				local Text_1 = Instance.new("Frame")
				local UIListLayout_2 = Instance.new("UIListLayout")
				local Title_1 = Instance.new("TextLabel")
				local Desc_1 = Instance.new("TextLabel")
				local check_1 = Instance.new("Frame")
				local true_1 = Instance.new("Frame")
				local UICorner_1 = Instance.new("UICorner")
				local UIGradient_2 = Instance.new("UIGradient")
				local trueicon_1 = Instance.new("ImageLabel")
				local ClickToggle = click(Toggle)

				layer(Toggle)

				local function Togglex(Value)
					if not Value then 
						Callback(Value)
						tw({
							v = true_1,
							t = 0.5,
							s = "Back",
							d = "Out",
							g = {BackgroundTransparency = 1}
						}):Play()
						tw({
							v = trueicon_1,
							t = 0.2,
							s = "Back",
							d = "Out",
							g = {Size = UDim2.new(0, 0,0, 0)}
						}):Play()
						tw({
							v = Title_1,
							t = 0.15,
							s = "Linear",
							d = "Out",
							g = {TextTransparency = 0.5}
						}):Play()
					elseif Value then 
						Callback(Value)
						tw({
							v = true_1,
							t = 0.5,
							s = "Back",
							d = "Out",
							g = {BackgroundTransparency = 0}
						}):Play()
						tw({
							v = trueicon_1,
							t = 0.1,
							s = "Bounce",
							d = "Out",
							g = {Size = UDim2.new(0, 21,0, 21)}
						}):Play()
						tw({
							v = Title_1,
							t = 0.15,
							s = "Linear",
							d = "Out",
							g = {TextTransparency = 0}
						}):Play()
						delay(0.05, function()
							tw({
								v = trueicon_1,
								t = 0.2,
								s = "Bounce",
								d = "Out",
								g = {Size = UDim2.new(0, 13,0, 13)}
							}):Play()
						end)
					end
				end

				Toggle.Name = "Toggle"
				Toggle.Parent = Section
				Toggle.AnchorPoint = Vector2.new(0.5, 0.5)
				Toggle.BackgroundColor3 = Color3.fromRGB(0,0,0)
				Toggle.BackgroundTransparency = 0.5
				Toggle.BorderColor3 = Color3.fromRGB(0,0,0)
				Toggle.BorderSizePixel = 0

				if Desc ~= "" or Icon ~= "" then
					Toggle.Size = UDim2.new(0.949999988, 0,0, 50)
				else
					Toggle.Size = UDim2.new(0.949999988, 0,0, 40)
				end
				Toggle.ClipsDescendants = true

				UIStroke_1.Parent = Toggle
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 1
				UIStroke_1.Transparency = 0.7

				UIGradient_1.Parent = UIStroke_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Rotation = 90

				IN_1.Name = "IN"
				IN_1.Parent = Toggle
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				IN_1.BackgroundTransparency = 1
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(1, 0,1, 0)

				UIPadding_1.Parent = IN_1
				UIPadding_1.PaddingLeft = UDim.new(0,5)

				UIListLayout_1.Parent = IN_1
				UIListLayout_1.FillDirection = Enum.FillDirection.Horizontal
				UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_1.VerticalAlignment = Enum.VerticalAlignment.Center

				if Icon ~= "" then
					UIListLayout_1.Padding = UDim.new(0,7)
					UIPadding_1.PaddingLeft = UDim.new(0,5)
					Icon_1.Name = "Icon"
					Icon_1.Parent = IN_1
					Icon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					Icon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Icon_1.BackgroundTransparency = 1
					Icon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Icon_1.BorderSizePixel = 0
					Icon_1.Position = UDim2.new(0.100000001, 0,0.5, 0)
					Icon_1.Size = UDim2.new(0, 40,0, 40)
					Icon_1.ZIndex = -3

					realicon_1.Name = "realicon"
					realicon_1.Parent = Icon_1
					realicon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					realicon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					realicon_1.BackgroundTransparency = 1
					realicon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					realicon_1.BorderSizePixel = 0
					realicon_1.Position = UDim2.new(0.5, 0,0.5, 0)
					realicon_1.Size = UDim2.new(0.899999976, 0,0.899999976, 0)
					realicon_1.Image = "rbxassetid://114522983600169"
				else
					UIPadding_1.PaddingLeft = UDim.new(0,10)
					UIListLayout_1.Padding = UDim.new(0,50)
				end

				Text_1.Name = "Text"
				Text_1.Parent = IN_1
				Text_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Text_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Text_1.BackgroundTransparency = 1
				Text_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Text_1.BorderSizePixel = 0
				Text_1.Position = UDim2.new(0.491390377, 0,0.5, 0)
				Text_1.Size = UDim2.new(0, 145,0, 40)

				UIListLayout_2.Parent = Text_1
				UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_2.VerticalAlignment = Enum.VerticalAlignment.Center

				Title_1.Name = "Title"
				Title_1.Parent = Text_1
				Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Title_1.BackgroundTransparency = 1
				Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Title_1.BorderSizePixel = 0
				Title_1.LayoutOrder = -3
				Title_1.Size = UDim2.new(0.899999976, 0,0, 15)
				Title_1.Font = Enum.Font.GothamBold
				Title_1.Text = Title
				Title_1.TextColor3 = Color3.fromRGB(255,255,255)
				Title_1.TextSize = 15
				Title_1.TextXAlignment = Enum.TextXAlignment.Left

				if Desc ~= "" then
					Desc_1.Name = "Desc"
					Desc_1.Parent = Text_1
					Desc_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Desc_1.BackgroundTransparency = 1
					Desc_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Desc_1.BorderSizePixel = 0
					Desc_1.LayoutOrder = -3
					Desc_1.Size = UDim2.new(0.899999976, 0,0, 15)
					Desc_1.Font = Enum.Font.GothamMedium
					Desc_1.Text = Desc
					Desc_1.TextColor3 = Color3.fromRGB(255,255,255)
					Desc_1.TextSize = 12
					Desc_1.TextTransparency = 0.5
					Desc_1.TextXAlignment = Enum.TextXAlignment.Left
				end

				check_1.Name = "check"
				check_1.Parent = IN_1
				check_1.AnchorPoint = Vector2.new(0.5, 0.5)
				check_1.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
				check_1.BackgroundTransparency = 0
				check_1.BorderColor3 = Color3.fromRGB(0,0,0)
				check_1.BorderSizePixel = 0
				check_1.Position = UDim2.new(0.882035494, 0,0.5, 0)
				check_1.Size = UDim2.new(0, 26,0, 26)

				true_1.Name = "true"
				true_1.Parent = check_1
				true_1.AnchorPoint = Vector2.new(0.5, 0.5)
				true_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				true_1.BorderColor3 = Color3.fromRGB(0,0,0)
				true_1.BorderSizePixel = 0
				true_1.Position = UDim2.new(0.5, 0,0.5, 0)
				true_1.Size = UDim2.new(1, 0,1, 0)

				UICorner_1.Parent = true_1
				UICorner_1.CornerRadius = UDim.new(0,4)

				local UICorner_2 = Instance.new("UICorner")
				UICorner_2.Parent = check_1
				UICorner_2.CornerRadius = UDim.new(0,4)

				UIGradient_2.Parent = true_1
				UIGradient_2.Color = GetColor()
				UIGradient_2.Rotation = 36

				trueicon_1.Name = "trueicon"
				trueicon_1.Parent = true_1
				trueicon_1.AnchorPoint = Vector2.new(0.5, 0.5)
				trueicon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				trueicon_1.BackgroundTransparency = 1
				trueicon_1.BorderColor3 = Color3.fromRGB(0,0,0)
				trueicon_1.BorderSizePixel = 0
				trueicon_1.Position = UDim2.new(0.5, 0,0.5, 0)
				trueicon_1.Size = UDim2.new(0.550000012, 0,0.550000012, 0)
				trueicon_1.Image = "rbxassetid://86682186031062"

				ClickToggle.MouseButton1Click:Connect(function()
					for _, v in pairs(Background_1:GetChildren()) do
						if v.Name == "Dropdown" and v.Visible then
							return
						end
					end
					EffectClick2(ClickToggle, Toggle)
					Value = not Value
					Togglex(Value)
				end)

				Togglex(Value)

				local Index = {}

				function Index:Title(v)
					Title_1 = v
				end

				function Index:Desc()
					Desc_1 = Desc
				end

				function Index:Value(v)
					Value = v
					Togglex(Value)
				end

				function Index:Icon(v)
					realicon_1.Image = GetIcon(v)
				end

				function Index:Visible(v)
					Toggle.Visible = v
				end

				return Index
			end

			function Env.Class:Dropdown(info)
				local Title = info.Title
				local Image = info.ListImage or false
				local IsPlayerList = info.IsPlayerList or false
				local List = info.List or {}
				local Value = info.Value
				local Multi = info.Multi or false
				local Callback = info.Callback
				local CallbackRefresh = info.CallbackRefresh

				local Dropdownz = Instance.new("Frame")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_1 = Instance.new("UIGradient")
				local IN_1 = Instance.new("Frame")
				local UIPadding_1 = Instance.new("UIPadding")
				local UIListLayout_1 = Instance.new("UIListLayout")
				local Icon_1 = Instance.new("Frame")
				local realicon_1 = Instance.new("ImageLabel")
				local Text_1 = Instance.new("Frame")
				local UIListLayout_2 = Instance.new("UIListLayout")
				local Title_1 = Instance.new("TextLabel")
				local Desc_1 = Instance.new("TextLabel")
				local Dropicon_1 = Instance.new("ImageLabel")
				local UIGradient_2 = Instance.new("UIGradient")
				local ClickDropdown = click(Dropdownz)
				layer(Dropdownz)

				Dropdownz.Name = "Dropdown"
				Dropdownz.Parent = Section
				Dropdownz.AnchorPoint = Vector2.new(0.5, 0.5)
				Dropdownz.BackgroundColor3 = Color3.fromRGB(0,0,0)
				Dropdownz.BackgroundTransparency = 0.5
				Dropdownz.BorderColor3 = Color3.fromRGB(0,0,0)
				Dropdownz.BorderSizePixel = 0
				Dropdownz.Size = UDim2.new(0.949999988, 0,0, 50)
				Dropdownz.ClipsDescendants = true

				UIStroke_1.Parent = Dropdownz
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 1
				UIStroke_1.Transparency = 0.7

				UIGradient_1.Parent = UIStroke_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Rotation = 90

				IN_1.Name = "IN"
				IN_1.Parent = Dropdownz
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				IN_1.BackgroundTransparency = 1
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(1, 0,1, 0)

				UIPadding_1.Parent = IN_1
				UIPadding_1.PaddingLeft = UDim.new(0,5)

				UIListLayout_1.Parent = IN_1
				UIListLayout_1.Padding = UDim.new(0,7)
				UIListLayout_1.FillDirection = Enum.FillDirection.Horizontal
				UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_1.VerticalAlignment = Enum.VerticalAlignment.Center

				if Icon ~= "" then
					UIPadding_1.PaddingLeft = UDim.new(0,5)
					UIListLayout_1.Padding = UDim.new(0,7)
					Icon_1.Name = "Icon"
					Icon_1.Parent = IN_1
					Icon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					Icon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Icon_1.BackgroundTransparency = 1
					Icon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Icon_1.BorderSizePixel = 0
					Icon_1.Position = UDim2.new(0.100000001, 0,0.5, 0)
					Icon_1.Size = UDim2.new(0, 40,0, 40)
					Icon_1.ZIndex = -3

					realicon_1.Name = "realicon"
					realicon_1.Parent = Icon_1
					realicon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					realicon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					realicon_1.BackgroundTransparency = 1
					realicon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					realicon_1.BorderSizePixel = 0
					realicon_1.Position = UDim2.new(0.5, 0,0.5, 0)
					realicon_1.Size = UDim2.new(0.899999976, 0,0.899999976, 0)
					realicon_1.Image = GetIcon(Icon)
				else
					UIPadding_1.PaddingLeft = UDim.new(0,10)
					UIListLayout_1.Padding = UDim.new(0,50)
				end

				Text_1.Name = "Text"
				Text_1.Parent = IN_1
				Text_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Text_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Text_1.BackgroundTransparency = 1
				Text_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Text_1.BorderSizePixel = 0
				Text_1.Position = UDim2.new(0.491390377, 0,0.5, 0)
				Text_1.Size = UDim2.new(0, 145,0, 40)

				UIListLayout_2.Parent = Text_1
				UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_2.VerticalAlignment = Enum.VerticalAlignment.Center

				Title_1.Name = "Title"
				Title_1.Parent = Text_1
				Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Title_1.BackgroundTransparency = 1
				Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Title_1.BorderSizePixel = 0
				Title_1.LayoutOrder = -3
				Title_1.Size = UDim2.new(0.899999976, 0,0, 15)
				Title_1.Font = Enum.Font.GothamBold
				Title_1.Text = Title
				Title_1.TextColor3 = Color3.fromRGB(255,255,255)
				Title_1.TextSize = 15
				Title_1.TextXAlignment = Enum.TextXAlignment.Left

				Desc_1.Name = "Desc"
				Desc_1.Parent = Text_1
				Desc_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Desc_1.BackgroundTransparency = 1
				Desc_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Desc_1.BorderSizePixel = 0
				Desc_1.LayoutOrder = -3
				Desc_1.Size = UDim2.new(0.899999976, 0,0, 15)
				Desc_1.Font = Enum.Font.GothamBold
				if type(Value) == "table" then
					if #Value > 3 then
						Desc_1.Text = "( . . . . . . )"
					else
						Desc_1.Text = table.concat(Value, ", ")
					end
				else
					Desc_1.Text = Value
				end
				Desc_1.TextColor3 = Color3.fromRGB(255,255,255)
				Desc_1.TextSize = 12
				Desc_1.TextXAlignment = Enum.TextXAlignment.Left

				local UIGradient_2z = Instance.new("UIGradient")
				UIGradient_2z.Parent = Desc_1
				UIGradient_2z.Color = GetColor()
				UIGradient_2z.Offset = Vector2.new(0, 0.00999999978)
				UIGradient_2z.Rotation = 90

				Dropicon_1.Name = "Dropicon"
				Dropicon_1.Parent = IN_1
				Dropicon_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Dropicon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Dropicon_1.BackgroundTransparency = 1
				Dropicon_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Dropicon_1.BorderSizePixel = 0
				Dropicon_1.Position = UDim2.new(0.5, 0,0.5, 0)
				Dropicon_1.Size = UDim2.new(0, 30,0, 30)
				Dropicon_1.Image = "rbxassetid://129573215183311"

				UIGradient_2.Parent = Dropicon_1
				UIGradient_2.Color = GetColor()
				UIGradient_2.Rotation = 90

				local function UpdateSelect()
					if type(Value) == "table" then
						Desc_1.Text = "( . . . )"
					else
						Desc_1.Text = Value
					end
				end

				local Dropdown = Instance.new("Frame")
				local DropShadow_1 = Instance.new("ImageLabel")
				local UIGradient_1 = Instance.new("UIGradient")
				local Head_1 = Instance.new("ImageLabel")
				local UIGradient_2 = Instance.new("UIGradient")
				local TextLabel_1 = Instance.new("TextLabel")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_3 = Instance.new("UIGradient")
				local Search_1 = Instance.new("Frame")
				local UICorner_1 = Instance.new("UICorner")
				local TextBox_1 = Instance.new("TextBox")
				local UIGradient_4 = Instance.new("UIGradient")
				local UIStroke_2 = Instance.new("UIStroke")
				local UIGradient_5 = Instance.new("UIGradient")
				local ScrollingFrame_1 = Instance.new("ScrollingFrame")
				local UIListLayout_1 = Instance.new("UIListLayout")
				local Refresh_1 = Instance.new("Frame")
				local i_2 = Instance.new("ImageLabel")
				local UIGradient_7 = Instance.new("UIGradient")
				local TextLabel_3 = Instance.new("TextLabel")
				local UIStroke_4 = Instance.new("UIStroke")

				local ClickRefresh = click(Refresh_1)

				Dropdown.Name = "Dropdown"
				Dropdown.Parent = Background_1
				Dropdown.AnchorPoint = Vector2.new(0.5, 0.5)
				Dropdown.BackgroundColor3 = Color3.fromRGB(0,0,0)
				Dropdown.BorderColor3 = Color3.fromRGB(0,0,0)
				Dropdown.BorderSizePixel = 0
				Dropdown.Position = UDim2.new(0.5, 0,0.516438365, 0)
				Dropdown.Size = UDim2.new(0, 250,0, 292)
				Dropdown.ZIndex = 3
				Dropdown.Visible = false

				DropShadow_1.Name = "DropShadow"
				DropShadow_1.Parent = Dropdown
				DropShadow_1.AnchorPoint = Vector2.new(0.5, 0.5)
				DropShadow_1.BackgroundColor3 = Color3.fromRGB(28,28,30)
				DropShadow_1.BackgroundTransparency = 1
				DropShadow_1.BorderColor3 = Color3.fromRGB(0,0,0)
				DropShadow_1.BorderSizePixel = 0
				DropShadow_1.Position = UDim2.new(0.5, 0,0.5, 0)
				DropShadow_1.Size = UDim2.new(1, 120,1, 120)
				DropShadow_1.ZIndex = 2
				DropShadow_1.Image = "rbxassetid://8992230677"
				DropShadow_1.ImageTransparency = 0.30000001192092896
				DropShadow_1.ScaleType = Enum.ScaleType.Slice
				DropShadow_1.SliceCenter = Rect.new(100, 100, 100, 100)

				UIGradient_1.Parent = DropShadow_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Rotation = 90

				Head_1.Name = "Head"
				Head_1.Parent = Dropdown
				Head_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Head_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Head_1.BackgroundTransparency = 1
				Head_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Head_1.BorderSizePixel = 0
				Head_1.Position = UDim2.new(0.482776254, 0,0.0223716833, 0)
				Head_1.Size = UDim2.new(0, 327,0, 97)
				Head_1.ZIndex = 3
				Head_1.Image = "rbxassetid://120486691266767"

				UIGradient_2.Parent = Head_1
				UIGradient_2.Color = GetColor()
				UIGradient_2.Rotation = -36

				TextLabel_1.Parent = Head_1
				TextLabel_1.AnchorPoint = Vector2.new(0.5, 0.5)
				TextLabel_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				TextLabel_1.BackgroundTransparency = 1
				TextLabel_1.BorderColor3 = Color3.fromRGB(0,0,0)
				TextLabel_1.BorderSizePixel = 0
				TextLabel_1.Position = UDim2.new(0.5, 0,0.458000004, 0)
				TextLabel_1.Size = UDim2.new(0.699999988, 0,0.285244763, 0)
				TextLabel_1.ZIndex = 3
				TextLabel_1.Font = Enum.Font.GothamBold
				TextLabel_1.Text = Title
				TextLabel_1.TextColor3 = Color3.fromRGB(255,255,255)
				TextLabel_1.TextSize = 21
				TextLabel_1.TextStrokeColor3 = Color3.fromRGB(52,52,52)
				TextLabel_1.TextStrokeTransparency = 0
				TextLabel_1.TextXAlignment = Enum.TextXAlignment.Left

				UIStroke_1.Parent = Dropdown
				UIStroke_1.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 2

				UIGradient_3.Parent = UIStroke_1
				UIGradient_3.Color = GetColor()
				UIGradient_3.Rotation = -36
				UIGradient_3.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0,0.5), NumberSequenceKeypoint.new(1,0.5)}

				Search_1.Name = "Search"
				Search_1.Parent = Dropdown
				Search_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Search_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Search_1.BackgroundTransparency = 0.5
				Search_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Search_1.BorderSizePixel = 0
				Search_1.Position = UDim2.new(0.5, 0,0.169, 0)
				Search_1.Size = UDim2.new(0.920000017, 0,0, 25)
				Search_1.ZIndex = 3

				UICorner_1.Parent = Search_1
				UICorner_1.CornerRadius = UDim.new(1,0)

				TextBox_1.Parent = Search_1
				TextBox_1.Active = true
				TextBox_1.AnchorPoint = Vector2.new(0.5, 0.5)
				TextBox_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				TextBox_1.BackgroundTransparency = 1
				TextBox_1.BorderColor3 = Color3.fromRGB(0,0,0)
				TextBox_1.BorderSizePixel = 0
				TextBox_1.Position = UDim2.new(0.5, 0,0.5, 0)
				TextBox_1.Size = UDim2.new(1, 0,1, 0)
				TextBox_1.ZIndex = 3
				TextBox_1.Font = Enum.Font.GothamBold
				TextBox_1.PlaceholderColor3 = Color3.fromRGB(178,178,178)
				TextBox_1.PlaceholderText = "Search"
				TextBox_1.Text = ""
				TextBox_1.TextColor3 = Color3.fromRGB(255,255,255)
				TextBox_1.TextSize = 14

				UIGradient_4.Parent = Search_1
				UIGradient_4.Color = GetColor()

				UIStroke_2.Parent = Search_1
				UIStroke_2.Color = Color3.fromRGB(255,255,255)
				UIStroke_2.Thickness = 1

				UIGradient_5.Parent = UIStroke_2
				UIGradient_5.Color = GetColor()

				ScrollingFrame_1.Name = "ScrollingFrame"
				ScrollingFrame_1.Parent = Dropdown
				ScrollingFrame_1.Active = true
				ScrollingFrame_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				ScrollingFrame_1.BackgroundTransparency = 1
				ScrollingFrame_1.BorderColor3 = Color3.fromRGB(0,0,0)
				ScrollingFrame_1.BorderSizePixel = 0
				ScrollingFrame_1.Position = UDim2.new(0.0500000007, 0,0.251078993, 0)
				ScrollingFrame_1.Size = UDim2.new(0.899999976, 0,0.6677472, 0)
				ScrollingFrame_1.ZIndex = 3
				ScrollingFrame_1.ClipsDescendants = true
				ScrollingFrame_1.AutomaticCanvasSize = Enum.AutomaticSize.None
				ScrollingFrame_1.BottomImage = "rbxasset://textures/ui/Scroll/scroll-bottom.png"
				ScrollingFrame_1.CanvasPosition = Vector2.new(0, 0)
				ScrollingFrame_1.ElasticBehavior = Enum.ElasticBehavior.WhenScrollable
				ScrollingFrame_1.HorizontalScrollBarInset = Enum.ScrollBarInset.None
				ScrollingFrame_1.MidImage = "rbxasset://textures/ui/Scroll/scroll-middle.png"
				ScrollingFrame_1.ScrollBarImageColor3 = Color3.fromRGB(0,0,0)
				ScrollingFrame_1.ScrollBarImageTransparency = 1
				ScrollingFrame_1.ScrollBarThickness = 0
				ScrollingFrame_1.ScrollingDirection = Enum.ScrollingDirection.XY
				ScrollingFrame_1.TopImage = "rbxasset://textures/ui/Scroll/scroll-top.png"
				ScrollingFrame_1.VerticalScrollBarInset = Enum.ScrollBarInset.None
				ScrollingFrame_1.VerticalScrollBarPosition = Enum.VerticalScrollBarPosition.Right

				UIListLayout_1.Parent = ScrollingFrame_1
				UIListLayout_1.Padding = UDim.new(0,5)
				UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder

				Refresh_1.Name = "Refresh"
				Refresh_1.Parent = Dropdown
				Refresh_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Refresh_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Refresh_1.BackgroundTransparency = 1
				Refresh_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Refresh_1.BorderSizePixel = 0
				Refresh_1.Position = UDim2.new(0.5, 0,0.985000014, 0)
				Refresh_1.Size = UDim2.new(0.6, 0,0.2, 0)
				Refresh_1.ZIndex = 4

				i_2.Name = "i"
				i_2.Parent = Refresh_1
				i_2.AnchorPoint = Vector2.new(0.5, 0.5)
				i_2.BackgroundColor3 = Color3.fromRGB(255,255,255)
				i_2.BackgroundTransparency = 1
				i_2.BorderColor3 = Color3.fromRGB(0,0,0)
				i_2.BorderSizePixel = 0
				i_2.Position = UDim2.new(0.5, 0,0.5, 0)
				i_2.Size = UDim2.new(0.800000012, 0,0.699999988, 0)
				i_2.ZIndex = 3
				i_2.Image = "rbxassetid://107541348612338"

				UIGradient_7.Parent = i_2
				UIGradient_7.Color = GetColor()
				UIGradient_7.Rotation = 94

				TextLabel_3.Parent = i_2
				TextLabel_3.AnchorPoint = Vector2.new(0.5, 0.5)
				TextLabel_3.BackgroundColor3 = Color3.fromRGB(255,255,255)
				TextLabel_3.BackgroundTransparency = 1
				TextLabel_3.BorderColor3 = Color3.fromRGB(0,0,0)
				TextLabel_3.BorderSizePixel = 0
				TextLabel_3.Position = UDim2.new(0.5, 0,0.5, 0)
				TextLabel_3.Size = UDim2.new(1, 0,1, 0)
				TextLabel_3.ZIndex = 3
				TextLabel_3.Font = Enum.Font.GothamBold
				TextLabel_3.Text = "Refresh"
				TextLabel_3.TextColor3 = Color3.fromRGB(255,255,255)
				TextLabel_3.TextSize = 17

				UIStroke_4.Parent = TextLabel_3
				UIStroke_4.Color = Color3.fromRGB(63,63,63)
				UIStroke_4.Thickness = 1


				local isOpen = false
				UserInputService.InputBegan:Connect(function(A)
					if A.UserInputType == Enum.UserInputType.MouseButton1 or A.UserInputType == Enum.UserInputType.Touch then
						local mouse = game:GetService("Players").LocalPlayer:GetMouse()
						local mx, my = mouse.X, mouse.Y

						local DBP, DBS = Dropdown.AbsolutePosition, Dropdown.AbsoluteSize
						local TBP, TBS = TextBox_1.AbsolutePosition, TextBox_1.AbsoluteSize
						local SBP, SBS = Search_1.AbsolutePosition, Search_1.AbsoluteSize
						local RBP, RBS = Refresh_1.AbsolutePosition, Refresh_1.AbsoluteSize

						local function inside(pos, size)
							return mx >= pos.X and mx <= pos.X + size.X and my >= pos.Y and my <= pos.Y + size.Y
						end

						if not inside(DBP, DBS)
							and not inside(TBP, TBS)
							and not inside(SBP, SBS)
							and not inside(RBP, RBS) then
							isOpen = false
							Dropdown.Size = UDim2.new(0, 0, 0, 0)
							Dropdown.Visible = false
						end
					end
				end)

				ClickDropdown.MouseButton1Click:Connect(function()
					
					for _, v in pairs(Background_1:GetChildren()) do
						if v.Name == "Dropdown" and v.Visible then
							return
						end
					end
					
					isOpen = not isOpen
					if isOpen then
						Dropdown.Visible = true
						tw({
							v = Dropdown,
							t = 0.3,
							s = "Back",
							d = "Out",
							g = {Size = UDim2.new(0, 250,0, 292)}
						}):Play()
					else
						tw({
							v = Dropdown,
							t = 0.3,
							s = "Bounce",
							d = "Out",
							g = {Size = UDim2.new(0, 0,0, 0)}
						}):Play()
						Dropdown.Visible = false
					end
					EffectClick2(ClickDropdown, Dropdownz)
					tw({
						v = Dropicon_1,
						t = 0.15,
						s = "Bounce",
						d = "Out",
						g = {Size = UDim2.new(0, 40,0, 40)}
					}):Play()
					delay(0.06, function()
						tw({
							v = Dropicon_1,
							t = 0.15,
							s = "Bounce",
							d = "Out",
							g = {Size = UDim2.new(0, 30,0, 30)}
						}):Play()
					end)
				end)

				TextBox_1.Changed:Connect(function()
					local SearchT = string.lower(TextBox_1.Text)
					for i, v in pairs(ScrollingFrame_1:GetChildren()) do
						if v:IsA("Frame") then
							local labelText = string.lower(v.Real.Title.Text)
							if string.find(labelText, SearchT, 1, true) then
								v.Visible = true
							else
								v.Visible = false
							end
						end
					end
				end)

				local itemslist = {}
				local selectedItem

				function itemslist:Clear(a)
					local function shouldClear(v)
						if a == nil then
							return true
						elseif type(a) == "string" then
							return v.Real:FindFirstChild("Title") and v.Real.Title.Text == a
						elseif type(a) == "table" then
							for _, name in ipairs(a) do
								if v.Real:FindFirstChild("Title") and v.Real.Title.Text == name then
									return true
								end
							end
						end
						return false
					end

					for _, v in ipairs(ScrollingFrame_1:GetChildren()) do
						if v:IsA("Frame") and shouldClear(v) then
							if selectedItem and v.Real:FindFirstChild("Title") and v.Real.Title.Text == selectedItem then
								selectedItem = nil
								Desc_1.Text = ""
							end
							v:Destroy()
						end
					end

					if selectedItem == a or Desc_1.Text == a then
						selectedItem = nil
						Desc_1.Text = ""
					end

					if a == nil then
						selectedItem = nil
						Desc_1.Text = ""
					end
				end

				local selectedValues = {}

				local function isValueInTable(val, tbl)
					if type(tbl) ~= "table" then
						return false
					end

					for _, v in pairs(tbl) do
						if v == val then
							return true
						end
					end
					return false
				end

				function itemslist:AddList(text, image)
					if Image then
						local Items = Instance.new("Frame")
						local UIGradient_1 = Instance.new("UIGradient")
						local Real_1 = Instance.new("Frame")
						local Title_1 = Instance.new("TextLabel")
						local Line_1 = Instance.new("Frame")
						local UIGradient_2 = Instance.new("UIGradient")
						local UICorner_1 = Instance.new("UICorner")
						local Iconss_1 = Instance.new("ImageLabel")
						local UIListLayout_1 = Instance.new("UIListLayout")
						local ClickList = click(Items)

						Items.Name = "Items"
						Items.Parent = ScrollingFrame_1
						Items.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Items.BackgroundTransparency = 1
						Items.BorderColor3 = Color3.fromRGB(0,0,0)
						Items.BorderSizePixel = 0
						Items.Size = UDim2.new(1, 0,0, 50)
						Items.ZIndex = 3

						UIGradient_1.Parent = Items
						UIGradient_1.Color = GetColor()

						Real_1.Name = "Real"
						Real_1.Parent = Items
						Real_1.AnchorPoint = Vector2.new(0.5, 0.5)
						Real_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Real_1.BackgroundTransparency = 1
						Real_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Real_1.BorderSizePixel = 0
						Real_1.Position = UDim2.new(0.5, 0,0.5, 0)
						Real_1.Size = UDim2.new(1, 0,1, 0)
						Real_1.ZIndex = 3

						Title_1.Name = "Title"
						Title_1.Parent = Real_1
						Title_1.AnchorPoint = Vector2.new(0.5, 0.5)
						Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Title_1.BackgroundTransparency = 1
						Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Title_1.BorderSizePixel = 0
						Title_1.LayoutOrder = -1
						Title_1.Position = UDim2.new(0.57476455, 0,0.5, 0)
						Title_1.Size = UDim2.new(0.660639942, 0,1, 0)
						Title_1.ZIndex = 3
						Title_1.Font = Enum.Font.GothamBold
						Title_1.Text = text
						Title_1.TextColor3 = Color3.fromRGB(255,255,255)
						Title_1.TextSize = 14
						Title_1.TextXAlignment = Enum.TextXAlignment.Left
						Title_1.TextTransparency = 0.5

						Line_1.Name = "Line"
						Line_1.Parent = Real_1
						Line_1.AnchorPoint = Vector2.new(0, 0.5)
						Line_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Line_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Line_1.BorderSizePixel = 0
						Line_1.LayoutOrder = -3
						Line_1.Position = UDim2.new(0, 0,0.5, 0)
						Line_1.Size = UDim2.new(0, 5,1, 0)
						Line_1.ZIndex = 3
						Line_1.BackgroundTransparency = 1

						UIGradient_2.Parent = Line_1
						UIGradient_2.Color = GetColor()
						UIGradient_2.Rotation = 90

						UICorner_1.Parent = Line_1
						UICorner_1.CornerRadius = UDim.new(1,0)

						Iconss_1.Name = "Iconss"
						Iconss_1.Parent = Real_1
						Iconss_1.AnchorPoint = Vector2.new(0, 0.5)
						Iconss_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Iconss_1.BackgroundTransparency = 1
						Iconss_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Iconss_1.BorderSizePixel = 0
						Iconss_1.LayoutOrder = -2
						Iconss_1.Position = UDim2.new(0, 0,0.5, 0)
						Iconss_1.Size = UDim2.new(0, 35,0, 35)
						Iconss_1.ZIndex = 3
						if IsPlayerList then
							Iconss_1.Image = game.Players:GetUserThumbnailAsync(image, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size420x420)
						else
							Iconss_1.Image = GetIcon(image)
						end
						Iconss_1.ImageTransparency = 0.5

						UIListLayout_1.Parent = Real_1
						UIListLayout_1.Padding = UDim.new(0,6)
						UIListLayout_1.FillDirection = Enum.FillDirection.Horizontal
						UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder
						UIListLayout_1.VerticalAlignment = Enum.VerticalAlignment.Center

						ClickList.MouseButton1Click:Connect(function()
							UpdateSelect()
							if Multi then
								if selectedValues[text] then
									selectedValues[text] = nil
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0.5}
									}):Play()
									tw({
										v = Iconss_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {ImageTransparency = 0.5}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 1}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 1}
									}):Play()

								else
									selectedValues[text] = true
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0}
									}):Play()
									tw({
										v = Iconss_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {ImageTransparency = 0}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0.85}
									}):Play()
								end
								local selectedList = {}
								for i, v in pairs(selectedValues) do
									table.insert(selectedList, i)
								end
								if #selectedList > 0 then
									UpdateSelect()
								else
									Desc_1.Text = ""
								end
								pcall(Callback, selectedList)
							else
								for i,v in pairs(ScrollingFrame_1:GetChildren()) do
									if v:IsA("Frame") then
										tw({
											v = v.Real.Title,
											t = 0.15,
											s = "Exponential",
											d = "Out",
											g = {TextTransparency = 0.5}
										}):Play()
										tw({
											v = v.Real.Line,
											t = 0.15,
											s = "Exponential",
											d = "Out",
											g = {BackgroundTransparency = 1}
										}):Play()
										tw({
											v = v.Real.Iconss,
											t = 0.15,
											s = "Exponential",
											d = "Out",
											g = {ImageTransparency = 0.5}
										}):Play()
										tw({
											v = v,
											t = 0.15,
											s = "Exponential",
											d = "Out",
											g = {BackgroundTransparency = 1}
										}):Play()
									end
								end
								tw({
									v = Iconss_1,
									t = 0.15,
									s = "Exponential",
									d = "Out",
									g = {ImageTransparency = 0}
								}):Play()
								tw({
									v = Title_1,
									t = 0.15,
									s = "Exponential",
									d = "Out",
									g = {TextTransparency = 0}
								}):Play()
								tw({
									v = Line_1,
									t = 0.15,
									s = "Exponential",
									d = "Out",
									g = {BackgroundTransparency = 0}
								}):Play()
								tw({
									v = Items,
									t = 0.15,
									s = "Exponential",
									d = "Out",
									g = {BackgroundTransparency = 0.85}
								}):Play()
								tw({
									v = Dropdown,
									t = 0.3,
									s = "Bounce",
									d = "Out",
									g = {Size = UDim2.new(0, 0,0, 0)}
								}):Play()
								isOpen = false
								Value = text
								Desc_1.Text = text
								pcall(function()
									Callback(Desc_1.Text)
								end)
								task.wait(0.05)
								Dropdown.Visible = false
							end
						end)

						delay(0,function()
							if Multi then
								if isValueInTable(text, Value) then
									tw({
										v = Iconss_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {ImageTransparency = 0}
									}):Play()
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0.85}
									}):Play()
									selectedValues[text] = true
									local selectedList = {}
									for i, v in pairs(selectedValues) do
										table.insert(selectedList, i)
									end
									if #selectedList > 0 then
										UpdateSelect()
									else
										Desc_1.Text = ""
									end
									pcall(Callback, selectedList)
								end
							else
								if text == Value then
									tw({
										v = Iconss_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {ImageTransparency = 0}
									}):Play()
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0.85}
									}):Play()
									Value = text
									Desc_1.Text = text
									Callback(Desc_1.Text)
								end
							end
						end)
					else
						local Items = Instance.new("Frame")
						local UIGradient_1 = Instance.new("UIGradient")
						local Real_1 = Instance.new("Frame")
						local Title_1 = Instance.new("TextLabel")
						local Line_1 = Instance.new("Frame")
						local UIGradient_2 = Instance.new("UIGradient")
						local UICorner_1 = Instance.new("UICorner")
						local ClickList = click(Items)

						Items.Name = "Items"
						Items.Parent = ScrollingFrame_1
						Items.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Items.BackgroundTransparency = 1
						Items.BorderColor3 = Color3.fromRGB(0,0,0)
						Items.BorderSizePixel = 0
						Items.Size = UDim2.new(1, 0,0, 30)
						Items.ZIndex = 3

						UIGradient_1.Parent = Items
						UIGradient_1.Color = GetColor()

						Real_1.Name = "Real"
						Real_1.Parent = Items
						Real_1.AnchorPoint = Vector2.new(0.5, 0.5)
						Real_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Real_1.BackgroundTransparency = 1
						Real_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Real_1.BorderSizePixel = 0
						Real_1.Position = UDim2.new(0.5, 0,0.5, 0)
						Real_1.Size = UDim2.new(1, 0,1, 0)
						Real_1.ZIndex = 3

						Title_1.Name = "Title"
						Title_1.Parent = Real_1
						Title_1.AnchorPoint = Vector2.new(0.5, 0.5)
						Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Title_1.BackgroundTransparency = 1
						Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Title_1.BorderSizePixel = 0
						Title_1.Position = UDim2.new(0.541989684, 0,0.5, 0)
						Title_1.Size = UDim2.new(0.916020691, 0,1, 0)
						Title_1.Font = Enum.Font.GothamBold
						Title_1.Text = tostring(text)
						Title_1.TextColor3 = Color3.fromRGB(255,255,255)
						Title_1.TextSize = 14
						Title_1.TextXAlignment = Enum.TextXAlignment.Left
						Title_1.TextTransparency = 0.5
						Title_1.ZIndex = 3

						Line_1.Name = "Line"
						Line_1.Parent = Real_1
						Line_1.AnchorPoint = Vector2.new(0, 0.5)
						Line_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
						Line_1.BorderColor3 = Color3.fromRGB(0,0,0)
						Line_1.BorderSizePixel = 0
						Line_1.Position = UDim2.new(0, 0,0.5, 0)
						Line_1.Size = UDim2.new(0, 5,0, 30)
						Line_1.BackgroundTransparency = 1
						Line_1.ZIndex = 3

						UIGradient_2.Parent = Line_1
						UIGradient_2.Color = GetColor()
						UIGradient_2.Rotation = 90

						UICorner_1.Parent = Line_1
						UICorner_1.CornerRadius = UDim.new(1,0)

						ClickList.MouseButton1Click:Connect(function()
							
							UpdateSelect()
							if Multi then
								if selectedValues[text] then
									selectedValues[text] = nil
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0.5}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 1}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 1}
									}):Play()
								else
									selectedValues[text] = true
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0.85}
									}):Play()
								end
								local selectedList = {}
								for i, v in pairs(selectedValues) do
									table.insert(selectedList, i)
								end
								if #selectedList > 0 then
									UpdateSelect()
								else
									Desc_1.Text = ""
								end
								pcall(Callback, selectedList)
							else
								for i,v in pairs(ScrollingFrame_1:GetChildren()) do
									if v:IsA("Frame") then
										tw({
											v = v.Real.Title,
											t = 0.15,
											s = "Exponential",
											d = "Out",
											g = {TextTransparency = 0.5}
										}):Play()
										tw({
											v = v.Real.Line,
											t = 0.15,
											s = "Exponential",
											d = "Out",
											g = {BackgroundTransparency = 1}
										}):Play()
										tw({
											v = v,
											t = 0.15,
											s = "Exponential",
											d = "Out",
											g = {BackgroundTransparency = 1}
										}):Play()
									end
								end

								tw({
									v = Title_1,
									t = 0.15,
									s = "Exponential",
									d = "Out",
									g = {TextTransparency = 0}
								}):Play()
								tw({
									v = Line_1,
									t = 0.15,
									s = "Exponential",
									d = "Out",
									g = {BackgroundTransparency = 0}
								}):Play()
								tw({
									v = Items,
									t = 0.15,
									s = "Exponential",
									d = "Out",
									g = {BackgroundTransparency = 0.85}
								}):Play()
								tw({
									v = Dropdown,
									t = 0.3,
									s = "Bounce",
									d = "Out",
									g = {Size = UDim2.new(0, 0,0, 0)}
								}):Play()
								isOpen = false
								Value = text
								Desc_1.Text = text
								pcall(function()
									Callback(Desc_1.Text)
								end)
								task.wait(0.05)
								Dropdown.Visible = false
							end
						end)

						delay(0,function()
							if Multi then
								if isValueInTable(text, Value) then
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0.85}
									}):Play()
									selectedValues[text] = true
									local selectedList = {}
									for i, v in pairs(selectedValues) do
										table.insert(selectedList, i)
									end
									if #selectedList > 0 then
										UpdateSelect()
									else
										Desc_1.Text = ""
									end
									pcall(Callback, selectedList)
								end
							else
								if text == Value then
									tw({
										v = Title_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {TextTransparency = 0}
									}):Play()
									tw({
										v = Line_1,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0}
									}):Play()
									tw({
										v = Items,
										t = 0.15,
										s = "Exponential",
										d = "Out",
										g = {BackgroundTransparency = 0.85}
									}):Play()
									Value = text
									Desc_1.Text = text
									Callback(Desc_1.Text)
								end
							end
						end)
					end
					UpdateSelect()
				end

				if Image then
					if IsPlayerList then
						for _, item in ipairs(List) do
							local name = item[1]
							local userId = item[2]
							local thumbnail = game.Players:GetUserThumbnailAsync(userId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size420x420)
							itemslist:AddList(name, thumbnail)
						end
					else
						for _, item in ipairs(List) do
							local name = item[1]
							local assetId = item[2]
							itemslist:AddList(name, GetIcon(assetId))
						end
					end
				else
					for _, name in ipairs(List) do
						itemslist:AddList(name)
					end
				end

				UIListLayout_1:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
					ScrollingFrame_1.CanvasSize = UDim2.new(0, 0, 0, UIListLayout_1.AbsoluteContentSize.Y + 5)
				end)

				ClickRefresh.MouseButton1Click:Connect(function()
					CallbackRefresh()
					tw({
						v = Refresh_1,
						t = 0.2,
						s = "Back",
						d = "Out",
						g = {Size = UDim2.new(0.5, 0,0.1, 0)}
					}):Play()
					delay(0.05, function()
						tw({
							v = Refresh_1,
							t = 0.2,
							s = "Back",
							d = "Out",
							g = {Size = UDim2.new(0.6, 0,0.2, 0)}
						}):Play()
					end)
				end)

				return itemslist
			end

			function Env.Class:Slider(info)

				local Title = info.Title
				local Min = info.Min or 0
				local Max = info.Max or 100
				local Rounding = info.Rounding or 0
				local Value = info.Value or Min
				local Callback = info.CallBack or function() end

				local Slider = Instance.new("Frame")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_1 = Instance.new("UIGradient")
				local IN_1 = Instance.new("Frame")
				local Text_1 = Instance.new("Frame")
				local Title_1 = Instance.new("TextLabel")
				local Bar_1 = Instance.new("Frame")
				local UICorner_1 = Instance.new("UICorner")
				local Colorbar_1 = Instance.new("Frame")
				local UICorner_2 = Instance.new("UICorner")
				local UIGradient_2 = Instance.new("UIGradient")
				local valuetext_1 = Instance.new("TextLabel")
				local Slide = click(Bar_1)
				layer(Slider)

				Slider.Name = "Slider"
				Slider.Parent = Section
				Slider.AnchorPoint = Vector2.new(0.5, 0.5)
				Slider.BackgroundColor3 = Color3.fromRGB(0,0,0)
				Slider.BackgroundTransparency = 0.5
				Slider.BorderColor3 = Color3.fromRGB(0,0,0)
				Slider.BorderSizePixel = 0
				Slider.Size = UDim2.new(0.949999988, 0,0, 50)

				UIStroke_1.Parent = Slider
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 1
				UIStroke_1.Transparency = 0.7

				UIGradient_1.Parent = UIStroke_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Rotation = 90

				IN_1.Name = "IN"
				IN_1.Parent = Slider
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				IN_1.BackgroundTransparency = 1
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(1, 0,1, 0)

				Text_1.Name = "Text"
				Text_1.Parent = IN_1
				Text_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Text_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Text_1.BackgroundTransparency = 1
				Text_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Text_1.BorderSizePixel = 0
				Text_1.Position = UDim2.new(0.503192723, 0,0.31, 0)
				Text_1.Size = UDim2.new(1, 0,1, 0)

				Title_1.Name = "Title"
				Title_1.Parent = Text_1
				Title_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Title_1.BackgroundTransparency = 1
				Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Title_1.BorderSizePixel = 0
				Title_1.LayoutOrder = -3
				Title_1.Position = UDim2.new(0.5, 0,0.5, 0)
				Title_1.Size = UDim2.new(1, 0,1, 0)
				Title_1.Font = Enum.Font.GothamBold
				Title_1.Text = Title
				Title_1.TextColor3 = Color3.fromRGB(255,255,255)
				Title_1.TextSize = 15

				Bar_1.Name = "Bar"
				Bar_1.Parent = IN_1
				Bar_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Bar_1.BackgroundColor3 = Color3.fromRGB(49,49,49)
				Bar_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Bar_1.BorderSizePixel = 0
				Bar_1.Position = UDim2.new(0.5, 0,0.75, 0)
				Bar_1.Size = UDim2.new(0.899999976, 0,0, 15)

				UICorner_1.Parent = Bar_1
				UICorner_1.CornerRadius = UDim.new(1,0)

				Colorbar_1.Name = "Colorbar"
				Colorbar_1.Parent = Bar_1
				Colorbar_1.AnchorPoint = Vector2.new(0, 0.5)
				Colorbar_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Colorbar_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Colorbar_1.BorderSizePixel = 0
				Colorbar_1.Position = UDim2.new(0, 0,0.5, 0)
				Colorbar_1.Size = UDim2.new(1, 0,1, 0)

				UICorner_2.Parent = Colorbar_1
				UICorner_2.CornerRadius = UDim.new(1,0)

				UIGradient_2.Parent = Colorbar_1
				UIGradient_2.Color = GetColor()

				valuetext_1.Name = "valuetext"
				valuetext_1.Parent = Bar_1
				valuetext_1.AnchorPoint = Vector2.new(0.5, 0.5)
				valuetext_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				valuetext_1.BackgroundTransparency = 1
				valuetext_1.BorderColor3 = Color3.fromRGB(0,0,0)
				valuetext_1.BorderSizePixel = 0
				valuetext_1.Position = UDim2.new(0.5, 0,0.5, 0)
				valuetext_1.Size = UDim2.new(1, 0,0, 5)
				valuetext_1.Font = Enum.Font.GothamBold
				valuetext_1.Text = Value
				valuetext_1.TextColor3 = Color3.fromRGB(255,255,255)
				valuetext_1.TextSize = 12
				valuetext_1.TextStrokeTransparency = 0.5

				local function roundToDecimal(value, decimals)
					local factor = 10 ^ decimals
					return math.floor(value * factor + 0.5) / factor
				end

				local function updateSlider(value)
					value = math.clamp(value, Min, Max)
					value = roundToDecimal(value, Rounding)
					tw({
						v = Colorbar_1,
						t = 0.15,
						s = "Exponential",
						d = "Out",
						g = {Size = UDim2.new((value - Min) / (Max - Min), 0, 1, 0)}
					}):Play()
					local startValue = tonumber(valuetext_1.Text) or 0
					local targetValue = value

					local steps = 5
					local currentValue = startValue
					for i = 1, steps do
						task.wait(0.01 / steps)
						currentValue = currentValue + (targetValue - startValue) / steps
						valuetext_1.Text = tostring(roundToDecimal(currentValue, Rounding))
					end

					valuetext_1.Text = tostring(roundToDecimal(targetValue, Rounding))

					Callback(value)
				end

				updateSlider(Value or 0)

				local function move(input)
					local sliderBar = Bar_1
					local relativeX = math.clamp((input.Position.X - sliderBar.AbsolutePosition.X) / sliderBar.AbsoluteSize.X, 0, 1)
					local value = relativeX * (Max - Min) + Min
					if Colorbar_1.Size.X.Scale < 0.5 then
						tw({
							v = valuetext_1,
							t = 0.1,
							s = "Bounce",
							d = "Out",
							g = {Rotation = -15}
						}):Play()
					else
						tw({
							v = valuetext_1,
							t = 0.1,
							s = "Bounce",
							d = "Out",
							g = {Rotation = 15}
						}):Play()
					end
					updateSlider(value)
				end

				local dragging = false

				Slide.InputBegan:Connect(function(input)
					for _, v in pairs(Background_1:GetChildren()) do
						if v.Name == "Dropdown" and v.Visible then
							return
						end
					end
					if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
						dragging = true
						valuetext_1.TextSize = 33
						move(input)
					end
				end)

				Slide.InputEnded:Connect(function(input)
					for _, v in pairs(Background_1:GetChildren()) do
						if v.Name == "Dropdown" and v.Visible then
							return
						end
					end
					if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
						valuetext_1.TextSize = 12
						tw({
							v = valuetext_1,
							t = 0.3,
							s = "Bounce",
							d = "Out",
							g = {Rotation = 0}
						}):Play()
						dragging = false
					end
				end)

				UserInputService.InputChanged:Connect(function(input)
					for _, v in pairs(Background_1:GetChildren()) do
						if v.Name == "Dropdown" and v.Visible then
							return
						end
					end
					if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
						move(input)
					end
				end)

				local NewValue = {}

				function NewValue:Value(a)
					Value = a
					updateSlider(Value)
				end

				function NewValue:Visible(a)
					Slider.Visible = a
				end

				function NewValue:Title(b)
					Title_1.Text = b
				end

				return NewValue
			end

			function Env.Class:Textbox(meta)
				local Value = meta.Value or "Example"
				local PlaceHolder = meta.PlaceHolder or "Place"
				local ClearOnFocus = meta.ClearOnFocus or false
				local Callback = meta.Callback

				local Textbox = Instance.new("Frame")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_1 = Instance.new("UIGradient")
				local UIStroke_1xx = Instance.new("UIStroke")
				local UIGradient_1xx = Instance.new("UIGradient")
				local IN_1 = Instance.new("Frame")
				local TextBox_1 = Instance.new("TextBox")
				layer(Textbox)

				Textbox.Name = "Textbox"
				Textbox.Parent = Section
				Textbox.AnchorPoint = Vector2.new(0.5, 0.5)
				Textbox.BackgroundColor3 = Color3.fromRGB(0,0,0)
				Textbox.BackgroundTransparency = 0.5
				Textbox.BorderColor3 = Color3.fromRGB(0,0,0)
				Textbox.BorderSizePixel = 0
				Textbox.Size = UDim2.new(0.949999988, 0,0, 40)

				UIStroke_1.Parent = Textbox
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 1
				UIStroke_1.Transparency = 0.7

				UIGradient_1.Parent = UIStroke_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Rotation = 90

				IN_1.Name = "IN"
				IN_1.Parent = Textbox
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
				IN_1.BackgroundTransparency = 0.30000001192092896
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(0.949999988, 0,0.600000024, 0)

				TextBox_1.Parent = IN_1
				TextBox_1.Active = true
				TextBox_1.AnchorPoint = Vector2.new(0.5, 0.5)
				TextBox_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				TextBox_1.BackgroundTransparency = 1
				TextBox_1.BorderColor3 = Color3.fromRGB(0,0,0)
				TextBox_1.BorderSizePixel = 0
				TextBox_1.CursorPosition = -1
				TextBox_1.Position = UDim2.new(0.5, 0,0.5, 0)
				TextBox_1.Size = UDim2.new(1, 0,1, 0)
				TextBox_1.ClipsDescendants = true
				TextBox_1.Font = Enum.Font.GothamBold
				TextBox_1.PlaceholderColor3 = Color3.fromRGB(178,178,178)
				TextBox_1.PlaceholderText = PlaceHolder
				TextBox_1.Text = Value
				TextBox_1.TextColor3 = Color3.fromRGB(255,255,255)
				TextBox_1.TextSize = 13

				UIStroke_1xx.Parent = IN_1
				UIStroke_1xx.Color = Color3.fromRGB(255,255,255)
				UIStroke_1xx.Thickness = 1
				UIStroke_1xx.Transparency = 0.7

				UIGradient_1xx.Parent = UIStroke_1xx
				UIGradient_1xx.Color = GetColor()

				TextBox_1.FocusLost:Connect(function()
					if #TextBox_1.Text > 0 then
						pcall(Callback, TextBox_1.Text)
					end
					tw({
						v = UIStroke_1xx,
						t = 0.3,
						s = "Back",
						d = "Out",
						g = {Transparency = 0.7}
					}):Play()
				end)

				TextBox_1.Focused:Connect(function()
					tw({
						v = UIStroke_1xx,
						t = 0.3,
						s = "Back",
						d = "Out",
						g = {Transparency = 0}
					}):Play()
				end)

				local Index = {}

				function Index:Value(v)
					Value = v
					Title_1.Text = v
				end

				function Index:Visible(v)
					Textbox.Visible = v
				end

				return Index
			end

			function Env.Class:AddFive()
				local FiveToggle = Instance.new("Frame")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_1 = Instance.new("UIGradient")
				local IN_1 = Instance.new("Frame")
				local UIListLayout_1 = Instance.new("UIListLayout")

				layer(FiveToggle)

				FiveToggle.Name = "FiveToggle"
				FiveToggle.Parent = Section
				FiveToggle.AnchorPoint = Vector2.new(0.5, 0.5)
				FiveToggle.BackgroundColor3 = Color3.fromRGB(0,0,0)
				FiveToggle.BackgroundTransparency = 0.5
				FiveToggle.BorderColor3 = Color3.fromRGB(0,0,0)
				FiveToggle.BorderSizePixel = 0
				FiveToggle.Size = UDim2.new(0.949999988, 0,0, 50)

				UIStroke_1.Parent = FiveToggle
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 1
				UIStroke_1.Transparency = 0.7

				UIGradient_1.Parent = UIStroke_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Rotation = 90

				IN_1.Name = "IN"
				IN_1.Parent = FiveToggle
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
				IN_1.BackgroundTransparency = 1
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(1, 0,1, 0)

				UIListLayout_1.Parent = IN_1
				UIListLayout_1.Padding = UDim.new(0,8)
				UIListLayout_1.FillDirection = Enum.FillDirection.Horizontal
				UIListLayout_1.HorizontalAlignment = Enum.HorizontalAlignment.Center
				UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_1.VerticalAlignment = Enum.VerticalAlignment.Center

				Env.Add = {}

				function Env.Add:Add(meta)
					local Template_1 = Instance.new("Frame")
					local UICorner_1 = Instance.new("UICorner")
					local In_1 = Instance.new("Frame")
					local UICorner_2 = Instance.new("UICorner")
					local UIGradient_2 = Instance.new("UIGradient")
					local ICon_1 = Instance.new("ImageLabel")

					local Icon = meta.Icon
					local Value = meta.Value or false
					local Callback = meta.Callback

					Template_1.Name = "Template"
					Template_1.Parent = IN_1
					Template_1.BackgroundColor3 = Color3.fromRGB(24,24,24)
					Template_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Template_1.BorderSizePixel = 0
					Template_1.Size = UDim2.new(0, 37,0, 37)
					local ClickToggle = click(Template_1)

					UICorner_1.Parent = Template_1
					UICorner_1.CornerRadius = UDim.new(0,5)

					In_1.Name = "In"
					In_1.Parent = Template_1
					In_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					In_1.BorderColor3 = Color3.fromRGB(0,0,0)
					In_1.BorderSizePixel = 0
					In_1.Size = UDim2.new(0, 37,0, 37)

					UICorner_2.Parent = In_1
					UICorner_2.CornerRadius = UDim.new(0,5)

					UIGradient_2.Parent = In_1
					UIGradient_2.Color = GetColor()
					UIGradient_2.Rotation = -29

					ICon_1.Name = "ICon"
					ICon_1.Parent = In_1
					ICon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					ICon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					ICon_1.BackgroundTransparency = 1
					ICon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					ICon_1.BorderSizePixel = 0
					ICon_1.Position = UDim2.new(0.5, 0,0.5, 0)
					ICon_1.Size = UDim2.new(0.600000024, 0,0.600000024, 0)
					ICon_1.Image = GetIcon(Icon)

					local function Togglex(Value)
						tw({
							v = ICon_1,
							t = 0.1,
							s = "Bounce",
							d = "Out",
							g = {Size = UDim2.new(0.5, 0,0.5, 0)}
						}):Play()
						delay(0.05, function()
							tw({
								v = ICon_1,
								t = 0.2,
								s = "Bounce",
								d = "Out",
								g = {Size = UDim2.new(0.600000024, 0,0.600000024, 0)}
							}):Play()
						end)
						if not Value then 
							Callback(Value)
							tw({
								v = In_1,
								t = 0.2,
								s = "Back",
								d = "Out",
								g = {BackgroundTransparency = 1}
							}):Play()
						elseif Value then 
							Callback(Value)
							tw({
								v = In_1,
								t = 0.2,
								s = "Back",
								d = "Out",
								g = {BackgroundTransparency = 0}
							}):Play()
						end
					end

					ClickToggle.MouseButton1Click:Connect(function()
						for _, v in pairs(Background_1:GetChildren()) do
							if v.Name == "Dropdown" and v.Visible then
								return
							end
						end
						Value = not Value
						Togglex(Value)
					end)

					Togglex(Value)

					local i = {}

					function i:Value(v)
						Value = v
						Togglex(v)
					end
					
					function i:Icon(v)
						ICon_1.Image = GetIcon(v)
					end

					return i
				end
				return Env.Add
			end

			function Env.Class:Discord(Link)
				local Discord = Instance.new("Frame")
				local IN_1 = Instance.new("Frame")
				local Close_1 = Instance.new("ImageLabel")
				local UIGradient_1 = Instance.new("UIGradient")
				local Icon_1 = Instance.new("ImageLabel")
				local TextLabel_1 = Instance.new("TextLabel")
				local UICorner_1 = Instance.new("UICorner")
				local ClickDiscord = click(Discord)			


				Discord.Name = "Discord"
				Discord.Parent = Section
				Discord.AnchorPoint = Vector2.new(0.5, 0.5)
				Discord.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Discord.BackgroundTransparency = 1
				Discord.BorderColor3 = Color3.fromRGB(0,0,0)
				Discord.BorderSizePixel = 0
				Discord.Size = UDim2.new(0.949999988, 0,0, 50)

				IN_1.Name = "IN"
				IN_1.Parent = Discord
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
				IN_1.BackgroundTransparency = 1
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(1, 0,1, 0)

				Close_1.Name = "Close"
				Close_1.Parent = IN_1
				Close_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Close_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Close_1.BackgroundTransparency = 1
				Close_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Close_1.BorderSizePixel = 0
				Close_1.Position = UDim2.new(0.5, 0,0.5, 0)
				Close_1.Size = UDim2.new(1, 0,1, 0)
				Close_1.Image = "rbxassetid://140569271063085"

				UIGradient_1.Parent = Close_1
				UIGradient_1.Color = ColorSequence.new{ColorSequenceKeypoint.new(0, Color3.fromRGB(88, 101, 242)), ColorSequenceKeypoint.new(1, Color3.fromRGB(142, 130, 255))}
				UIGradient_1.Rotation = 180

				TextLabel_1.Parent = Close_1
				TextLabel_1.AnchorPoint = Vector2.new(0.5, 0.5)
				TextLabel_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				TextLabel_1.BackgroundTransparency = 1
				TextLabel_1.BorderColor3 = Color3.fromRGB(0,0,0)
				TextLabel_1.BorderSizePixel = 0
				TextLabel_1.Position = UDim2.new(0.5, 0,0.469999999, 0)
				TextLabel_1.Size = UDim2.new(0.5, 0,0.560000002, 0)
				TextLabel_1.Font = Enum.Font.GothamBold
				TextLabel_1.Text = "Discord"
				TextLabel_1.TextColor3 = Color3.fromRGB(255,255,255)
				TextLabel_1.TextSize = 19
				TextLabel_1.TextStrokeTransparency = 0.5199999809265137

				UICorner_1.Parent = Discord
				UICorner_1.CornerRadius = UDim.new(0,5)

				ClickDiscord.MouseButton1Click:Connect(function()
					for _, v in pairs(Background_1:GetChildren()) do
						if v.Name == "Dropdown" and v.Visible then
							return
						end
					end
					pcall(setclipboard, tostring(Link))
					tw({
						v = IN_1,
						t = 0.15,
						s = "Bounce",
						d = "Out",
						g = {Size = UDim2.new(0.9, 0,0.9, 0)}
					}):Play()
					delay(0.05, function()
						tw({
							v = IN_1,
							t = 0.15,
							s = "Bounce",
							d = "Out",
							g = {Size = UDim2.new(1, 0,1, 0)}
						}):Play()
					end)
				end)
			end

			local function GetAlig(v)
				if v == 'l' then
					return Enum.TextXAlignment.Left
				elseif v == 'r' then
					return Enum.TextXAlignment.Right
				else
					return Enum.TextXAlignment.Center
				end
			end

			function Env.Class:Label(meta)

				local Title = meta.Title
				local Side = meta.Side

				local Label = Instance.new("TextLabel")
				Label.Name = "Label"
				Label.Parent = Section
				Label.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Label.BackgroundTransparency = 1
				Label.BorderColor3 = Color3.fromRGB(0,0,0)
				Label.BorderSizePixel = 0
				Label.Size = UDim2.new(0.92, 0,0, 20)
				Label.Font = Enum.Font.GothamBold
				Label.RichText = true
				Label.Text = Title
				Label.TextColor3 = Color3.fromRGB(255,255,255)
				Label.TextSize = 14
				Label.TextXAlignment = GetAlig(Side)

				local Index = {}

				function Index:Visible(v)
					Label.Visible = v
				end

				function Index:Title(a)
					Label.Text = a
				end

				return Index
			end

			function Env.Class:IconState(met)

				local Title = met.Title
				local Icon = met.Icon

				local Iconlabel = Instance.new("Frame")
				local IN_1 = Instance.new("Frame")
				local Icon_1 = Instance.new("ImageLabel")
				local Title_1 = Instance.new("TextLabel")
				local UIGradient_1 = Instance.new("UIGradient")
				local UICorner_1 = Instance.new("UICorner")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_2 = Instance.new("UIGradient")
				local ligh_1 = Instance.new("ImageLabel")
				local UIGradient_3 = Instance.new("UIGradient")
				local UICorner_2 = Instance.new("UICorner")
				Iconlabel.Name = "Iconlabel"
				Iconlabel.Parent = Section
				Iconlabel.AnchorPoint = Vector2.new(0.5, 0.5)
				Iconlabel.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Iconlabel.BackgroundTransparency = 1
				Iconlabel.BorderColor3 = Color3.fromRGB(0,0,0)
				Iconlabel.BorderSizePixel = 0
				Iconlabel.Size = UDim2.new(0.949999988, 0,0, 40)

				IN_1.Name = "IN"
				IN_1.Parent = Iconlabel
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(0,0,0)
				IN_1.BackgroundTransparency = 0.5
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(1, 0,1, 0)

				Icon_1.Name = "Icon"
				Icon_1.Parent = IN_1
				Icon_1.Active = true
				Icon_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Icon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Icon_1.BackgroundTransparency = 1
				Icon_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Icon_1.BorderSizePixel = 0
				Icon_1.Position = UDim2.new(0.100000001, 0,0.5, 0)
				Icon_1.Size = UDim2.new(0, 25,0, 25)
				Icon_1.Image = GetIcon(Icon)
				Icon_1.ScaleType = Enum.ScaleType.Crop

				Title_1.Name = "Title"
				Title_1.Parent = IN_1
				Title_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Title_1.BackgroundTransparency = 1
				Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Title_1.BorderSizePixel = 0
				Title_1.Position = UDim2.new(0.46661371, 0,0.5, 0)
				Title_1.Size = UDim2.new(0.56677258, 0,0.5, 0)
				Title_1.Font = Enum.Font.FredokaOne
				Title_1.Text = Title
				Title_1.TextColor3 = Color3.fromRGB(255,255,255)
				Title_1.TextSize = 15
				Title_1.TextStrokeTransparency = 0.5199999809265137
				Title_1.TextXAlignment = Enum.TextXAlignment.Left

				UIGradient_1.Parent = Title_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Offset = Vector2.new(0, 0.0500000007)
				UIGradient_1.Rotation = 90

				UICorner_1.Parent = IN_1
				UICorner_1.CornerRadius = UDim.new(1,0)

				UIStroke_1.Parent = IN_1
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 1

				UIGradient_2.Parent = UIStroke_1
				UIGradient_2.Color = GetColor()
				UIGradient_2.Rotation = 90

				ligh_1.Name = "ligh"
				ligh_1.Parent = IN_1
				ligh_1.AnchorPoint = Vector2.new(0.5, 0.5)
				ligh_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				ligh_1.BackgroundTransparency = 1
				ligh_1.BorderColor3 = Color3.fromRGB(0,0,0)
				ligh_1.BorderSizePixel = 0
				ligh_1.Position = UDim2.new(0.5, 0,0.5, 0)
				ligh_1.Size = UDim2.new(1, 0,1, 0)
				ligh_1.ClipsDescendants = true
				ligh_1.Image = "rbxassetid://300134974"
				ligh_1.ScaleType = Enum.ScaleType.Tile
				ligh_1.TileSize = UDim2.new(0.25, 0,1, 0)

				UIGradient_3.Parent = ligh_1
				UIGradient_3.Color = GetColor()
				UIGradient_3.Rotation = 90
				UIGradient_3.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0,0.85), NumberSequenceKeypoint.new(1,0.85)}

				UICorner_2.Parent = ligh_1
				UICorner_2.CornerRadius = UDim.new(1,0)

				local i ={}

				function i:Title(a)
					Title_1.Text = a
				end

				function i:Icon(a)
					Icon_1.Image = GetIcon(a)
				end
				
				function i:Visible(a)
					Iconlabel.Visible = a
				end

				return i
			end

			function Env.Class:ThumnailsImage(meta)
				local Banner = meta.Banner
				local Y = meta.SizeY or 150

				local Image = Instance.new("ImageLabel")
				Image.Name = "Image"
				Image.Parent = Section
				Image.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Image.BorderColor3 = Color3.fromRGB(0,0,0)
				Image.BackgroundTransparency = 1
				Image.BorderSizePixel = 0
				Image.Size = UDim2.new(0.95, 0,0, Y)
				Image.Image = GetIcon(Banner)
				Image.ScaleType = Enum.ScaleType.Crop

				local Index = {}

				function Index:Image(v)
					Image.Image = GetIcon(v)
				end

				function Index:Y(v)
					Image.Size = UDim2.new(0.97, 0,0, v)
				end

				function Index:Visible(v)
					Image.Visible = v
				end

				return Index
			end

			function Env.Class:Paragarp(meta)
				local Title = meta.Title or "for got title?"
				local Desc = meta.Desc or ""
				local Icon = meta.Icon or ""

				local Toggle = Instance.new("Frame")
				local UIStroke_1 = Instance.new("UIStroke")
				local UIGradient_1 = Instance.new("UIGradient")
				local IN_1 = Instance.new("Frame")
				local UIPadding_1 = Instance.new("UIPadding")
				local UIListLayout_1 = Instance.new("UIListLayout")
				local Icon_1 = Instance.new("Frame")
				local realicon_1 = Instance.new("ImageLabel")
				local Text_1 = Instance.new("Frame")
				local UIListLayout_2 = Instance.new("UIListLayout")
				local Title_1 = Instance.new("TextLabel")
				local Desc_1 = Instance.new("TextLabel")
				local ClickToggle = click(Toggle)
				
				layer(Toggle)

				Toggle.Name = "Paragarp"
				Toggle.Parent = Section
				Toggle.AnchorPoint = Vector2.new(0.5, 0.5)
				Toggle.BackgroundColor3 = Color3.fromRGB(0,0,0)
				Toggle.BackgroundTransparency = 0.5
				Toggle.BorderColor3 = Color3.fromRGB(0,0,0)
				Toggle.BorderSizePixel = 0
				Toggle.ClipsDescendants = true

				UIStroke_1.Parent = Toggle
				UIStroke_1.Color = Color3.fromRGB(255,255,255)
				UIStroke_1.Thickness = 1
				UIStroke_1.Transparency = 0.7

				UIGradient_1.Parent = UIStroke_1
				UIGradient_1.Color = GetColor()
				UIGradient_1.Rotation = 90

				IN_1.Name = "IN"
				IN_1.Parent = Toggle
				IN_1.AnchorPoint = Vector2.new(0.5, 0.5)
				IN_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				IN_1.BackgroundTransparency = 1
				IN_1.BorderColor3 = Color3.fromRGB(0,0,0)
				IN_1.BorderSizePixel = 0
				IN_1.Position = UDim2.new(0.5, 0,0.5, 0)
				IN_1.Size = UDim2.new(1, 0,1, 0)

				UIPadding_1.Parent = IN_1
				UIPadding_1.PaddingLeft = UDim.new(0,5)

				UIListLayout_1.Parent = IN_1
				UIListLayout_1.FillDirection = Enum.FillDirection.Horizontal
				UIListLayout_1.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_1.VerticalAlignment = Enum.VerticalAlignment.Center

				if Icon ~= "" then
					UIListLayout_1.Padding = UDim.new(0,7)
					UIPadding_1.PaddingLeft = UDim.new(0,5)
					Icon_1.Name = "Icon"
					Icon_1.Parent = IN_1
					Icon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					Icon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Icon_1.BackgroundTransparency = 1
					Icon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Icon_1.BorderSizePixel = 0
					Icon_1.Position = UDim2.new(0.100000001, 0,0.5, 0)
					Icon_1.Size = UDim2.new(0, 40,0, 40)
					Icon_1.ZIndex = -3

					realicon_1.Name = "realicon"
					realicon_1.Parent = Icon_1
					realicon_1.AnchorPoint = Vector2.new(0.5, 0.5)
					realicon_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					realicon_1.BackgroundTransparency = 1
					realicon_1.BorderColor3 = Color3.fromRGB(0,0,0)
					realicon_1.BorderSizePixel = 0
					realicon_1.Position = UDim2.new(0.5, 0,0.5, 0)
					realicon_1.Size = UDim2.new(0.899999976, 0,0.899999976, 0)
					realicon_1.Image = "rbxassetid://114522983600169"
					Text_1.Size = UDim2.new(0.8, 0,0, 40)
				else
					UIPadding_1.PaddingLeft = UDim.new(0,10)
					UIListLayout_1.Padding = UDim.new(0,50)
					Text_1.Size = UDim2.new(1, 0,0, 40)
				end

				Text_1.Name = "Text"
				Text_1.Parent = IN_1
				Text_1.AnchorPoint = Vector2.new(0.5, 0.5)
				Text_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Text_1.BackgroundTransparency = 1
				Text_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Text_1.BorderSizePixel = 0
				Text_1.Position = UDim2.new(0.491390377, 0,0.5, 0)


				UIListLayout_2.Parent = Text_1
				UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_2.VerticalAlignment = Enum.VerticalAlignment.Center

				Title_1.Name = "Title"
				Title_1.Parent = Text_1
				Title_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
				Title_1.BackgroundTransparency = 1
				Title_1.BorderColor3 = Color3.fromRGB(0,0,0)
				Title_1.BorderSizePixel = 0
				Title_1.LayoutOrder = -3
				Title_1.Size = UDim2.new(0.899999976, 0,0, 15)
				Title_1.Font = Enum.Font.GothamBold
				Title_1.Text = Title
				Title_1.TextColor3 = Color3.fromRGB(255,255,255)
				Title_1.TextSize = 15
				Title_1.TextXAlignment = Enum.TextXAlignment.Left
				Title_1.RichText = true

				if Desc ~= "" then
					Desc_1.Name = "Desc"
					Desc_1.Parent = Text_1
					Desc_1.BackgroundColor3 = Color3.fromRGB(255,255,255)
					Desc_1.BackgroundTransparency = 1
					Desc_1.BorderColor3 = Color3.fromRGB(0,0,0)
					Desc_1.BorderSizePixel = 0
					Desc_1.LayoutOrder = -3
					Desc_1.Size = UDim2.new(0.95, 0,0, 15)
					Desc_1.Font = Enum.Font.GothamMedium
					Desc_1.Text = Desc
					Desc_1.TextColor3 = Color3.fromRGB(255,255,255)
					Desc_1.TextSize = 12
					Desc_1.TextTransparency = 0.5
					Desc_1.TextXAlignment = Enum.TextXAlignment.Left
					Desc_1.RichText = true
					Desc_1.TextWrapped = true
				end

				if Desc ~= "" or Icon ~= "" then
					Toggle.Size = UDim2.new(0.949999988, 0,0, 50)
					local descHeight = Desc_1.TextBounds.Y + 5
					Desc_1.Size = UDim2.new(0.95, 0, 0, descHeight)
					Toggle.Size = UDim2.new(0.95, 0, 0, descHeight + 25)
				else
					Toggle.Size = UDim2.new(0.949999988, 0,0, 40)
				end

				local Index = {}

				function Index:Title(v)
					Title_1 = v
				end

				function Index:Desc()
					Desc_1 = Desc
					if Desc ~= "" or Icon ~= "" then
						local descHeight = Desc_1.TextBounds.Y + 5
						Desc_1.Size = UDim2.new(0.899999976, 0, 0, descHeight)
						Toggle.Size = UDim2.new(0.95, 0, 0, descHeight + 25)
					end
				end

				function Index:Icon(v)
					realicon_1.Image = GetIcon(v)
				end

				function Index:Visible(v)
					Toggle.Visible = v
				end

				return Index
			end

			return Env.Class
		end

		return Env.Section
	end
	return Env.Tabs
end
return Env
