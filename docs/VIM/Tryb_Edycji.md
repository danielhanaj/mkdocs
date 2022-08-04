# Tryby edycji
Uruchomimy teraz vi ponownie, lecz tym razem przekazując w poleceniu nazwę
nieistniejącego pliku. Tak tworzymy nowy plik za pomocą vi:  
```bash
[me@linuxbox ~]$ rm -f foo.txt
[me@linuxbox ~]$ vi foo.txt
```
Jeśli wszystko pójdzie dobrze, powinniśmy uzyskać na ekranie następujący
widok:
```bash
~
~
"foo.txt" [New File]
```
Znaki tyldy (~) na początku wierszy oznaczają, że wiersze te nie zawierają
żadnego tekstu. Nasz plik jest więc pusty. Niczego jeszcze nie wpisujmy!
Kolejną ważną funkcją vi, którą musimy poznać (oprócz sposobu wychodzenia
z programu) jest to, że vi może pracować w różnych trybach. Po uruchomieniu
program znajduje się w trybie poleceń. W tym trybie niemal każdy klawisz odpowiada poleceniu, dlatego jeśli zaczniemy coś pisać, vi właściwie oszaleje, pozostawiając nas z wielkim bałaganem.

## Włączanie trybu edycji
Aby dodać do pliku trochę tekstu, musimy najpierw włączyć tryb edycji. W tym
celu należy nacisnąć klawisz i. Gdy to zrobimy, powinniśmy następujący napis
w dolnej części ekranu, o ile vim działa w zwykłym wzbogaconym trybie (nie będzie
on widoczny w trybie zgodnym z vi):
```bash
-- INSERT --
```
Możemy już wpisać jakiś tekst. Na przykład:
```
Szybki brązowy lis przeskoczył nad leniwym psem.
```
Aby wyjść z trybu wstawiania i powrócić do trybu poleceń, należy nacisnąć
klawisz Esc.

## Zapisywanie pracy
Aby zapisać zmiany wprowadzone w pliku, musimy włączyć polecenia ex, pozostając w trybie poleceń. Jest to bardzo łatwe, wystarczy nacisnąć klawisz :. Gdy to
zrobimy, w dolnej części ekranu powinien się pojawić znak dwukropka:
```bash
:
```
Aby zapisać nasz zmodyfikowany plik, po dwukropku wpisujemy w, a następnie naciskamy Enter:
```bash
:w
```
Plik zostanie zapisany na twardym dysku. W dolnej części ekranu powinniśmy
uzyskać potwierdzenie, jak poniżej:
```bash
"foo.txt" [New] 1L, 46C written
```