-- Script VertexHUB AI Chat - Black & White Theme
-- Untuk Delta Executor (HP Optimized)
-- Guess My Country Edition

local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local player = Players.LocalPlayer

local API_URL = "https://api.groq.com/openai/v1/chat/completions"

-- Variabel
local currentAPIKey = ""
local isAuthenticated = false
local mainGui = nil
local loginGui = nil

-- ========== FUNGSI MEMBUAT LOGO DARI URL ==========
local function createLogoFromURL(parent, size, position)
    local logoContainer = Instance.new("Frame")
    logoContainer.Size = size
    logoContainer.Position = position
    logoContainer.BackgroundTransparency = 1
    logoContainer.Parent = parent
    
    -- Menggunakan ImageLabel dengan URL (jika didukung executor)
    local logoImage = Instance.new("ImageLabel")
    logoImage.Size = UDim2.new(1, 0, 1, 0)
    logoImage.BackgroundTransparency = 1
    logoImage.Image = "https://raw.githubusercontent.com/lionelbenayap1910-ctrl/vertexhub/31a7fe0907df11e6d34944582330db55f5d71054/file_00000000bb4c71fd8f7c25f3adda9f0a.png"
    logoImage.ScaleType = Enum.ScaleType.Fit
    logoImage.Parent = logoContainer
    
    return logoContainer
end

-- ========== FUNGSI VALIDASI API KEY ==========
local function validateAPIKey(apiKey)
    if not apiKey or apiKey == "" then
        return false, "API Key tidak boleh kosong!"
    end
    
    local headers = {
        ["Authorization"] = "Bearer " .. apiKey,
        ["Content-Type"] = "application/json"
    }
    
    local body = {
        messages = {{role = "user", content = "test"}},
        model = "llama-3.1-8b-instant",
        max_tokens = 5
    }
    
    local success, response = pcall(function()
        return HttpService:RequestAsync({
            Url = API_URL,
            Method = "POST",
            Headers = headers,
            Body = HttpService:JSONEncode(body),
            Timeout = 10
        })
    end)
    
    if not success then
        return false, "Gagal koneksi ke server!"
    end
    
    if response.Success and response.StatusCode == 200 then
        return true, "API Key Valid!"
    elseif response.StatusCode == 401 then
        return false, "API Key SALAH! Periksa kembali."
    else
        return false, "Error: " .. tostring(response.StatusCode)
    end
end

-- ========== LOGIN WINDOW (VERTEXHUB THEME) ==========
local function createLoginWindow()
    if loginGui then loginGui:Destroy() end
    if mainGui then mainGui:Destroy() end
    
    loginGui = Instance.new("ScreenGui")
    loginGui.Name = "VertexHUB_Login"
    loginGui.Parent = player:WaitForChild("PlayerGui")
    
    local screenSize = workspace.CurrentCamera.ViewportSize
    local frameWidth = math.min(340, screenSize.X - 40)
    local frameHeight = 520
    
    -- Frame utama
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, frameWidth, 0, frameHeight)
    frame.Position = UDim2.new(0.5, -frameWidth/2, 0.5, -frameHeight/2)
    frame.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
    frame.BorderSizePixel = 1
    frame.BorderColor3 = Color3.fromRGB(60, 60, 60)
    frame.Parent = loginGui
    
    local frameCorner = Instance.new("UICorner")
    frameCorner.CornerRadius = UDim.new(0, 20)
    frameCorner.Parent = frame
    
    -- Header dengan logo
    local header = Instance.new("Frame")
    header.Size = UDim2.new(1, 0, 0, 130)
    header.BackgroundColor3 = Color3.fromRGB(5, 5, 5)
    header.BorderSizePixel = 0
    header.Parent = frame
    
    -- Logo dari URL
    local logo = createLogoFromURL(header, UDim2.new(0, 80, 0, 80), UDim2.new(0.5, -40, 0, 15))
    
    -- Title
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, 0, 0, 22)
    title.Position = UDim2.new(0, 0, 0, 105)
    title.BackgroundTransparency = 1
    title.Text = "VERTEXHUB"
    title.TextColor3 = Color3.fromRGB(255, 255, 255)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 20
    title.Parent = header
    
    -- Subtitle
    local subtitle = Instance.new("TextLabel")
    subtitle.Size = UDim2.new(1, 0, 0, 15)
    subtitle.Position = UDim2.new(0, 0, 0, 125)
    subtitle.BackgroundTransparency = 1
    subtitle.Text = "Guess My Country • AI Assistant"
    subtitle.TextColor3 = Color3.fromRGB(150, 150, 150)
    subtitle.Font = Enum.Font.Gotham
    subtitle.TextSize = 10
    subtitle.Parent = header
    
    -- Form area
    local formFrame = Instance.new("Frame")
    formFrame.Size = UDim2.new(1, -30, 0, 200)
    formFrame.Position = UDim2.new(0, 15, 0, 145)
    formFrame.BackgroundTransparency = 1
    formFrame.Parent = frame
    
    -- Label
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, 0, 0, 25)
    label.Position = UDim2.new(0, 0, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = "GROQ API KEY"
    label.TextColor3 = Color3.fromRGB(180, 180, 180)
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Font = Enum.Font.GothamBold
    label.TextSize = 11
    label.Parent = formFrame
    
    -- Input box
    local inputBox = Instance.new("TextBox")
    inputBox.Size = UDim2.new(1, 0, 0, 45)
    inputBox.Position = UDim2.new(0, 0, 0, 30)
    inputBox.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
    inputBox.BorderSizePixel = 1
    inputBox.BorderColor3 = Color3.fromRGB(60, 60, 60)
    inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    inputBox.PlaceholderText = "gsk_xxxxxxxxxxxxxxxxxxxx"
    inputBox.PlaceholderColor3 = Color3.fromRGB(100, 100, 100)
    inputBox.Font = Enum.Font.Gotham
    inputBox.TextSize = 12
    inputBox.ClearTextOnFocus = true
    inputBox.Parent = formFrame
    
    local inputCorner = Instance.new("UICorner")
    inputCorner.CornerRadius = UDim.new(0, 10)
    inputCorner.Parent = inputBox
    
    -- Status label
    local statusLabel = Instance.new("TextLabel")
    statusLabel.Size = UDim2.new(1, 0, 0, 50)
    statusLabel.Position = UDim2.new(0, 0, 0, 85)
    statusLabel.BackgroundTransparency = 1
    statusLabel.Text = ""
    statusLabel.TextColor3 = Color3.fromRGB(255, 100, 100)
    statusLabel.TextSize = 11
    statusLabel.TextWrapped = true
    statusLabel.Parent = formFrame
    
    -- Button area
    local buttonFrame = Instance.new("Frame")
    buttonFrame.Size = UDim2.new(1, -30, 0, 100)
    buttonFrame.Position = UDim2.new(0, 15, 1, -130)
    buttonFrame.BackgroundTransparency = 1
    buttonFrame.Parent = frame
    
    -- Get Key Button
    local getKeyBtn = Instance.new("TextButton")
    getKeyBtn.Size = UDim2.new(1, 0, 0, 40)
    getKeyBtn.Position = UDim2.new(0, 0, 0, 0)
    getKeyBtn.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    getKeyBtn.BorderSizePixel = 1
    getKeyBtn.BorderColor3 = Color3.fromRGB(80, 80, 80)
    getKeyBtn.Text = "🔑 GET API KEY"
    getKeyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    getKeyBtn.Font = Enum.Font.GothamBold
    getKeyBtn.TextSize = 13
    getKeyBtn.Parent = buttonFrame
    
    local getKeyCorner = Instance.new("UICorner")
    getKeyCorner.CornerRadius = UDim.new(0, 10)
    getKeyCorner.Parent = getKeyBtn
    
    -- Login Button
    local loginBtn = Instance.new("TextButton")
    loginBtn.Size = UDim2.new(1, 0, 0, 45)
    loginBtn.Position = UDim2.new(0, 0, 0, 50)
    loginBtn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    loginBtn.BorderSizePixel = 1
    loginBtn.BorderColor3 = Color3.fromRGB(100, 100, 100)
    loginBtn.Text = "LOGIN"
    loginBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    loginBtn.Font = Enum.Font.GothamBold
    loginBtn.TextSize = 14
    loginBtn.Parent = buttonFrame
    
    local loginCorner = Instance.new("UICorner")
    loginCorner.CornerRadius = UDim.new(0, 10)
    loginCorner.Parent = loginBtn
    
    -- Info text
    local info = Instance.new("TextLabel")
    info.Size = UDim2.new(1, -30, 0, 35)
    info.Position = UDim2.new(0, 15, 1, -40)
    info.BackgroundTransparency = 1
    info.Text = "💡 Dapatkan API Key gratis di console.groq.com"
    info.TextColor3 = Color3.fromRGB(100, 100, 100)
    info.TextSize = 9
    info.TextWrapped = true
    info.Parent = frame
    
    -- Version text
    local version = Instance.new("TextLabel")
    version.Size = UDim2.new(1, 0, 0, 15)
    version.Position = UDim2.new(0, 0, 1, -20)
    version.BackgroundTransparency = 1
    version.Text = "VertexHUB v1.0 • Guess My Country"
    version.TextColor3 = Color3.fromRGB(80, 80, 80)
    version.TextSize = 8
    version.Parent = frame
    
    -- Fungsi Get Key
    local function openGroqKeys()
        if setclipboard then
            setclipboard("https://console.groq.com/keys")
            statusLabel.Text = "✅ Link disalin! Buka browser dan paste."
            statusLabel.TextColor3 = Color3.fromRGB(100, 255, 100)
            task.wait(2)
            statusLabel.Text = ""
        else
            statusLabel.Text = "⚠️ Buka manual: console.groq.com/keys"
            statusLabel.TextColor3 = Color3.fromRGB(255, 255, 100)
            task.wait(3)
            statusLabel.Text = ""
        end
    end
    
    -- Fungsi Login
    local function doLogin()
        local apiKey = inputBox.Text
        if apiKey == "" then
            statusLabel.Text = "❌ Masukkan API Key terlebih dahulu!"
            return
        end
        
        statusLabel.Text = "⏳ Memverifikasi API Key..."
        statusLabel.TextColor3 = Color3.fromRGB(255, 255, 100)
        loginBtn.Text = "VERIFYING..."
        loginBtn.Active = false
        
        local valid, msg = validateAPIKey(apiKey)
        
        if valid then
            currentAPIKey = apiKey
            isAuthenticated = true
            statusLabel.Text = "✅ " .. msg
            statusLabel.TextColor3 = Color3.fromRGB(100, 255, 100)
            task.wait(1)
            loginGui:Destroy()
            createChatUI()
        else
            statusLabel.Text = "❌ " .. msg
            statusLabel.TextColor3 = Color3.fromRGB(255, 100, 100)
            loginBtn.Text = "LOGIN"
            loginBtn.Active = true
            inputBox.Text = ""
        end
    end
    
    getKeyBtn.MouseButton1Click:Connect(openGroqKeys)
    loginBtn.MouseButton1Click:Connect(doLogin)
    inputBox.FocusLost:Connect(function(enter)
        if enter then doLogin() end
    end)
end

-- ========== CHAT UI (VERTEXHUB THEME) ==========
function createChatUI()
    if mainGui then mainGui:Destroy() end
    
    mainGui = Instance.new("ScreenGui")
    mainGui.Name = "VertexHUB_Chat"
    mainGui.Parent = player:WaitForChild("PlayerGui")
    
    local screenSize = workspace.CurrentCamera.ViewportSize
    local frameWidth = math.min(360, screenSize.X - 20)
    local frameHeight = math.min(540, screenSize.Y - 80)
    
    -- Frame utama
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, frameWidth, 0, frameHeight)
    frame.Position = UDim2.new(0.5, -frameWidth/2, 0.05, 0)
    frame.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
    frame.BorderSizePixel = 1
    frame.BorderColor3 = Color3.fromRGB(50, 50, 50)
    frame.Active = true
    frame.Draggable = true
    frame.ClipsDescendants = true
    frame.Parent = mainGui
    
    local frameCorner = Instance.new("UICorner")
    frameCorner.CornerRadius = UDim.new(0, 16)
    frameCorner.Parent = frame
    
    -- Title bar
    local titleBar = Instance.new("Frame")
    titleBar.Size = UDim2.new(1, 0, 0, 50)
    titleBar.BackgroundColor3 = Color3.fromRGB(5, 5, 5)
    titleBar.BorderSizePixel = 0
    titleBar.Parent = frame
    
    -- Logo kecil di title
    local titleLogo = Instance.new("ImageLabel")
    titleLogo.Size = UDim2.new(0, 28, 0, 28)
    titleLogo.Position = UDim2.new(0, 10, 0.5, -14)
    titleLogo.BackgroundTransparency = 1
    titleLogo.Image = "https://raw.githubusercontent.com/lionelbenayap1910-ctrl/vertexhub/31a7fe0907df11e6d34944582330db55f5d71054/file_00000000bb4c71fd8f7c25f3adda9f0a.png"
    titleLogo.ScaleType = Enum.ScaleType.Fit
    titleLogo.Parent = titleBar
    
    -- Title text
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, -90, 1, 0)
    title.Position = UDim2.new(0, 45, 0, 0)
    title.BackgroundTransparency = 1
    title.Text = "VertexHUB AI"
    title.TextColor3 = Color3.fromRGB(255, 255, 255)
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.Font = Enum.Font.GothamBold
    title.TextSize = 15
    title.Parent = titleBar
    
    -- Subtitle di title bar
    local titleSub = Instance.new("TextLabel")
    titleSub.Size = UDim2.new(1, -90, 0, 12)
    titleSub.Position = UDim2.new(0, 45, 1, -14)
    titleSub.BackgroundTransparency = 1
    titleSub.Text = "Guess My Country"
    titleSub.TextColor3 = Color3.fromRGB(120, 120, 120)
    titleSub.TextXAlignment = Enum.TextXAlignment.Left
    titleSub.Font = Enum.Font.Gotham
    titleSub.TextSize = 9
    titleSub.Parent = titleBar
    
    -- Status indicator
    local statusDot = Instance.new("Frame")
    statusDot.Size = UDim2.new(0, 8, 0, 8)
    statusDot.Position = UDim2.new(1, -50, 0.5, -4)
    statusDot.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
    statusDot.BorderSizePixel = 0
    statusDot.Parent = titleBar
    
    local dotCorner = Instance.new("UICorner")
    dotCorner.CornerRadius = UDim.new(1, 0)
    dotCorner.Parent = statusDot
    
    -- Close button
    local closeBtn = Instance.new("TextButton")
    closeBtn.Size = UDim2.new(0, 32, 1, -10)
    closeBtn.Position = UDim2.new(1, -38, 0, 5)
    closeBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    closeBtn.BorderSizePixel = 1
    closeBtn.BorderColor3 = Color3.fromRGB(80, 80, 80)
    closeBtn.Text = "✕"
    closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    closeBtn.Font = Enum.Font.GothamBold
    closeBtn.TextSize = 12
    closeBtn.Parent = titleBar
    
    local closeCorner = Instance.new("UICorner")
    closeCorner.CornerRadius = UDim.new(0, 8)
    closeCorner.Parent = closeBtn
    
    -- Chat area
    local chatFrame = Instance.new("ScrollingFrame")
    chatFrame.Size = UDim2.new(1, -12, 1, -115)
    chatFrame.Position = UDim2.new(0, 6, 0, 58)
    chatFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
    chatFrame.BorderSizePixel = 1
    chatFrame.BorderColor3 = Color3.fromRGB(45, 45, 45)
    chatFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
    chatFrame.ScrollBarThickness = 4
    chatFrame.ScrollBarImageColor3 = Color3.fromRGB(80, 80, 80)
    chatFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
    chatFrame.Parent = frame
    
    local chatCorner = Instance.new("UICorner")
    chatCorner.CornerRadius = UDim.new(0, 10)
    chatCorner.Parent = chatFrame
    
    local chatLayout = Instance.new("UIListLayout")
    chatLayout.Parent = chatFrame
    chatLayout.Padding = UDim.new(0, 8)
    
    -- Input area
    local inputBox = Instance.new("TextBox")
    inputBox.Size = UDim2.new(1, -80, 0, 44)
    inputBox.Position = UDim2.new(0, 6, 1, -50)
    inputBox.BackgroundColor3 = Color3.fromRGB(8, 8, 8)
    inputBox.BorderSizePixel = 1
    inputBox.BorderColor3 = Color3.fromRGB(60, 60, 60)
    inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    inputBox.PlaceholderText = "Ask VertexHUB AI..."
    inputBox.PlaceholderColor3 = Color3.fromRGB(100, 100, 100)
    inputBox.Font = Enum.Font.Gotham
    inputBox.TextSize = 12
    inputBox.ClearTextOnFocus = false
    inputBox.Parent = frame
    
    local inputCorner = Instance.new("UICorner")
    inputCorner.CornerRadius = UDim.new(0, 10)
    inputCorner.Parent = inputBox
    
    -- Send button
    local sendBtn = Instance.new("TextButton")
    sendBtn.Size = UDim2.new(0, 65, 0, 44)
    sendBtn.Position = UDim2.new(1, -71, 1, -50)
    sendBtn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    sendBtn.BorderSizePixel = 1
    sendBtn.BorderColor3 = Color3.fromRGB(100, 100, 100)
    sendBtn.Text = "→"
    sendBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    sendBtn.Font = Enum.Font.GothamBold
    sendBtn.TextSize = 18
    sendBtn.Parent = frame
    
    local sendCorner = Instance.new("UICorner")
    sendCorner.CornerRadius = UDim.new(0, 10)
    sendCorner.Parent = sendBtn
    
    -- Loading overlay
    local loading = Instance.new("Frame")
    loading.Size = UDim2.new(0, 150, 0, 38)
    loading.Position = UDim2.new(0.5, -75, 0.5, -19)
    loading.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    loading.BackgroundTransparency = 0.9
    loading.BorderSizePixel = 1
    loading.BorderColor3 = Color3.fromRGB(80, 80, 80)
    loading.Visible = false
    loading.Parent = frame
    
    local loadingCorner = Instance.new("UICorner")
    loadingCorner.CornerRadius = UDim.new(0, 10)
    loadingCorner.Parent = loading
    
    local loadingText = Instance.new("TextLabel")
    loadingText.Size = UDim2.new(1, 0, 1, 0)
    loadingText.BackgroundTransparency = 1
    loadingText.Text = "⏳ VertexHUB Thinking..."
    loadingText.TextColor3 = Color3.fromRGB(255, 255, 255)
    loadingText.TextSize = 11
    loadingText.Font = Enum.Font.Gotham
    loadingText.Parent = loading
    
    -- Floating toggle button
    local toggleBtn = Instance.new("TextButton")
    toggleBtn.Size = UDim2.new(0, 48, 0, 48)
    toggleBtn.Position = UDim2.new(1, -58, 0, 12)
    toggleBtn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    toggleBtn.BorderSizePixel = 1
    toggleBtn.BorderColor3 = Color3.fromRGB(100, 100, 100)
    toggleBtn.Text = ""
    toggleBtn.Parent = mainGui
    
    -- Logo untuk toggle button
    local toggleLogo = Instance.new("ImageLabel")
    toggleLogo.Size = UDim2.new(0, 32, 0, 32)
    toggleLogo.Position = UDim2.new(0.5, -16, 0.5, -16)
    toggleLogo.BackgroundTransparency = 1
    toggleLogo.Image = "https://raw.githubusercontent.com/lionelbenayap1910-ctrl/vertexhub/31a7fe0907df11e6d34944582330db55f5d71054/file_00000000bb4c71fd8f7c25f3adda9f0a.png"
    toggleLogo.ScaleType = Enum.ScaleType.Fit
    toggleLogo.Parent = toggleBtn
    
    local toggleCorner = Instance.new("UICorner")
    toggleCorner.CornerRadius = UDim.new(1, 0)
    toggleCorner.Parent = toggleBtn
    
    -- Fungsi add message
    local function addMessage(text, isUser)
        local msgFrame = Instance.new("Frame")
        msgFrame.Size = UDim2.new(1, 0, 0, 0)
        msgFrame.BackgroundTransparency = 1
        msgFrame.AutomaticSize = Enum.AutomaticSize.Y
        msgFrame.Parent = chatFrame
        
        local maxWidth = chatFrame.AbsoluteSize.X - 20
        local bubble = Instance.new("Frame")
        bubble.Size = UDim2.new(0, math.min(maxWidth, 280), 0, 0)
        bubble.BackgroundColor3 = isUser and Color3.fromRGB(20, 20, 20) or Color3.fromRGB(30, 30, 30)
        bubble.BackgroundTransparency = 0
        bubble.BorderSizePixel = 1
        bubble.BorderColor3 = Color3.fromRGB(55, 55, 55)
        bubble.AutomaticSize = Enum.AutomaticSize.Y
        bubble.Position = isUser and UDim2.new(1, -5, 0, 0) or UDim2.new(0, 5, 0, 0)
        bubble.Parent = msgFrame
        
        local bubbleCorner = Instance.new("UICorner")
        bubbleCorner.CornerRadius = UDim.new(0, 12)
        bubbleCorner.Parent = bubble
        
        local msgLabel = Instance.new("TextLabel")
        msgLabel.Size = UDim2.new(1, -14, 0, 0)
        msgLabel.Position = UDim2.new(0, 7, 0, 8)
        msgLabel.BackgroundTransparency = 1
        msgLabel.Text = text
        msgLabel.TextColor3 = Color3.fromRGB(220, 220, 220)
        msgLabel.TextWrapped = true
        msgLabel.AutomaticSize = Enum.AutomaticSize.Y
        msgLabel.Font = Enum.Font.Gotham
        msgLabel.TextSize = 12
        msgLabel.TextXAlignment = isUser and Enum.TextXAlignment.Right or Enum.TextXAlignment.Left
        msgLabel.Parent = bubble
        
        local nameLabel = Instance.new("TextLabel")
        nameLabel.Size = UDim2.new(1, 0, 0, 14)
        nameLabel.Position = UDim2.new(0, 7, 0, -14)
        nameLabel.BackgroundTransparency = 1
        nameLabel.Text = isUser and "👤 You" : "⚡ VertexHUB AI"
        nameLabel.TextColor3 = Color3.fromRGB(110, 110, 110)
        nameLabel.TextSize = 9
        nameLabel.Font = Enum.Font.Gotham
        nameLabel.TextXAlignment = isUser and Enum.TextXAlignment.Right or Enum.TextXAlignment.Left
        nameLabel.Parent = bubble
        
        task.wait()
        chatFrame.CanvasPosition = Vector2.new(0, chatFrame.CanvasSize.Y.Offset)
    end
    
    -- Fungsi AI
    local isBusy = false
    
    local function askAI(question)
        local headers = {
            ["Authorization"] = "Bearer " .. currentAPIKey,
            ["Content-Type"] = "application/json"
        }
        
        local body = {
            messages = {
                {role = "system", content = "Kamu adalah VertexHUB AI, asisten untuk game 'Guess My Country'. Bantu pemain menebak negara dengan memberikan petunjuk menarik. Jawab singkat dan jelas dalam bahasa Indonesia."},
                {role = "user", content = question}
            },
            model = "llama-3.1-8b-instant",
            temperature = 0.7,
            max_tokens = 300
        }
        
        local success, response = pcall(function()
            return HttpService:RequestAsync({
                Url = API_URL,
                Method = "POST",
                Headers = headers,
                Body = HttpService:JSONEncode(body),
                Timeout = 15
            })
        end)
        
        if success and response.Success and response.StatusCode == 200 then
            local data = HttpService:JSONDecode(response.Body)
            if data.choices and data.choices[1] then
                return data.choices[1].message.content
            end
            return "Maaf, tidak ada response."
        else
            if response and response.StatusCode == 401 then
                return "❌ API Key invalid! Silakan login ulang."
            end
            return "❌ Error koneksi. Cek internet!"
        end
    end
    
    local function sendMessage()
        if isBusy then return end
        
        local msg = inputBox.Text
        if msg == "" then return end
        
        addMessage(msg, true)
        inputBox.Text = ""
        
        isBusy = true
        sendBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
        sendBtn.Text = "⌛"
        loading.Visible = true
        
        local reply = askAI(msg)
        
        loading.Visible = false
        sendBtn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
        sendBtn.Text = "→"
        
        addMessage(reply, false)
        isBusy = false
    end
    
    sendBtn.MouseButton1Click:Connect(sendMessage)
    inputBox.FocusLost:Connect(function(enter)
        if enter then sendMessage() end
    end)
    
    closeBtn.MouseButton1Click:Connect(function()
        mainGui:Destroy()
    end)
    
    local isMinimized = false
    toggleBtn.MouseButton1Click:Connect(function()
        isMinimized = not isMinimized
        frame.Visible = not isMinimized
        toggleBtn.BackgroundColor3 = isMinimized and Color3.fromRGB(40, 40, 40) or Color3.fromRGB(0, 0, 0)
    end)
    
    -- Welcome message
    addMessage("Welcome to VertexHUB! Saya AI assistant untuk Guess My Country. Ada yang bisa saya bantu? 🌍", false)
    
    print("✅ VertexHUB AI Chat loaded - Guess My Country Edition")
end

-- ========== START ==========
print("VertexHUB AI Chat Starting...")
createLoginWindow()
