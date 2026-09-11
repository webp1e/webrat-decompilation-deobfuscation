# webrat-decompilation-deobfuscation

Декомпилированная структура spyware salat stealer (WebRAT) v6.0.3

## Структура файлов

```
salat/
├── funcs.go
├── init.go
├── main.go
├── sets.go
├── task.go
├── tsc.go
└── screenshot/
    └── screenshot.go
```

## Статистика

| Категория | Функций |
|-----------|---------|
| C2 и сеть | ~30 |
| Кража браузеров (Chromium) | ~25 |
| Кража Firefox (Gecko) | ~6 |
| Кража мессенджеров | ~5 |
| Кража крипто/Steam | ~6 |
| Слежка | ~20 |
| Elevation (UAC bypass) | ~10 |
| HVNC / удалённый стол | ~10 |
| Память и процессы | ~10 |
| Архивация | ~5 |
| Самоуничтожение | ~3 |
| Утилиты | ~15 |
| Всего | ~250 |

## main.go

Точка входа и главный цикл:

```
main.main
main.tloop
main.tloop.func1
main.newTask
main.doTask
main.doTask.gowrap1..5
main.updTaskStatus
main.changeEndpoint
main.initConnection
main.initConnection.func1
main.initConnection.func2
main.c2Server
main.dec
main.rq
main.ensure
main.log
main.reportError
```

C2 и сеть:

```
main.p2pSocks
main.proxySocks
main.proxy
main.forward
main.copyConn
main.(*Conn).Serve
main.(*socks5Conn).Serve
main.(*socks5Conn).handshake
main.(*socks5Conn).processRequest
main.tonResolve
main.tryTonResolve
main.tryRQ
```

WebSocket-сессия (RAT):

```
main.(*wsSess).Start
main.(*wsSess).Stop
main.(*wsSess).recvWss
main.(*wsSess).execCommand
main.(*wsSess).shellCommand
main.(*wsSess).sendShellCommand
main.(*wsSess).startShell
main.(*wsSess).stopShell
main.(*wsSess).ffdesktop
main.(*wsSess).sepDesktop
main.(*wsSess).ffwcam
main.(*wsSess).ffwmic
main.(*wsSess).p2p
main.(*wsSess).errorHandler
```

## funcs.go

Кража хром браузеров (Chromium):

```
main.getChrome
main.getChromeLogins
main.getChromeCookies
main.getChromeAutofils
main.getChromeToken
main.DecryptChrome
main.decryptData
main.decryptDataBrave
main.decryptDataEdge
main.GetChromiumMasterKeys
main.GetAppBoundKey
main.StartAPPB
main.DPAPI
main.getLocalEncryptorDataKey
main.loginPBE.Decrypt
main.metaPBE.Decrypt
main.nssPBE.Decrypt
main.NewASN1PBE
main.ASN1PBE
```

Кража firefox (gecko):

```
main.getGecko
main.getGeckoLogins
main.getGeckoCookies
main.GetGeckoMasterKey
main.DecryptGecko
```

Кража яндекс и других:

```
main.getYandexLogins
```

Кража мессенджеров и игр:

```
main.getDiscord
main.getSteams
main.decodeSteam
main.parseVdf
main.decodeFromTonAddress
main.getEp
main.getBC
```

Кража системных данных:

```
main.Steal
main.findLsassProcess
main.findProcessByName
main.getClipboardText
main.getDevices
main.getDrives
main.getRandomFolders
main.getRandomProcesses
main.getSystemToken
main.impersonateSystem
main.DuplicateUserTokenFromSessionID
main.duplicateHandle
main.openHndl
main.readFileFromHandle
main.readProcFile
main.NtQuerySystemHandles
```

Слежка:

```
main.runKeylogger
main.startKeylogger
main.stopKeylogger
main.keyPressCallback
main.specialKeyName
main.windowChangeCallback
main.SetWinEventHook
main.getScreen
main.sendScreen
main.screenStream
main.getWebcams
main.getMics
main.getActiveWin
main.getForegroundWindow
main.EnumWindows
main.GetWindowText
main.IsIdle
```

Дешифровка:

```
main.decryptAesGcm256
main.aes128CBCDecrypt
main.des3Decrypt
main.decryptAPPB
main.DPAPI
main.dec
main.md5str
main.RandStringRunes
```

Elevation (UAC bypass):

```
main.Elevate
main.IElevator
main.IElevatorVtbl
main.IElevatorBrave
main.IElevatorVtblBrave
main.IElevatorEdge
main.IElevatorVtblEdge
main.enablePrivilege
main.isAdmin
main.impersonateSystem
main.getSystemToken
```

Работа с памятью и процессами:

```
main.suspendProcessThreads
main.unlockProcs
main.findProcessByName
main.GetProcessPath
main.newWindowsProcess
main.WindowsProcess
main.Process
main.PROCESSENTRY32
```

Архивация:

```
main.zipFiles
main.zipFilesCreate
main.zipAddFS
main.unzip
```

Самоуничтожение:

```
main.selfDelete
main.Suicide
main.checkDupe
```

Утилиты:

```
main.bytesToBSTR
main.fixBytes
main.isValidString
main.isInvalidUnicode
main.GetHWID
main.GetHWID2
main.getBestMethod
main.getlock
main.staticinstall
main.periodicFlush
main.errorHandler
main.preErrorHandler
```

## init.go

```
main.init
main.init.0
main.initConnection
main.initConnection.func1
main.initConnection.func2
main.map.init.0
main.map.init.1
main.map.init.2
main.map.init.3
```

## sets.go

```
(хранит C2, RSA-ключ, AES-ключ, endpoint)
```

## task.go

```
main.newTask
main.doTask
main.doTask.gowrap1..5
main.updTaskStatus
```

## tsc.go

```
(Telegram Stealer Client или Task Scheduler Client)
```

## screenshot/screenshot.go

```
salat/screenshot.Capture
salat/screenshot.CaptureRect
salat/screenshot.CreateImage
salat/screenshot.CreateImage.func1
salat/screenshot.enumDisplayMonitors
salat/screenshot.getDesktopWindow
```

## Ключеевые артефакты

C2 endpoint:

```
GETbldpcnwincpugpumemadm[0]/saat/numMK:1//v10KEYkey'"'nil01_"
```

RSA-публичный ключ (1024-bit):

```
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCTJPWl2JbiGm5m/JFe2+V04s4xiCtCB+aljdutGzQkiCjbds0Di6uoxn4flbwAP3Xc1t0xssQVDG8mvAmrXBDwgolOEhHPMY8hP5/PjtLmuKfIOKKG0SKzRR60VckinIck799q3Hut1lr5o/qg78FBx5BGPg7I3+OguNL1iw8QIDAQAB
```

Сертификат:

```
Subject: CN=VenomRAT
Issuer: CN=VenomRAT Server, OU=qwqdanchun, O=VenomRAT By qwqdanchun, L=SH, C=CN
Valid: 2022-08-14 → 2033-05-23
```

DoH-резолверы:

```
https://cloudflare-dns.com/dns-query?name=
https://1.1.1.1/dns-query?name=
https://dns.google/resolve?name=
```

SQL-запросы:

```
SELECT LogonId, StartTime, LogonType FROM Win32_LogonSession WHERE LogonType=2
SELECT a11, a102 from nssPrivate
SELECT origin_url, username_value, password_value FROM logins
SELECT name, encrypted_value, host_key, path, expires_utc FROM cookies
```

Цели кражи:

```
SOFTWARE\Valve\Steam
Roaming\Mozilla\Firefox\Profiles
Local\Elements Browser\User Data
Local\Sputnik\Sputnik\User Data
lsass.exe
Metamask, TonKeeper, SuiWallet, Maiar, DEFI
```

## нструменты анализа

```
GoReSym
Rizin
pyinstxtractor
upx
strings
```

## Метаданные образца

```
Образец: payload_1.exe
Размер: 3.5 MB (UPX), 12 MB (распакованный)
Тип: PE32
Go Build ID: soaSZ3gtdf5oZjHHPnzB/jbJqVBD1Wvb3uj4gNdCH/m0su5JzGJzWj-0qjn9aX/-nSasggksAZHPIgvCjcl
Go Version: 1.24.0
Arch: 386 (32-bit)
OS: Windows
```

## вытащенный python загрузчик

```
def run_exe_from_b64(b64_data, wait = (False,)):
    
    try:
        raw = base64.b64decode(b64_data)
        temp_dir = os.environ.get('TEMP', tempfile.gettempdir())
        filename = os.path.join(temp_dir, f'''tmp_{uuid.uuid4().hex[:8]}.exe''')
        f = open(filename, 'wb')
        f.write(raw)
        
        try:
            None(None, None)
        with None:
            if not None:
                
                try:
                    
                    try:
                        if wait:
                            subprocess.run([
                                filename], shell = True, creationflags = 134217728)
                        else:
                            subprocess.Popen([
                                filename], shell = True, creationflags = 134217728)
                        return filename
                    except Exception:
                        e = None
                        e = None
                        del e
                        return None
                        e = None
                        del e





if __name__ == '__main__':
    path1 = run_exe_from_b64(EXE1_B64, wait = True)
    path2 = run_exe_from_b64(EXE2_B64, wait = True)
    return None
54 _payload_temp.py

```

## предупреждение

Материал предоставлен исключительно в образовательных и исследовательских целях
Автор не несёт ответственности за использование в противоправных целях

## В основану использованы данные источники

https://github.com/kaandemir993/Salat-Stealer-Telegram-Proxy-Decoy-C2-Analysis
https://darkatlas.io/blog/salat-stealer-analysis-go-based-rat-c2-resilience-and-info-stealing-capabilities

Благодарю dark atlas и kaandemir993 за предоставленную информацию
