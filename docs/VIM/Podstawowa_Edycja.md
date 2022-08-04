# Podstawowa edycja
Najczęściej podczas edycji wykonujemy kilka podstawowych operacji, takich jak wpisywanie tekstu, usuwanie tekstu oraz przenoszenie tekstu poprzez wycinanie i wklejanie. Oczywiście vi pozwala na wykonanie wszystkich wymienionych operacji na swój własny sposób. W programie vi możemy także w ograniczonym stopniu cofać polecenia. Gdy naciśniemy u w trybie poleceń, vi cofnie ostatnią dokonaną zmianę. Może się to przydać podczas wypróbowywania podstawowych poleceń edycji.
## Dodawanie tekstu
W trybie edycji programu vi możemy dodawać tekst na kilka sposobów. Korzystaliśmy już z polecenia i do wstawiania tekstu.
Powróćmy na chwilę do pliku foo.txt:

>Szybki brązowy lis przeskoczył nad leniwym psem.
  
Gdybyśmy chcieli dodać nieco tekstu na końcu tego zdania, okazałoby się, że polecenie i nam na to nie pozwoli, ponieważ nie możemy przenieść kursora
poza koniec wiersza. W vi dostępne jest polecenie służące do dodawania tekstu. Jest to polecenie a. Jeśli umieścimy kursor na końcu wiersza i naciśniemy klawisz A, kursor przejdzie poza koniec wiersza, a vi wejdzie w tryb edycji. Będziemy już mogli dodać nieco tekstu:

>Szybki brązowy lis przeskoczył nad leniwym psem. **To było fajne.**

Pamiętajmy o naciśnięciu klawisza Esc, aby wyjść z trybu edycji. Ponieważ niemal zawsze chcemy dodawać tekst na końcu wiersza, vi udostępnia skrót służący do przeniesienia kursora na koniec bieżącego wiersza i rozpoczęcie dodawania tekstu. Jest to polecenie A. Wypróbujmy je i dodajmy do naszego pliku kilka nowych wierszy.  
Najpierw przenieśmy kursor na początek wiersza, korzystając z polecenia 0 (zero). Następnie naciśnijmy klawisz A i dodajmy następujące wiersze:

>Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
**Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5**  


Naciśnijmy klawisz Esc, aby wyjść z trybu edycji. Jak widać, polecenie A jest wygodniejsze, ponieważ przenosi kursor na koniec wiersza przed włączeniem trybu edycji.

## Otwieranie wiersza
Innym sposobem wstawiania wiersza jest „otwieranie” wiersza. Możemy wstawić pusty wiersz pomiędzy dwa istniejące wiersze i włączyć tryb edycji. Polecenie to ma dwie postacie, przedstawione w tabeli 12.2.
Tabela 12.2. Klawisze służące do otwierania wiersza

Polecenie | Otwiera
--------- | ---------
o         | wiersz poniżej bieżącego wiersza
O         | wiersz powyżej bieżącego wiersza

Możemy to zademonstrować w następujący sposób — umieśćmy kursor w wierszu 3. i naciśnijmy klawisz o.

>Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5  

Poniżej trzeciego wiersza został wstawiony nowy wiersz i włączył się tryb edycji. Wyjdźmy z trybu edycji, naciskając klawisz Esc. Naciśnijmy klawisz U, aby cofnąć zmianę.
Naciśnijmy klawisz O, aby otworzyć wiersz powyżej kursora:

>Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
>Wiersz 2  
>  
>Wiersz 3  
>Wiersz 4  
>Wiersz 5  


Wyjdźmy z trybu edycji, naciskając klawisz Esc, i naciśnijmy klawisz u, aby cofnąć zmianę.

## Usuwanie tekstu
Jak można się spodziewać, vi udostępnia wiele poleceń służących do usuwania tekstu, z których wszystkie składają się z jednego lub kilku znaków. Na przykład polecenie x usuwa znak w miejscu położenia kursora. x może być poprzedzony liczbą, określającą, ile znaków należy usunąć. Polecenie d ma bardziej ogólne znaczenie. Podobnie jak x, można je poprzedzić liczbą, określającą, ile razy należy wykonać polecenie usuwania. Ponadto po znaku d zawsze występuje polecenie zmiany położenia, sterujące rozmiarem usuwanego fragmentu. Kilka przykładów znajdziemy w tabeli 12.3.
Tabela 12.3. Polecenia służące do usuwania tekstu

Polecenie | Usuwa
--------- | --------
cc        | całą bieżącą linię tekstu
:%d       | całą zawartość pliku
x         | bieżący znak
X         | usuwa znak przed kursorem
3x        | bieżący znak i dwa kolejne znaki
dd | bieżący wiersz
5dd | bieżący wiersz i cztery kolejne wiersze
dW | fragment od bieżącego położenia kursora do początku kolejnego słowa
d$ | fragment od bieżącego położenia kursora do końca bieżącego wiersza
d0 | fragment od bieżącego położenia kursora do początku wiersza
d^ | fragment od bieżącego położenia kursora do pierwszego znaku niebędącego białym znakiem w bieżącym wierszu
dG | fragment od bieżącego wiersza do końca pliku
d20G | fragment od bieżącego wiersza do 20. wiersza pliku

## Usuwanie zawartości pliku
Komenda ggVG  

* gg - przeskakuje do poczatku pliku
* V - zaznacza bieżącą linię (w tym przypadku pierwszą linię bieżącego pliku)
* G - przeskakuje do konca pliku. Jako że zanzaczyliśmy pierwszą linię polecenie G zaznaczy nam wszystkie linie pliku.
* Wciśnięcie d lub x wykasuje wszystkie linie

### Alternatywna metoda usuwania zawartości pliku
Komenda :1,$d  

Jest to o tyle elastyczniejsza metoda iż potrafi nam skasować zawartość pliku pomiędzy wierszami. Używając polecenia :4,$-2d zostawimy 3 pierwsze linie i dwie ostatnie usuwając pozostałą zawartość pliku.


Umieśćmy kursor w wyrazie To w pierwszym wierszu naszego tekstu. Naciśnijmy kilkakrotnie klawisz x, aż usuniemy resztę zdania. Następnie kilkakrotnie naciśnijmy klawisz u, aby cofnąć usuwanie.
>**UWAGA**
W prawdziwym programie vi możemy cofnąć tylko jedno polecenie. Natomiast
w programie vim możemy cofnąć kilka poleceń.

Ponownie usuńmy tekst, tym razem korzystając z polecenia d. Przenieśmy
kursor do słowa To i wpiszmy **dW**, aby usunąć słowo:

>Szybki brązowy lis przeskoczył nad leniwym psem. było fajne.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5  

Wpiszmy **d$**, aby usunąć fragment od miejsca położenia kursora do końca
wiersza:

>Szybki brązowy lis przeskoczył nad leniwym psem.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5  

Wpiszmy dG, aby usunąć fragment od bieżącego wiersza do końca pliku:

>~  
~  
~  
~  

Wpiszmy trzykrotnie **u**, aby cofnąć zmiany.

## Wycinanie, kopiowanie i wklejanie tekstu
Polecenie d nie tylko usuwa tekst, ale także go „wycina”. Za każdym razem, gdy użyjemy polecenia d, usunięty fragment jest kopiowany do bufora wklejania (czyli do schowka), z którego możemy go później pobrać, korzystając z polecenia p, które wklei zawartość bufora za miejscem położenia kursora, lub przed kursorem. Polecenie y służy do kopiowania tekstu. Działa ono w podobny sposób jak polecenie d. W tabeli 12.4 znajdziemy kilka przykładów kombinacji polecenia y z różnymi poleceniami zmiany położenia kursora.
Tabela 12.4. Polecenia kopiowania

Polecenie | Kopiuje
--------- | ---------
yy        | bieżący wiersz
5yy       | bieżący i cztery kolejne wiersze
yW | fragment od bieżącego położenia kursora do początku kolejnego słowa
y$ | fragment od bieżącego położenia kursora do końca bieżącego wiersza
y0 | fragment od bieżącego położenia kursora do końca bieżącego wiersza
y^ | fragment od bieżącego położenia kursora do pierwszego znaku niebędącego białym znakiem w bieżącym wierszu
yG | fragment od bieżącego wiersza do końca pliku
y20G | fragment od bieżącego wiersza do 20. wiersza pliku

Poćwiczmy kopiowanie i wklejanie. Umieśćmy kursor w pierwszym wierszu pliku i wpiszmy **yy**, aby skopiować bieżący wiersz. Następnie przesuńmy kursor
do ostatniego wiersza (G) i wpiszmy **p**, aby wkleić skopiowany wiersz poniżej bieżącego wiersza:

>Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5  
**Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.**  


Podobnie jak poprzednio, polecenie u cofnie zmianę. Upewnijmy się, że kursor nadal znajduje się w ostatnim wierszu pliku, i wpiszmy P, aby wkleić tekst powyżej bieżącego wiersza:

>Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
**Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.**  
Wiersz 5  

Wypróbujmy kilka innych poleceń y, wymienionych w tabeli 12.4, i sprawdźmy zachowanie poleceń p i P. Gdy skończymy, przywróćmy plik do stanu początkowego.

## Łączenie wierszy
vi jest dość restrykcyjny, jeśli chodzi o to, jak interpretuje wiersze. Zwykle nie możemy połączyć wiersza z wierszem znajdującym się poniżej poprzez przeniesienie kursora na koniec wiersza i usunięcie znaku końca wiersza. Dlatego w vi dostępne jest specjalne polecenie J (nie mylmy go z poleceniem j, które przesuwa
kursor), służące do łączenia wierszy.
Jeśli umieścimy kursor w wierszu 3. i wpiszemy polecenie J, zobaczymy następujący efekt:

>Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
Wiersz 2  
**Wiersz 3 Wiersz 4**  
Wiersz 5  
