local redzlib = loadstring(game:HttpGet("https://raw.githubusercontent.com/tbao143/Library-ui/refs/heads/main/Redzhubui"))()

local Window = redzlib:MakeWindow({
    Title = "Matrix hub v4.2",
    SubTitle = "by Matrix Community",
    SaveFolder = "AmirHubConfigs"
})

Window:AddMinimizeButton({
    Button = { Image = "rbxassetid://85219327131493", BackgroundTransparency = 0 },
    Corner = { CornerRadius = UDim.new(35, 1) },
})

local Tab1 = Window:MakeTab({"Bem", "Vindo"})

local Paragraph = Tab1:AddParagraph({"CRÉDITOS", "OWNER: MINI PUMPKIN|DEVS: NOT LEGITTY, SOY EL TORRADA,SH|MEMBERS: ANGOLA DA SHOPY, CALEBITO39"})

local Tab1 = Window:MakeTab({"Fling", "v17"})

local Section = Tab1:AddSection({"Fling op"})

local Targets = {""} -- Nome será preenchido pela TextBox
local LoopAtivo = false

-- TextBox para capturar o nome do jogador e armazenar em Targets[1]
Tab1:AddTextBox({
  Name = "Player",
  Description = "", 
  PlaceholderText = "item only",
  Callback = function(Value)
Targets[1] = Value    
  end
})


local Toggle1 = Tab1:AddToggle({
  Name = "Fling",
  Description = "This is a <font color='rgb(88, 101, 242)'>Toggle</font> Example",
  Default = false 
})
Toggle1:Callback(function(Value)
 		if Value then
            -- Ativa o loop quando a toggle é ligada
            LoopAtivo = true
            task.spawn(function()
                while LoopAtivo do
                    local player = game.Players.LocalPlayer
 local mouse = player:GetMouse()
 local Targets = {Targets[1]}
 
 local Players = game:GetService("Players")
 local Player = Players.LocalPlayer
 
 local AllBool = false
 
 local GetPlayer = function(Name)
	Name = Name:lower()
	if Name == "all" or Name == "others" then
		AllBool = true
		return
	elseif Name == "random" then
		local GetPlayers = Players:GetPlayers()
		if table.find(GetPlayers,Player) then table.remove(GetPlayers,table.find(GetPlayers,Player)) end
		return GetPlayers[math.random(#GetPlayers)]
	elseif Name ~= "random" and Name ~= "all" and Name ~= "others" then
		for _,x in next, Players:GetPlayers() do
			if x ~= Player then
				if x.Name:lower():match("^"..Name) then
					return x;
				elseif x.DisplayName:lower():match("^"..Name) then
					return x;
				end
			end
		end
	else
		return
	end
 end
 
 local Message = function(_Title, _Text, Time)
	print(_Title)
	print(_Text)
	print(Time)
end

local SkidFling = function(TargetPlayer)
	local Character = Player.Character
	local Humanoid = Character and Character:FindFirstChildOfClass("Humanoid")
	local RootPart = Humanoid and Humanoid.RootPart
 
	local TCharacter = TargetPlayer.Character
	local THumanoid
	local TRootPart
	local THead
	local Accessory
	local Handle
 
	if TCharacter:FindFirstChildOfClass("Humanoid") then
		THumanoid = TCharacter:FindFirstChildOfClass("Humanoid")
	end
	if THumanoid and THumanoid.RootPart then
		TRootPart = THumanoid.RootPart
	end
	if TCharacter:FindFirstChild("Head") then
		THead = TCharacter.Head
	end
	if TCharacter:FindFirstChildOfClass("Accessory") then
		Accessory = TCharacter:FindFirstChildOfClass("Accessory")
	end
	if Accessoy and Accessory:FindFirstChild("Handle") then
		Handle = Accessory.Handle
	end
 
	if Character and Humanoid and RootPart then
		if RootPart.Velocity.Magnitude < 50 then
			getgenv().OldPos = RootPart.CFrame
		end
		if THumanoid and THumanoid.Sit and not AllBool then
		end
		if THead then
			workspace.CurrentCamera.CameraSubject = THead
		elseif not THead and Handle then
			workspace.CurrentCamera.CameraSubject = Handle
		elseif THumanoid and TRootPart then
			workspace.CurrentCamera.CameraSubject = THumanoid
		end
		if not TCharacter:FindFirstChildWhichIsA("BasePart") then
			return
		end
		
		local FPos = function(BasePart, Pos, Ang)
			RootPart.CFrame = CFrame.new(BasePart.Position) * Pos * Ang
			Character:SetPrimaryPartCFrame(CFrame.new(BasePart.Position) * Pos * Ang)
			RootPart.Velocity = Vector3.new(9e7, 9e7 * 10, 9e7)
			RootPart.RotVelocity = Vector3.new(9e8, 9e8, 9e8)
		end
		
		local SFBasePart = function(BasePart)
			local TimeToWait = 2
			local Time = tick()
			local Angle = 0
 
			repeat
				if RootPart and THumanoid then
					if BasePart.Velocity.Magnitude < 50 then
						Angle = Angle + 100
 
						FPos(BasePart, CFrame.new(0, 1.5, 0) + THumanoid.MoveDirection * BasePart.Velocity.Magnitude / 1.25, CFrame.Angles(math.rad(Angle),0 ,0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5, 0) + THumanoid.MoveDirection * BasePart.Velocity.Magnitude / 1.25, CFrame.Angles(math.rad(Angle), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(2.25, 1.5, -2.25) + THumanoid.MoveDirection * BasePart.Velocity.Magnitude / 1.25, CFrame.Angles(math.rad(Angle), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(-2.25, -1.5, 2.25) + THumanoid.MoveDirection * BasePart.Velocity.Magnitude / 1.25, CFrame.Angles(math.rad(Angle), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, 1.5, 0) + THumanoid.MoveDirection,CFrame.Angles(math.rad(Angle), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5, 0) + THumanoid.MoveDirection,CFrame.Angles(math.rad(Angle), 0, 0))
						task.wait()
					else
						FPos(BasePart, CFrame.new(0, 1.5, THumanoid.WalkSpeed), CFrame.Angles(math.rad(90), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5, -THumanoid.WalkSpeed), CFrame.Angles(0, 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, 1.5, THumanoid.WalkSpeed), CFrame.Angles(math.rad(90), 0, 0))
						task.wait()
						
						FPos(BasePart, CFrame.new(0, 1.5, TRootPart.Velocity.Magnitude / 1.25), CFrame.Angles(math.rad(90), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5, -TRootPart.Velocity.Magnitude / 1.25), CFrame.Angles(0, 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, 1.5, TRootPart.Velocity.Magnitude / 1.25), CFrame.Angles(math.rad(90), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5, 0), CFrame.Angles(math.rad(90), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5, 0), CFrame.Angles(0, 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5 ,0), CFrame.Angles(math.rad(-90), 0, 0))
						task.wait()
 
						FPos(BasePart, CFrame.new(0, -1.5, 0), CFrame.Angles(0, 0, 0))
						task.wait()
					end
				else
					break
				end
			until BasePart.Velocity.Magnitude > 500 or BasePart.Parent ~= TargetPlayer.Character or TargetPlayer.Parent ~= Players or not TargetPlayer.Character == TCharacter or THumanoid.Sit or Humanoid.Health <= 0 or tick() > Time + TimeToWait
		end
		
		workspace.FallenPartsDestroyHeight = 0/0
		
		local BV = Instance.new("BodyVelocity")
		BV.Name = "EpixVel"
		BV.Parent = RootPart
		BV.Velocity = Vector3.new(9e8, 9e8, 9e8)
		BV.MaxForce = Vector3.new(1/0, 1/0, 1/0)
		
		Humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, false)
		
		if TRootPart and THead then
			if (TRootPart.CFrame.p - THead.CFrame.p).Magnitude > 5 then
				SFBasePart(THead)
			else
				SFBasePart(TRootPart)
			end
		elseif TRootPart and not THead then
			SFBasePart(TRootPart)
		elseif not TRootPart and THead then
			SFBasePart(THead)
		elseif not TRootPart and not THead and Accessory and Handle then
			SFBasePart(Handle)
		else
		end
		
		BV:Destroy()
		Humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
		workspace.CurrentCamera.CameraSubject = Humanoid
	
		workspace.FallenPartsDestroyHeight = getgenv().FPDH
	else
	end
 end
 
 getgenv().Welcome = true
 if Targets[1] then for _,x in next, Targets do GetPlayer(x) end else return end
 
 if AllBool then
	for _,x in next, Players:GetPlayers() do
		SkidFling(x)
	end
 end
 
 for _,x in next, Targets do
	if GetPlayer(x) and GetPlayer(x) ~= Player then
		if GetPlayer(x).UserId ~= 1414978355 then
			local TPlayer = GetPlayer(x)
			if TPlayer then
				SkidFling(TPlayer)
			end
		else
		end
	elseif not GetPlayer(x) and not AllBool then
	end
 end
                    task.wait(0.1)
                end
            end)
        else
            -- Desativa o loop quando a toggle é desligada
            LoopAtivo = false
        end
end)


local Tab1 = Window:MakeTab({"BOOMBOX", "FE"})

Tab1:AddButton({"Print", function(Value)
        local player = game.Players.LocalPlayer
        local playerGui = player:FindFirstChild("PlayerGui")
        if not playerGui then return end -- Verifica se o jogador tem PlayerGui

        local boombox
        local sg
        local savedID = nil  -- Variável para armazenar o ID salvo
        local listFrame = {}  -- Tabela para controlar múltiplos frames da boombox

        -- Função para criar a Boombox
        local function createBoombox()
            boombox = Instance.new("Tool")
            boombox.Name = "Boombox"
            boombox.RequiresHandle = true
            boombox.Parent = player.Backpack

            local handle = Instance.new("Part")
            handle.Name = "Handle"
            handle.Size = Vector3.new(1, 1, 1)
            handle.CanCollide = false
            handle.Anchored = false
            handle.Transparency = 1
            handle.Parent = boombox

            -- Função para criar a GUI de música
            local function createGui()
                -- Verifica se já existe um frame da boombox
                if listFrame[player.UserId] then
                    return  -- Interrompe a criação da GUI se já existir
                end

                -- Marca que a GUI foi criada para esse jogador
                listFrame[player.UserId] = true

                sg = Instance.new("ScreenGui")
                sg.Name = "ChooseSongGui"
                sg.Parent = playerGui  

                local frame = Instance.new("Frame")
                frame.Style = "RobloxRound"
                frame.Size = UDim2.new(0.25, 0, 0.25, 0)
                frame.Position = UDim2.new((1-frame.Size.X.Scale)/2, 0, (1-frame.Size.Y.Scale)/2, 0)
                frame.Parent = sg
                frame.Draggable = true

                local text = Instance.new("TextLabel")
                text.BackgroundTransparency = 1
                text.TextStrokeTransparency = 0
                text.TextColor3 = Color3.new(1, 1, 1)
                text.Size = UDim2.new(1, 0, 0.6, 0)
                text.TextScaled = true
                text.Text = "Lay down the beat!\nPut in the ID number for a song you love that's been uploaded to ROBLOX.\nLeave it blank to stop playing music."
                text.Parent = frame

                local input = Instance.new("TextBox")
                input.BackgroundColor3 = Color3.new(0, 0, 0)
                input.BackgroundTransparency = 0.5
                input.BorderColor3 = Color3.new(1, 1, 1)
                input.TextColor3 = Color3.new(1, 1, 1)
                input.TextStrokeTransparency = 1
                input.TextScaled = true
                input.Text = savedID or "142376088"  -- Usar o ID salvo ou o padrão
                input.Size = UDim2.new(1, 0, 0.2, 0)
                input.Position = UDim2.new(0, 0, 0.6, 0)
                input.Parent = frame

                local button = Instance.new("TextButton")
                button.Style = "RobloxButton"
                button.Size = UDim2.new(0.75, 0, 0.2, 0)
                button.Position = UDim2.new(0.125, 0, 0.8, 0)
                button.TextColor3 = Color3.new(1, 1, 1)
                button.TextStrokeTransparency = 0
                button.Text = "Play!"
                button.TextScaled = true
                button.Parent = frame

                -- Função para tocar a música no servidor
                local function playAudioAll(ID)
                    if type(ID) ~= "number" then
                        print("Insira um número válido!")
                        return
                    end

                    local ReplicatedStorage = game:GetService("ReplicatedStorage")
                    local GunSoundEvent = ReplicatedStorage:FindFirstChild("1Gu1nSound1s", true)
                    if GunSoundEvent then
                        GunSoundEvent:FireServer(workspace, ID, 1)
                    end
                end

                -- Função para tocar a música localmente
                local function playAudioLocal(ID)
                    local sound = Instance.new("Sound")
                    sound.SoundId = "rbxassetid://" .. ID
                    sound.Volume = 1
                    sound.Looped = false
                    sound.Parent = player.Character or workspace
                    sound:Play()
                    task.wait(3)
                    sound:Destroy()
                end

                -- Função do botão "Play!"
                button.MouseButton1Click:Connect(function()
                    local soundID = tonumber(input.Text)
                    if soundID then
                        savedID = soundID  -- Salva o ID que foi inserido
                        playAudioAll(soundID) -- Toca para o servidor
                        playAudioLocal(soundID) -- Toca para você também
                    else
                        print("ID inválido!")
                    end

                    -- Remove a GUI instantaneamente
                    if sg then
                        sg:Destroy()
                        listFrame[player.UserId] = nil  -- Libera a GUI para futuras interações
                    end
                end)

            end

            -- Evento ao equipar a Boombox
            boombox.Equipped:Connect(function()
                -- Cria a GUI quando a Boombox é equipada, se ainda não existir
                if not listFrame[player.UserId] then
                    createGui()
                end

                -- Comando para equipar visualmente o Boombox no avatar
                local args = {
                    [1] = 1018548665  -- ID original
                }
                game:GetService("ReplicatedStorage").Remotes.Wear:InvokeServer(unpack(args))
            end)

            -- Evento ao desequipar a Boombox
            boombox.Unequipped:Connect(function()
                -- Remove a GUI quando o item for desequipado
                if sg then
                    sg:Destroy()
                    sg = nil
                end

                -- Comando para remover a Boombox visual do avatar
                local args = {
                    [1] = 1018548665  -- ID original
                }
                game:GetService("ReplicatedStorage").Remotes.Wear:InvokeServer(unpack(args))

                -- Libera a GUI para a criação de um novo frame caso o item seja re-equipado
                listFrame[player.UserId] = nil
            end)

            -- Evento para detectar se a Boombox foi deletada da mochila
            boombox.AncestryChanged:Connect(function(_, parent)
                if not parent and sg then
                    sg:Destroy()
                    sg = nil
                    listFrame[player.UserId] = nil  -- Permite criar a GUI novamente quando o item for removido
                end
            end)
        end

        -- Chama a função para criar a Boombox
        createBoombox()
    end("Hello World!")
end})
