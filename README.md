
local WindUI = loadstring(game:HttpGet(

"https://raw.githubusercontent.com/Footagesus/WindUI/main/dist/main.lua"

))()

local Players = game:GetService("Players")

local RunService = game:GetService("RunService")

local UIS = game:GetService("UserInputService")

local player = Players.LocalPlayer

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- ตั้งค่าชื่อ Folder ที่เก็บเหรียญใน Workspace (ต้องแก้ให้ตรงกับชื่อในเกมของคุณ)
local coinFolder = workspace:FindFirstChild("Coins") 

local isFarming = true -- เปิด-ปิดระบบฟาร์ม

-- ฟังก์ชันแจ้งเตือน
local function notify(message)
    print("System: " .. message)
    -- หากต้องการให้ขึ้นจอ สามารถใช้ StarterGui:SetCore("SendNotification", ...) ได้
end

-- ลูปการทำงานหลัก
task.spawn(function()
    while isFarming do
        local coins = coinFolder:GetChildren() -- ดึงรายการเหรียญทั้งหมดออกมา

        if #coins > 0 then
            -- ถ้ามีเหรียญ ให้เริ่มเก็บ
            for _, coin in pairs(coins) do
                if coin:IsA("BasePart") then
                    -- วาร์ปไปที่เหรียญ (หรือจะใช้ TweenService เพื่อความเนียน)
                    humanoidRootPart.CFrame = coin.CFrame
                    
                    -- รอสักพักให้ระบบเกมประมวลผลการเก็บ
                    task.wait(0.1) 
                end
            end
        else
            -- ถ้าเหรียญในโฟลเดอร์ไม่มีเหลือแล้ว
            notify("เหรียญหมดแล้ว!")
            
            -- รอสัก 5 วินาทีก่อนตรวจสอบใหม่ (ป้องกันเครื่องค้าง)
            task.wait(5) 
        end
        
        task.wait(0.5) -- หน่วงเวลาเล็กน้อยก่อนเริ่ม Loop รอบใหม่
    end
end)


local WindUI = loadstring(game:HttpGet(

"https://raw.githubusercontent.com/Footagesus/WindUI/main/dist/main.lua"

))()

