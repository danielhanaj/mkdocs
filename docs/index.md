# Przydatne sktóty klawaiturowe w Linuxie:

Komenda Emacs | Komenda Vim|  Wynik
--------|------|------
Tab | none | uzupełnia nazwę pliku lub folderu
Crtl+c | none |  Zabija proces terminala
Ctrl+z | none | Zawiesza proces terminala
Ctrl+d | x | Usuwa znak ustawiony za pozycją kursora
Ctrl+l | %d | Czyści screen tak jak komenda clear
Ctrl+a | 0 | Przesuwa kursor na początek linii
Ctrl+e | $ | Przesuwa kursor na koniec linii
Alt+b | b | Przesuwa kursor na początek poprzedniego słowa lub znaku interpunkcyjnego
Alt+f | w | Przesuwa kursor na koniec kolejnego słowa lub znaku interpunkcyjnego
Ctrl+b | h | Przesuwa kursor o jeden znak wstecz
Ctrl+f | l | Przesuwa kursor o jeden znak do przodu
Ctrl+u | d0 |  Usuwa i kopiuje do schowka część linii przed kursorem
Ctrl+k | d$ | Usuwa i kopiuje do schowka częśc linii za kursorem
Ctrl+w | | Usuwa słowo przed kursorem
Ctrl+y | p | Wstawia ostatni wycięty tekst ze schowka
Ctrl+p | k | Przchodzi do poprzedniej komendy z historii
Ctrl+n | | Przechodzi do następnej komendy z historii
Ctrl+r | j | przeszukuje komendę w historii 
Ctrl+shift+c | yy | kopiuje tekst
Ctrl+shift+v | p | wstawia tekst

# Włączanie VIM mode w konsoli
Można aktywować vim mode tak by skróty vima działały w konsoli Linuxa. by to zrobić należy wydać polecenie:
```bash
# Ustawia skróty klawiaturowe vima w konsoli Linuca
set -o vi
```
Komendę tę należy dodać do .bashrc i wykonać polecenie 
```bash
$ source ~/.bashrc
```
Aby aktywowac tryb vim nalezy najpierw wcisnać ESc