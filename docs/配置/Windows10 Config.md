## Regedit

### Close Cortana：

`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows Search`

New `DWORD` named `AllowCortana`, and it't value is `0`.

### Set Key Map

`Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout`

Swap `Esc` with `Caps`:

New `Binaray Value` named `Scancode Map`, and value like this ![Input](./fig/1.png)

### Install App

```powershell
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
scoop install aria2
scoop intall 7zip
scoop install python3
scoop install git
scoop install github
scoop install vscode
```