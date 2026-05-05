# Skrypty
w ostatnich latach na egzaminach INF02 coraz częściej pojawiają się skrypty powłoki ( bash ) i skrypty wsadowe ( bat ) w tej sekcji omówimy wszystkie przykłady z egzaminów w ,których występowało zadanie z napisaniem tego typu skryptów oraz nauczymy cię jak je pisać.
> Powoli na egzaminach INF02 odchodzi się już od arkuszy kalkulacyjnych i zastępuje się je skrypytami !

nie ma zauważalnej różnicy między plikami .bat a plikami .cmd, istnieją wyłącznie małe różnice, których na egzaminie nie będziemt musieli rozróżnić ani się do nich dopasować


## Skrypty z 2021-2026 roku 
<br>
<img width="677" height="237" alt="image" src="https://github.com/user-attachments/assets/86818d59-7f47-4036-b29c-c898512017e0" />
<br>
Rozwiązanie:
<br>
nano konfiguracja.sh
*** 

    #!/bin/bash
    groupadd informatycy
    usermod -aG informatycy administrator
    groupmod -g 1111 informatycy

***
<br>
chmod +x konfiguracja.sh

sudo ./konfiguracja.sh

> tar -cvf konfiguracja.tar konfiguracja.sh - dodatkowo jeszcze jest tutaj utworzenie archiwum. ( Komendy tego typu będą znajdować się w pliku 'Windows-Client','Windows-Server'

<img width="674" height="180" alt="image" src="https://github.com/user-attachments/assets/00699952-3a05-4725-a9ab-6df479a2ee68" />
Rozwiązanie:

tworzymy na pulpicie plik .bat o nazwie konto.bat ( przez stworzenie pliku tekstowego i zmienienie rozszerzenia )
***

    @echo off
    net user tester /add
    net localgroup testerzy /add
    net localgroup testerzy tester /add

***
<br>
Aby otworzyć plik należy zrobić na niego prawoklik i kliknąć 'Uruchom jako administrator'
<br>
<img width="677" height="135" alt="image" src="https://github.com/user-attachments/assets/0c5ae09f-ace7-4cef-bf42-aa7047aea66a" />

Rowzwiązanie:

Utwórz na pulpicie plik student.txt a następnie zmień jego rozszerzenie na student.cmd. Następnie go zedytuj

***
    @echo off
    FOR /L %%i IN (1, 1, 5) DO (
        net user student_%%i /add
    )

***


## Skrypty z 2026 roku
<img width="896" height="330" alt="image" src="https://github.com/user-attachments/assets/518f74e5-a41a-4860-a8cf-3741d242d72c" />
Rozwiązanie:
<br>
nano konta.sh

***

    #!/bin/bash
    for i in {1..5}; do
        useradd -m -d /home/$2$i $1$i
    done

***
chmod +x konta.sh

sudo ./konta.sh uczen 3TI

<img width="777" height="455" alt="image" src="https://github.com/user-attachments/assets/370a6132-a0cb-4237-9b8d-f0c4682ed9dd" />
Rozwiązanie:
<br>
Tworzymy folder C:\Wsadowe a następnie kopiujemy do tego folderu foldery archiwum1, archiwum2, dane 

Następnie tworzymy 3 pliki wsadowe
- plik1.bat
- plik2.bat
- plik3.bat

***
Edytujemy plik1.bat

    @echo off
    copy C:\Wsadowe\dane\*.* C:\Wsadowe\archiwum1\
***
<br>
Aby uruchomić ten skrypt należy go dwukrotnie kliknąć


***
Edytujemy plik2.bat

    @echo off
    copy C:\Wsadowe\dane\*.%1 C:\Wsadowe\archiwum2\
***
<br>
Aby go uruchomić należy wpisać w cmd 'plik2.bat txt'


***
Edytujemy plik3.bat

    @echo off
    echo Nowy wpis w dniu: >> C:\Wsadowe\dane\informacje.txt
    date /t >> C:\Wsadowe\dane\informacje.txt
    dir C:\ >> C:\Wsadowe\dane\informacje.txt
***
<br>
Aby uruchomić ten skrypt należy go dwukrotnie klikąć



<img width="1191" height="441" alt="image" src="https://github.com/user-attachments/assets/59ca4c35-8ed2-4aa7-bc16-d3496447aab5" />

