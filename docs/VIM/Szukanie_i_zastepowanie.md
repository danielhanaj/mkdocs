## Szukanie i zastępowanie
vi pozwala na przeniesienie kursora do miejsca będącego wynikiem wyszukiwania. Dotyczy to jednego wiersza lub całego pliku. Program może też zastępować tekst,
żądając (lub nie) potwierdzenia od użytkownika.

## Przeszukiwanie wiersza
Polecenie f przeszukuje wiersz i przenosi kursor do kolejnego wystąpienia podanego znaku. Na przykład polecenie fa przesunie kursor do kolejnego wystąpienia znaku a w bieżącym wierszu. Po wyszukaniu znaku w wierszu możemy powtórzyć tę operację, wpisując średnik.

Przeszukiwanie całego pliku
Aby przenieść kursor do kolejnego wystąpienia słowa lub frazy, korzystamy z polecenia /. Działa ono podobnie jak polecenie less opisane wcześniej. Gdy wpiszemy polecenie /, w dolnej części ekranu pojawi się ukośnik. Następnie wpisujemy wyraz lub frazę, którą chcemy wyszukać, i naciskamy Enter. Kursor zostanie przesunięty do miejsca zawierającego wyszukiwany tekst. Korzystając z polecenia n, możemy kilkakrotnie powtórzyć wyszukiwanie na podstawie wcześniejszego tekstu. Oto przykład:

```bash
Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5  
```
Umieśćmy kursor w pierwszym wierszu pliku, wpiszmy poniższe polecenie i naciśnijmy Enter:
```bash
/Wiersz
```
Kursor zostanie przeniesiony do drugiego wiersza. Następnie wpiszmy n, aby przenieść kursor do trzeciego wiersza. Powtórzmy kilkakrotnie polecenie n, aby przesunąć kursor w dół pliku, aż wyczerpią się pasujące fragmenty. Chociaż dotychczas wyszukiwaliśmy na podstawie słów i fraz, vi pozwala na wykorzystanie wyrażeń regularnych, potężnej techniki służącej do definiowania skomplikowanych wzorców tekstowych.

## Wyszukiwanie i zastępowanie globalne
vi wykorzystuje polecenie ex do wykonania operacji „wyszukaj i zamień” (zwanej w programie vi substytucją) w kilku wierszach lub w całym pliku. Aby zamienić **Wiersz** na **wiersz** w całym pliku, należy wpisać następujące polecenie:
```bash
:%s/Wiersz/wiersz/g
```
Rozbijmy powyższe polecenie na poszczególne elementy i sprawdźmy ich znaczenie (tabela 12.5).
Po wykonaniu polecenia „wyszukaj i zamień” treść naszego pliku jest następująca:
```bash
Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
wiersz 2  
wiersz 3  
wiersz 4  
wiersz 5  
```
Tabela 12.5. Przykład składni globalnego wyszukiwania i zastępowania:

Element | Znaczenie
------- | -------
: | Znak dwukropka rozpoczyna polecenie ex.
% | Określa zakres wierszy dla polecenia. % jest skrótem oznaczającym fragment od pierwszego do ostatniego wiersza. Możemy też zdefiniować własny zakres 1,5 (ponieważ nasz plik zawiera 5 wierszy) lub 1,$, co oznacza „od wiersza pierwszego do ostatniego wiersza w pliku”. Jeśli pominiemy zakres wierszy, operacja zostanie wykonana tylko w bieżącym wierszu.
s | Określa operację — w tym przypadku substytucję (wyszukanie i zamiana).
/Wiersz/wiersz/ | Wzorzec wyszukania i zamiany tekstu.
g | Definiuje globalne działanie polecenia. W tym przypadku substytucja będzie wykonana na każdej instancji znalezionego łańcucha w każdym wierszu. Jeśli pominiemy g, zamienione zostanie tylko pierwsze wystąpienie wyszukiwanego tekstu w każdym wierszu.

Możemy też zdefiniować polecenie substytucji wymagające potwierdzenia użytkownika. W tym celu należy na końcu polecenia dodać znak c. Na przykład:
```bash
:%s/wiersz/Wiersz/gc
```
Polecenie to przywróci pierwotną treść pliku. Jednak przed dokonaniem każdej zamiany vi się zatrzyma i poprosi nas o potwierdzenie w następujący sposób:
```bash
replace with Wiersz (y/n/a/q/l/^E/^Y)?
```
W odpowiedzi możemy wpisać jeden ze znaków w nawiasie. Ich znaczenie jest opisane w tabeli 12.6.

Tabela 12.6. Znaki potwierdzenia zamiany

Klawisz | Działanie
------- | -------
y | Dokona zamiany.
n | Pominie tę instancję wzorca.
a | Dokona zamiany tej i wszystkich kolejnych instancji wzorca.
q | lub Esc Zatrzymuje proces zamiany.
l | Wykona bieżącą zamianę i zakończy proces (skrót od ang. słowa last — „ostatni”).
Ctrl+E, Ctrl+Y | Przewija odpowiednio w dół lub w górę. Przydatne podczas przeglądania proponowanych zamian.

Jeśli wpiszemy **y**, operacja zostanie wykonana. Natomiast po wybraniu **n** program vi zignoruje tę zmianę i przejdzie do następnej.