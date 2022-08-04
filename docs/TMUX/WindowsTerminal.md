# Konfiguracja SSH pod Windows Terminal
Aby logować się kluczem publicznym bez podawania hasła w Windows Terminal należy wykonać następujące polecenia:

## Generowanie klucza
Przy generowaniu należy podac passphrase
```ps
>ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\dan/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in hanselpi4.
Your public key has been saved in hanselpi4.pub.
```
## Kopiowanie klucza publicznego na zdalny serwer:
```ps
type c:\users\dan\.ssh\id_rsa.pub | ssh pi@hanselpi4 'cat >> .ssh/authorized_keys'
```
## Konfiguracja Windows Terminala
Dodajemy nowy profil
```json
"backgroundImage": "D:\\Windows_Terminal\\Ubuntu\\ubuntu-logo32.png",
                "backgroundImageAlignment": "center",
                "backgroundImageOpacity": 0.10000000000000001,
                "backgroundImageStretchMode": "none",
                "colorScheme": "UbuntuLegit",
                "commandline": "ssh alex@hanselpi4",
                "experimental.retroTerminalEffect": false,
                "font": 
                {
                    "face": "JetBrains Mono",
                    "size": 10
                },
                "guid": "{3b6e258c-bd69-43af-9365-69b153b0ece6}",
                "icon": "D:\\Windows_Terminal\\Ubuntu\\ubuntu-logo32.png",
                "name": "SSH pi@hanselpi4 \ud83d\udcbb",
                "opacity": 100,
                "startingDirectory": "%USERPROFILE%",
                "suppressApplicationTitle": false,
                "tabTitle": "hanselpi4",
                "useAcrylic": true
```

## Usługa OpenSSH Authentication Agent
Sprawdzamy w serwisach na maszynie Windowsowej czy usługa *OpenSSH Authentication Agent* jest włączona. Jeżeli nie jest to ją włączamy


## Dodanie klucza prywatnego do agenta SSH:
Następnie musimy dodać klucz prywatny do OpenSSH Authentication Agenta
```ps
ssh-add $HOME/.ssh/your_file_name
```
Po wykonaniu powyższych powinniśmy móczalogować się do naszego systemu bez użycia hasła.