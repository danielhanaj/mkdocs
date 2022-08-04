# Polecenia multiplexera terminali tmux

## Skróty przydatne do pracy z panelami 

Polecenie                | Akcja
---------------------- | ---------------
tmux | Uruchamia okno terminala tmux
tmux new -t new-project | Uruchamia okno terminala tmux z nazwą projektu new-project
tmux list-sessions | Listuje sesje tmuxa
tmux attach -t nazwa_sesji | Podłącza nas do sesji. Zamiast nazwa_sesji można podać jej numer co będzie szybsze. Zamiast attach można użyć skrótu a
tmux ls | Listuje wszystkie aktywne sesje tmuxa
tmux rename-session -t a b| Zmienia nazę sesji z a na b z poziomu konsoli głównej
tmux new -s nazwasesji | Tworzy nową sesję z podaną nazwą
tmux kill-session -t sessionname | Zamyka sesję
Ctrl + b | Domyślny skrót dla prefixu
Crtl + d | Zamyka aktywną sesję
Prefix + ? | Pokazuje wszystkie skróty tmuxa 
Prefix + d | Odłącza od aktywnej sesji tmux bez jej zamykania
Prefix + % | Tworzy nowy panel w oknie obok
Prefix + " | Tworzy nowy panel w oknie poniżej
Prefix + o | Przełącza między sesjami
Prefix + Spacja | Przełącza layout z horyzontalnego na vertykalny i odwrotnie
Prefix + x z potwierdzeniem y | Zamyka panel
Prefix + kursor | Przełącza panel
Prefix + } | Zamienia panele kolejnością
Prefix + { | Zamienia panele kolejnością
Prefix + $ | Zmienia nazwę sesji z numeru do dowolnej nazwy
Prefix + s | Listuje sesje tmuxa z poziomu aktywnej sesji. Fajne bo nie trzeba wychodzic z tmuxa żeby przełączyć się na inną sesję
Prefix + z | Zoomuje aktywną sesję. Ponowne użycie tej kombinacji przywraca pozostałe sesje

## Skróty przydatne do pracy z oknami

Polecenie                | Akcja
---------------------- | ---------------
Prefix + c | Uruchamia nowe okno w bieżącym projekcie tmux
Prefix + p | Przełącza na poprzednie okno
Prefix + n | Przełącza na następne okno
Prefix + & z potwierdzeniem y | Zamyka bieżące okno
Prefix + , | Zmienia nazwę aktywnego okna
Prefix + w | Listuje wszystkie okna i pozwala się między nimi przemieszczać kursorami
Prefix + f | Pozwala wyszukać okno po nazwie

# Edycja pliku konfiguracyjnego
Możemy zmienić defaultowe ustawienia tmuxa edytując plik ~/.tmux.conf

## Zmiana defaultowego prefixu na Ctrl+a
```bash
# Rebind prefix key  
unbind C-b
set-option -g prefix C-a
bind-key C-a send-refix
```

## Zmiana kolorów
```bash
# Pretty colors
set -g status-bg blue
set -g status-fg white
```

## Przeładowanie pliku konfiguracyjnego

```bash
# Easy reloading
bind R source-file ~/.tmux.conf
```


# Sprawdzanie defaultowych przypisań

```bash
man tmux
/bind
```

# Kopiowanie w tmux
Aby skopiowac dany tekst należy włączyć tryb kopiowania używając Prefix + [  
Pozwala to przełączać się między liniami w pliku kursorami. By wyjść z trybu skrolowania wytarczy wcisnąć q bez prefixu.
Zaznaczamy początek tekstu który chcemy skopiować i wciskamy Ctrl + Space i kursorami przesuwamy tekst który będzie się zaznaczał. kiedy już mamy zanznaczony tekst wciskamy Ctrl + w
Spowoduje to wyjście z trybu kopiowania. 

Wklejamy wciskając Prefix + ]

# Włączanie trybu myszy
Możemy nawigować używając myszki. Buy to zrobić należy wybrać Prefix + : i wydać komendę
```bash
:set mouse on
```
By wyłączyć tryb myszy:
```bash
:set mouse off
```
# Udostępnianie sesji
Używając tmux i łącząc się z tą samą sesją z wielu maszyn zdalnych możemy współdzielić daną sesję z wieloma użytkownikami w tym samym czasie tworząc tzw. "zdalny pulpit". Użytkownicty pdpięci do tej samej sesji w tym samym czasie mogą pracować jednocześnie.  
Podobnie można łączyć się z sesją tmux a zniej łączyć przez ssh z maszyną która nie ma tmuxa tak by robić np troubleshooting na maszynie, np na ESXie czy na vCenter.

# Współdzielenie historii między sesjami
By default historia między sesjami tmux nie jest współdzielona. Oznacza to że komenda wpisana w jednej sesji nie jest widoczna w historii drugiej sesji. Można to zmienićw następujący sposób.
Edytujemy plik:
```bash
vim ~/.bashrc
```
A wnim dodajemy następujące wpisy:
```bash
shopt -s histappend
shopt -s histreedit
shopt -s histverify
HISTCONTROL='ignoreboth'
PROMPT_COMMAND="history -a;history -c;history -r; $PROMPT_COMMAND"
```
Zapisujemy zmiany i wydajemy komende 
```bash
source ~/.bashrc
```
Jeżeli używamy zsh to najpierw musimy uruchomić basha
```bash
exec bash
```
Wykonać powyższe  polecenia a potem 
```bash
exec zsh
```
