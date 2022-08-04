# Edycja wielu plików
Często chcemy edytować kilka plików jednocześnie. Może się pojawić konieczność dokonania zmian w kilku plikach lub skopiowania treści jednego pliku do drugiego. W programie vi możemy otworzyć do edycji kilka plików, podając w wierszu poleceń ich nazwy:
```bash
vi plik1 plik2 plik3...
```
Wyjdźmy z bieżącej sesji vi, aby utworzyć nowy plik do edycji. Najpierw wpiszmy **:wq**, aby zamknąć vi i zapisać zmiany w tekście. Następnie utwórzmy w katalogu domowym dodatkowy plik, który posłuży nam do ćwiczeń. Nowy plik utworzymy, przechwytując wynik z polecenia ls:

```bash
[me@linuxbox ~]$ ls -l /usr/bin > ls-output.txt
```
Dokonajmy zmian w starym i nowym pliku, korzystając z vi:

```bash
[me@linuxbox ~]$ vi foo.txt ls-output.txt
```
Uruchomimy w ten sposób vi; na ekranie pojawi się treść pierwszego pliku:

```bash
Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5  
```
## Przełączanie między plikami
Aby przełączyć się między jednym plikiem a drugim, korzystamy z następującego polecenia ex:
```bash
:bn
```
Aby powrócić do poprzedniego pliku, korzystamy z polecenia:
```bash
:bp
```
Chociaż możemy przełączać się między plikami, vi przestrzega zasady zapobiegającej przełączaniu, jeśli nie zapisaliśmy zmian w bieżącym pliku. Aby wymusić na vi przełączenie pliku i porzucenie zmian, należy dodać na końcu polecenia wykrzyknik (!).

Oprócz opisanej powyżej metody przełączania się między plikami vim (i niektóre wersje vi) udostępnia polecenia ex ułatwiające zarządzanie kilkoma plikami. Korzystając z polecenia :buffers, możemy wyświetlić listę edytowanych plików. Lista plików zostanie wyświetlona w dolnej części ekranu:

```bash
:buffers
1 %a "foo.txt" line 1
2 "ls-output.txt" line 0
Press ENTER or type command to continue
```
Aby przełączyć się do innego bufora (pliku), należy wpisać **:buffer** wraz z numerem bufora, który chcemy edytować. Aby na przykład przełączyć się z bufora 1., zawierającego plik foo.txt, do bufora 2., który zawiera plik ls-output.txt, należy wpisać polecenie:

```bash
:buffer 2
```
a na ekranie pojawi się zawartość drugiego pliku. Bufory można też zmieniać wspomnianymi wcześniej poleceniami :bn (skrót od słów buffer next) oraz :bp (skrót od buffer previous).

## Otwieranie do edycji dodatkowych plików
Możemy też dodać kolejne pliki do bieżącej sesji edycji. Polecenie ex :e (skrót od ang. słowa edit — „edycja”), po którym następuje nazwa pliku, otworzy dodatkowy plik. Zakończmy bieżącą sesję edycji i powróćmy do wiersza poleceń. Uruchomimy teraz vi ponownie, otwierając tylko jeden plik:

```bash
[me@linuxbox ~]$ vi foo.txt
```
Aby dodać drugi plik, wpiszmy:

```bash
:e ls-output.txt
```
Plik powinien się pojawić na ekranie. Możemy też sprawdzić, czy pierwszy plik jest nadal dostępny:

```bash
:buffers
1 # "foo.txt" line 1
2 %a "ls-output.txt" line 0
Press ENTER or type command to continue
```
## Kopiowanie treści z jednego pliku do drugiego
Podczas edycji wielu plików często chcemy skopiować fragment jednego edytowanego pliku do drugiego. Można tego z łatwością dokonać, korzystając z używanych wcześniej zwykłych poleceń „kopiuj” i „wklej”. Możemy to zademonstrować w opisany dalej sposób. Najpierw przełączmy się do bufora 1. (foo.txt), wpisując polecenie:

```bash
:buffer 1
```
Na ekranie powinna się pojawić następująca treść:

```bash
Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.  
Wiersz 2  
Wiersz 3  
Wiersz 4  
Wiersz 5  
```
Następnie przenieśmy kursor do pierwszego wiersza i wpiszmy **yy**, aby go skopiować.
Przełączmy się do drugiego bufora, wpisując:

```bash
:buffer 2
```
Ekran będzie teraz przedstawiał listę plików podobną do poniższej (tutaj widoczny jest tylko fragment):

```bash
total 343700
-rwxr-xr-x 1 root root 31316 2017-12-05 08:58 [
-rwxr-xr-x 1 root root 8240 2017-12-09 13:39 411toppm
-rwxr-xr-x 1 root root 111276 2018-01-31 13:36 a2p
-rwxr-xr-x 1 root root 25368 2016-10-06 20:16 a52dec
-rwxr-xr-x 1 root root 11532 2017-05-04 17:43 aafire
-rwxr-xr-x 1 root root 7292 2017-05-04 17:43 aainfo
```
Umieśćmy kursor w pierwszym wierszu i wpiszmy polecenie **p**, aby wkleić wiersz skopiowany w poprzednim pliku:
```bash
total 343700
Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.
-rwxr-xr-x 1 root root 31316 2017-12-05 08:58 [
-rwxr-xr-x 1 root root 8240 2017-12-09 13:39 411toppm
-rwxr-xr-x 1 root root 111276 2018-01-31 13:36 a2p
-rwxr-xr-x 1 root root 25368 2016-10-06 20:16 a52dec
-rwxr-xr-x 1 root root 11532 2017-05-04 17:43 aafire
-rwxr-xr-x 1 root root 7292 2017-05-04 17:43 aainfo
```
## Wstawianie treści całego pliku do drugiego pliku
Mamy również możliwość wstawienia treści całego pliku do pliku, który edytujemy. Aby przećwiczyć tę metodę, zakończmy naszą sesję vi i zacznijmy nową sesję z jednym plikiem:
```bash
[me@linuxbox ~]$ vi ls-output.txt
```
Na ekranie ponownie zobaczymy listę plików:
```bash
total 343700
-rwxr-xr-x 1 root root 31316 2017-12-05 08:58 [
-rwxr-xr-x 1 root root 8240 2017-12-09 13:39 411toppm
-rwxr-xr-x 1 root root 111276 2018-01-31 13:36 a2p
-rwxr-xr-x 1 root root 25368 2016-10-06 20:16 a52dec
-rwxr-xr-x 1 root root 11532 2017-05-04 17:43 aafire
-rwxr-xr-x 1 root root 7292 2017-05-04 17:43 aainfo
```
Umieśćmy kursor w trzecim wierszu i wpiszmy następujące polecenie ex:
```bash
:r foo.txt
```
Polecenie :r (skrót od ang. słowa read — „czytaj”) wstawia treść podanego pliku przed miejscem położenia kursora. Na ekranie powinna się pojawić następująca treść:
```bash
total 343700
-rwxr-xr-x 1 root root 31316 2017-12-05 08:58 [
-rwxr-xr-x 1 root root 8240 2017-12-09 13:39 411toppm
Szybki brązowy lis przeskoczył nad leniwym psem. To było fajne.
Wiersz 2
Wiersz 3
Wiersz 4
Wiersz 5
-rwxr-xr-x 1 root root 111276 2018-01-31 13:36 a2p
-rwxr-xr-x 1 root root 25368 2016-10-06 20:16 a52dec
-rwxr-xr-x 1 root root 11532 2017-05-04 17:43 aafire
-rwxr-xr-x 1 root root 7292 2017-05-04 17:43 aainfo
```

## Zapisywanie zmian
Podobnie jak w przypadku innych operacji w vi, istnieje kilka sposobów zapisywania edytowanych plików. Wspomnieliśmy już o poleceniu ex :w, jednak do dyspozycji mamy kilka innych przydatnych poleceń.
Jeśli wpiszemy w trybie poleceń ZZ, zapiszemy bieżący plik i zamkniemy vi. Podobnie działa polecenie ex :wq, które jest kombinacją polecenia :w i :q i służy do zapisania pliku i zamknięcia programu. Polecenie :w można też opcjonalnie uzupełnić nazwą pliku. Uzyskamy wtedy efekt polecenia Zapisz jako. Jeśli na przykład edytujemy plik foo.txt i chcemy zapisać jego drugą wersję pod nazwą foo1.txt, powinniśmy wpisać:
```bash
:w foo1.txt
```
> **UWAGA**
> Polecenie to zapisze plik pod nową nazwą, jednak nie zmieni nazwy bieżącego
edytowanego pliku. Jeśli będziemy kontynuować edycję, nadal będziemy modyfikować plik foo.txt, a nie foo1.txt.