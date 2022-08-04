# Odczyt, zapis i wykonywanie
Prawa dostępu do plików i katalogów są zdefiniowane pod względem uprawnień do odczytu, zapisu oraz do wykonywania. Jeśli zerkniemy na wynik działania polecenia ls, uzyskamy pewną wskazówkę o sposobie implementacji:

```bash
[me@linuxbox ~]$ > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw-rw-r-- 1 me me 0 2018-03-06 14:52 foo.txt
```
10 pierwszych znaków na liście to atrybuty pliku. Pierwszy znak oznacza typ pliku. W tabeli 9.1 wypisano często używane typy plików (istnieją też inne, mniej znane)

Tabela 9.1. Typy plików

Atrybut | Typ pliku
-------- | --------
- | Zwykły plik.
d | Katalog.
l | Dowiązanie symboliczne. Zauważmy, że w przypadku dowiązań symbolicznych pozostałe atrybuty pliku mają zawsze postać rwxrwxrwx i są to wartości zastępcze. Rzeczywiste atrybuty plików są przypisane do pliku, do którego odwołuje się dowiązanie symboliczne.
c | Specjalny plik znakowy. Ten typ pliku odnosi się do urządzenia przetwarzającego dane w postaci strumienia bitów, na przykład do terminala czy mechanizmu /dev/null.
b | Specjalny plik blokowy. Ten typ pliku dotyczy urządzenia przetwarzającego dane w postaci bloków, na przykład dysku twardego lub czytnika DVD.

Pozostałe dziewięć znaków atrybutów pliku nosi nazwę trybu pliku. Reprezentują one uprawnienia do odczytu, zapisu i wykonywania przez posiadacza pliku, grupy, do której plik jest przypisany, oraz przez wszystkich pozostałych użytkowników.

Właściciel | Grupa | Świat
---------- | ----- | ------
rwx | rwx | rwx

W tabeli 9.2 opisano efekty, jakie uzyskamy na poprzez ustawienie atrybutów r, w i x dla plików i katalogów.
Tabela 9.2. Atrybuty uprawnień

Atrybut | Pliki | Katalogi
------- | ----- | ---------
r | Zezwala na otwarcie i odczyt pliku. | Zezwala na wyświetlanie zawartości katalogu, o ile ustawione są też uprawnienia do wykonywania.
w | Zezwala na zapis do pliku lub usunięcie zawartości pliku; nie pozwala jednak na zmianę nazwy ani na usunięcie pliku. Możliwość usuwania i zmiany nazwy plików jest determinowana przez atrybuty katalogu. | Zezwala na tworzenie, usuwanie i zmianę nazwy plików w katalogu, o ile ustawione są też uprawnienia do wykonywania.
x | Zezwala na traktowanie pliku jako programu i na jego uruchamianie. Programy napisane w językach skryptowych mogą być uruchamiane tylko wtedy, gdy zostały także udostępnione do odczytu. | Zezwala na przechodzenie do katalogu, na przykład w następujący sposób: cd katalog

Tabela 9.3. Przykłady atrybutów uprawnień

Atrybuty plików | Znaczenie
--------------- | -------
-rwx------ | Zwykły plik udostępniony do odczytu, zapisu i wykonywania przez właściciela pliku. Nikt inny nie ma dostępu.
-rw------- | Zwykły plik udostępniony do odczytu i zapisu przez właściciela pliku. Nikt inny nie ma dostępu.
-rw-r--r-- | Zwykły plik udostępniony do odczytu i zapisu przez właściciela pliku. Członkowie grupy oraz pozostali użytkownicy mają prawo do odczytu pliku.
-rwxr-xr-x | Zwykły plik udostępniony do odczytu, zapisu i uruchomienia przez właściciela pliku. Wszyscy pozostali użytkownicy mogą odczytać i uruchomić plik.
-rw-rw---- | Zwykły plik udostępniony do odczytu i zapisu tylko przez właściciela pliku i członków grupy, do której przypisany jest plik.
Lrwxrwxrwx | Dowiązanie symboliczne. Wszystkie dowiązania symboliczne posiadają uprawnienia zastępcze. Rzeczywiste uprawnienia są przypisane do pliku wskazywanego przez dowiązanie symboliczne.
drwxrwx--- | Katalog. Właściciel i członkowie grupy mogą wejść do katalogu oraz tworzyć, zmieniać nazwy i usuwać pliki wewnątrz katalogu.
drwxr-x--- | Katalog. Właściciel może wejść do katalogu oraz tworzyć, zmieniać nazwy i usuwać pliki wewnątrz katalogu. Członkowie grupy mogą wejść do katalogu, ale nie mogą tworzyć, usuwać i zmieniać nazw plików.