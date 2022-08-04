# chmod — zmiana trybu pliku
Aby zmienić tryb (uprawnienia) pliku lub katalogu, korzystamy z polecenia chmod. Należy zapamiętać, że tryb pliku lub katalogu może zmienić tylko właściciel pliku lub użytkownik uprzywilejowany. Polecenie chmod umożliwia zdefiniowanie trybu na dwa sposoby.

* Poprzez reprezentację ósemkową.
* Poprzez reprezentację symboliczną.

Najpierw omówimy reprezentację ósemkową. W notacji ósemkowej do określenia wzorca pożądanych uprawnień wykorzystujemy liczby w systemie ósemkowym. Ponieważ w systemie ósemkowym każda cyfra reprezentuje trzy cyfry binarne, można ją łatwo zmapować na schemat wykorzystywany do przechowywania trybu pliku. W tabeli 9.4 pokazano, co to oznacza.

Tabela 9.4. Tryby plików w reprezentacji binarnej i ósemkowej

Reprezentacja ósemkowa | Reprezentacja binarna | Tryb pliku
---------------------- | --------------------- | -----------
0 | 000 | ---
1 | 001 | --x
2 | 010 | -w-
3 | 011 | -wx
4 | 100 | r--
5 | 101 | r-x
6 | 110 | rw-
7 | 111 | rwx

>**CZYM U LICHA JEST SYSTEM ÓSEMKOWY?**

>System ósemkowy (o podstawie 8) oraz jego kuzyn, czyli system szesnastkowy (o podstawie 16), są systemami liczbowymi często wykorzystywanymi do wyrażania liczb w informatyce. My, ludzie, liczymy w systemie opartym na liczbie 10, co wynika z faktu posiadania przez nas 10 palców (a przynajmniej przez większość z nas). Natomiast komputery zostały wyposażone tylko w jeden palec i dlatego mogą wykonywać obliczenia w systemie binarnym (o podstawie 2). Ich system liczbowy operuje tylko na dwóch cyfrach: zero i jeden. To dlatego liczenie w systemie binarnym wygląda następująco:  

>0, 1, 10, 11, 100, 101, 110, 111, 1000, 1001, 1010, 1011

>W systemie ósemkowym liczymy z wykorzystaniem cyfr od zera do siedmiu, czyli:  

>0, 1, 2, 3, 4, 5, 6, 7, 10, 11, 12, 13, 14, 15, 16, 17, 20, 21…

>W systemie szesnastkowym korzystamy z cyfr od zera do dziewięciu oraz dodatkowo z liter od A do F:

>0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, 10, 11, 12, 13…

>Chociaż z łatwością dostrzeżemy sens stosowania systemu dwójkowego (komputery są wyposażone tylko w jeden palec), to możemy mieć wątpliwości co do systemu ósemkowego i szesnastkowego. Odpowiedź wiąże się z ludzką wygodą. Małe porcje danych są często reprezentowane na komputerach jako wzorce bitowe. Weźmy na przykład kolor RGB. W większości monitorów każdy piksel jest reprezentowany przez trzy komponenty koloru: 8 bitów dla koloru czerwonego, 8 bitów dla zielonego i 8 bitów dla niebieskiego. Piękny niebieski kolor zostałby zapisany w postaci 24-bitowej liczby:

>010000110110111111001101

>Czy ktokolwiek chciałby przez cały dzień odczytywać i zapisywać takie liczby? Nie sądzę. Tutaj pojawia się potrzeba wykorzystania innego systemu numerycznego. Każda cyfra w liczbie szesnastkowej reprezentuje cztery cyfry binarne. Dzięki temu zapis naszego 24-bitowego koloru niebieskiego można skrócić do 6-cyfrowej liczby szesnastkowej: 436FCD.

>Ponieważ cyfry w liczbie szesnastkowej odpowiadają bitom w liczbie binarnej, możemy zauważyć, że czerwony komponent naszego koloru jest reprezentowany przez liczbę 43, zielony przez 6F, a niebieski przez CD.

>Obecnie zapis szesnastkowy (zwykle określany jako hex) jest częściej stosowany niż ósemkowy, jednak możliwość zapisu trzech bitów liczby dwójkowej w systemie ósemkowym jest bardzo przydatna, o czym przekonamy się niebawem.

Za pomocą trzech cyfr w systemie ósemkowym możemy ustawić tryb pliku dla właściciela, dla grupy, do której przypisany jest plik, i dla pozostałych użytkowników.
```bash
[me@linuxbox ~]$ > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw-rw-r-- 1 me me 0 2018-03-06 14:52 foo.txt
[me@linuxbox ~]$ chmod 600 foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw------- 1 me me 0 2018-03-06 14:52 foo.txt
```
Przekazując argument 600, mogliśmy ustawić uprawnienia właściciela do odczytu i zapisu oraz usunąć uprawnienia grupy i pozostałych użytkowników. Chociaż zapamiętanie mapowania między reprezentacją ósemkową a binarną może się wydawać pewną niedogodnością, jednak w praktyce często stosuje się tylko kilka przypadków: 7 (rwx), 6 (rw-), 5 (r-x), 4 (r--) i 0 (---).

**chmod** pozwala też na ustawienie trybu plików za pomocą zapisu symbolicznego. Zapis symboliczny składa się z trzech części.  

* Użytkownik, którego dotyczy zmiana.  
* Operacja, która zostanie wykonana.  
* Uprawnienia, które zostaną ustawione  

Aby określić, kogo dotyczy zmiana, korzystamy z kombinacji znaków u, g, o i a zgodnie z opisem w tabeli 9.5.

Tabela 9.5. Zapis symboliczny polecenia chmod

Symbol | Znaczenie
------ | ---------
u | Skrót od ang. słowa user („użytkownik”); oznacza właściciela pliku lub katalogu.
g | Grupa.
o | Skrót od ang. słowa other („pozostali”); oznacza wszystkich pozostałych użytkowników.
a | Skrót od ang. słowa all („wszyscy”); obejmuje wszystkich użytkowników określanych przez symbole u, g i o.

Jeśli nie zdefiniujemy żadnego znaku, domyślnie zostanie użyta opcja all. Operacja może mieć postać a+, co oznacza dodanie uprawnienia, a-, co oznacza odebranie uprawnienia, lub a=, co oznacza, że przypisane zostaną tylko niektóre uprawnienia, a wszystkie pozostałe zostaną odebrane.  

Uprawnienia są określane z wykorzystaniem znaków r, w oraz x. W tabeli 9.6 przedstawiono kilka przykładów zapisu symbolicznego.  

Niektórzy wolą korzystać z zapisu ósemkowego; inni cenią sobie zapis symboliczny. Zapis symboliczny ma tę przewagę, że pozwala na ustawienie jednego atrybutu bez wpływu na pozostałe.  

Na stronie podręcznika man polecenia chmod znajdziemy więcej szczegółów oraz listę opcji. Uważajmy na opcję --recursive. Opcja ta sprawia, że polecenie zostanie wykonane zarówno na plikach, jak i na katalogach. To dlatego nie jest tak przydatna, jak mogłoby się wydawać, ponieważ rzadko chcemy, aby pliki i katalogi posiadały te same ustawienia uprawnień.

Tabela 9.6. Przykłady zapisu symbolicznego polecenia chmod

Zapis | Znaczenie
----- | -------
u+x | Nadaje właścicielowi pliku uprawnienia do wykonywania.
u-x | Odbiera właścicielowi pliku uprawnienia do wykonywania.
+x | Nadaje uprawnienia do wykonywania właścicielowi pliku, grupie i pozostałym użytkownikom. Odpowiednik zapisu a+x.
o-rw | Odbiera uprawnienia do odczytu i zapisu wszystkim poza właścicielem i grupą.
go=rw | Nadaje uprawnienia do odczytu i zapisu grupie i wszystkim innym poza właścicielem pliku. Jeśli grupa i pozostali użytkownicy posiadali wcześniej uprawnienia do wykonywania,
uprawnienia te zostaną im odebrane.
u+x,go=rx | Nadaje uprawnienia do wykonywania właścicielowi pliku oraz nadaje grupie i pozostałym użytkownikom prawa do odczytu i wykonywania. Kilka kombinacji uprawnień można oddzielić od siebie przecinki

