$token = "YOUR_NGROK_TOKEN"

Start-BitsTransfer -Source "https://fritzbox3272.controlliamo.com/cdn/Private/Windows-RDP/rdp_regs.reg" -Destination "registry.reg" -Description "Downloading additional files..."
reg import registry.reg | Out-Null
Remove-Item .\registry.reg -Force | Out-Null
Start-BitsTransfer -Source "https://fritzbox3272.controlliamo.com/cdn/Private/Windows-RDP/README.txt" -Destination "C:\Users\Public\Desktop\README.txt" -Description "Downloading additional files..."
Start-BitsTransfer -Source "https://qemu.weilnetz.de/w64/2023/qemu-w64-setup-20230414.exe" -Destination "qemu_setup.exe" -Description "Downloading additional files..."
.\qemu_setup.exe /S | Out-Null
Remove-Item .\qemu_setup.exe -Force | Out-Null

net.exe start Audiosrv | Out-Null
net.exe user $env:UserName "Password@001" | Out-Null
write-host Username: $env:UserName
write-host Password: Password@001

Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server'-name "fDenyTSConnections" -Value 0 | Out-Null
Enable-NetFirewallRule -DisplayGroup "Remote Desktop" | Out-Null

.\ngrok.exe config add-authtoken $token | Out-Null
.\ngrok.exe tcp 3389 | Out-Null
