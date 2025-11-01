【来自kimi2的答复：】 WSL2 在 NAT 网络模式下 的已知限制。意思是：
·你在 Windows 主机上配置了代理（比如 Clash、V2Ray、Proxifier 等），监听的是  127.0.0.1:端口 ；
·但 WSL2 内部是一个独立的虚拟网络环境，它的  localhost  并不是 Windows 的  localhost ；
·所以 WSL2 里访问  127.0.0.1:端口  是访问不到 Windows 的代理服务的；
·因此 WSL2 提示你：检测到了代理，但无法自动使用。

✅ 方法一：启用 Mirrored 网络模式（最简单）
从 Windows 11 22H2 + WSL 2.0.0+ 开始，支持  networkingMode=mirrored ，让 WSL2 和 Windows 共享 IP 和 localhost。
步骤：
1. 打开 PowerShell，执行：
```
notepad $env:USERPROFILE\.wslconfig
```

2. 添加以下内容：
```
[experimental]
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true
```

3. 保存后执行：
```
wsl --shutdown
```

4.【删除】设置声音：每当任务或子任务完成，都有塞尔达音效提示，非常带感
```
npm install -g zelda-claude-code@latest
```
注：新安装python314,发现找不到python3.exe，在系统环境变量里面将python的路径放到最前面，或者关闭windows应用执行别名：设置 → 应用 → 应用执行别名 → 关闭“Python”和“Python3”两个开关

4. 重新打开 WSL，提示应该消失，且代理可直接用  127.0.0.1:端口 。
⚠️ 注意：Mirrored 模式在某些公司 VPN 环境下可能不兼容，若无法联网可回滚。