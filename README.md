local Paragraph = {}
Paragraph.__index = Paragraph

function Paragraph.new(context: table)
	local self = setmetatable(context, Paragraph)
	return self
end

function Paragraph:renderParagraph()
	local paragraphLabel = Instance.new("TextLabel")
	paragraphLabel.Name = "Paragraph"
	paragraphLabel.Size = UDim2.new(1, 0, 0, 0)
	paragraphLabel.BackgroundTransparency = 1
	paragraphLabel.TextWrapped = true
	paragraphLabel.TextXAlignment = Enum.TextXAlignment.Left
	paragraphLabel.TextYAlignment = Enum.TextYAlignment.Top
	paragraphLabel.Font = Enum.Font.SourceSans
	paragraphLabel.TextSize = 16
	paragraphLabel.Text = self.Content or "No Content"
	paragraphLabel.AutomaticSize = Enum.AutomaticSize.Y
	
	if self.Title then
		local titleLabel = Instance.new("TextLabel")
		titleLabel.Name = "Title"
		titleLabel.Size = UDim2.new(1, 0, 0, 25)
		titleLabel.BackgroundTransparency = 1
		titleLabel.Font = Enum.Font.SourceSansBold
		titleLabel.TextSize = 18
		titleLabel.Text = self.Title
		titleLabel.TextXAlignment = Enum.TextXAlignment.Left
		titleLabel.TextYAlignment = Enum.TextYAlignment.Top

		titleLabel.Parent = self.Parent
	end

	paragraphLabel.Parent = self.Parent
	self.Paragraph = paragraphLabel
end

return Paragraph
