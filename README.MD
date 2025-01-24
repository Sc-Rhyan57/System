## **SISTEMA DE ÁUDIO**
```luau
local function GetGitAudioID(githubLink, soundName)
    local fileName = "customObject_Sound_" .. tostring(soundName) .. ".mp3"
    
    local success, audioData = pcall(function()
        return game:HttpGet(githubLink)
    end)
    
    if not success then
        warn("Falha ao baixar o áudio: " .. githubLink)
        return nil
    end
    
    writefile(fileName, audioData)
    return (getcustomasset or getsynasset)(fileName)
end

local function PlayGitSound(githubLink, soundName, volume)
    local soundId = GetGitAudioID(githubLink, soundName)
    
    if soundId then
        local sound = Instance.new("Sound")
        sound.SoundId = soundId
        sound.Volume = volume or 0.5
        sound.Parent = workspace
        sound:Play()
        
        sound.Ended:Connect(function()
            sound:Destroy()
            delfile("customObject_Sound_" .. tostring(soundName) .. ".mp3")
        end)
        
        return sound
    end
    
    return nil
end

PlayGitSound("link-do-audio", "NomeAudio", 0.5)
```


## **SISTEMA DE VÍDEO**
```luau
local function GetGitVideoID(githubLink, videoName)
    local fileName = "customObject_Video_" .. tostring(videoName) .. ".mp4"
    
    local success, videoData = pcall(function()
        return game:HttpGet(githubLink)
    end)
    
    if not success then
        warn("Falha ao baixar o vídeo: " .. githubLink)
        return nil
    end
    
    writefile(fileName, videoData)
    return (getcustomasset or getsynasset)(fileName)
end

local function PlayGitVideo(githubLink, videoName)
    local videoId = GetGitVideoID(githubLink, videoName)
    
    if videoId then
        local video = Instance.new("VideoFrame")
        video.Video = videoId
        video.Parent = workspace
        video:Play()
        
        video.Ended:Connect(function()
            video:Destroy()
            delfile("customObject_Video_" .. tostring(videoName) .. ".mp4")
        end)
        
        return video
    end
    
    return nil
end


PlayGitVideo("link-do-video", "NomeVideo")
````


### **SISTEMA DE IMAGEM**
```luau
local function GetGitImageID(githubLink, imageName)
    local fileName = "customObject_Image_" .. tostring(imageName) .. ".png"
    
    local success, imageData = pcall(function()
        return game:HttpGet(githubLink)
    end)
    
    if not success then
        warn("Falha ao baixar a imagem: " .. githubLink)
        return nil
    end
    
    writefile(fileName, imageData)
    return (getcustomasset or getsynasset)(fileName)
end

local function CreateGitImage(githubLink, imageName, parent)
    local imageId = GetGitImageID(githubLink, imageName)
    
    if imageId then
        local image = Instance.new("ImageLabel")
        image.Image = imageId
        image.Size = UDim2.new(0, 300, 0, 300)
        image.Parent = parent or workspace
        
        return image
    end
    
    return nil
end

CreateGitImage("link-da-imagem", "NomeImagem", workspace)
```
