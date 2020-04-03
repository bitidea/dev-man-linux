# Windows 10 LTSC 客户端

1. `控制面板` -> `启用或关闭 Windows 功能` -> `SMB 1.0/CIFS File Sharing Support`
2. `Win+R` -> `gpedit.msc`
3. `计算机配置` -> `管理模板` -> `网络` -> `Lanman 工作站` -> `启用不安全的来宾登录`
4. `PowerShell` -> `Get-SmbServerConfiguration | Select EnableSMB1Protocol`

可能需要重启
