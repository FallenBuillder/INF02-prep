# Skrypty
w ostatnich latach na egzaminach INF02 coraz częściej pojawiają się skrypty powłoki ( bash ) i skrypty wsadowe ( bat ) w tej sekcji omówimy wszystkie przykłady z egzaminów w ,których występowało zadanie z napisaniem tego typu skryptów oraz nauczymy cię jak je pisać.
> Powoli na egzaminach INF02 odchodzi się już od arkuszy kalkulacyjnych i zastępuje się je skrypytami !

nie ma zauważalnej różnicy między plikami .bat a plikami .cmd, istnieją wyłącznie małe różnice, których na egzaminie nie będziemt musieli rozróżnić ani się do nich dopasować.

pliki .cmd i pliki .bat pojawią się wtedy kiedy będziemy mieli stworzyć skrypty na Windows 10 / 11 albo na Windows Server 
pliki .sh (shellowe) pojawią się za to kiedy będziemy mieli stworzyć skrypty na Ubuntu Desktopie albo na Ubuntu Serverze

zagadnienia:
- podstawy skryptów wsadowych
- podstaway skryptów shellowych
- Omówienie wszystkich skryptów z egzaminów INF02

# pliki .bat / .cmd

### Teoria 

jak już wcześniej wspomniałem pliki .bat i pliki .cmd to praktycznie to samo a więc jedyną różnicą przy ich tworzeniu / wywoywaniu będzie zmiana rozszerzenia z .bat na .cmd i odwrotnie.
<br>

# pliki .sh 

### Teoria 

Skrypty shellowe ( .sh ) pozwalają nam na automatyzacje codziennych zadań lub wpisywania komend. 

Na egzaminie Praktycznym INF02 ich zadaniem jest sprawdzenie czy umie się ich prosty syntax.

Podstawy bash scriptingu:

***
Aby skrypt był traktowany przez powłoke bash jako skrypt bashowy musi mieć końcówke ( .sh )

    touch Skrypt_shellowy.sh

dodatkowo żeby skrypt był traktowany jako skrypt systemowy musi mieć na początku linijke #!/bin/bash

    #/!bin/bash

W bashu komentarze robimy poprzez hashtag ( # ) 

    # this is a bash script 
    
Bash używa normalnych komend systemowych do interekacji z shellem, czyli komenda echo będzie działała jak print

    echo "Hello World!"
    
Czyli podstawowy skrypt w bashu wyglądałby tak:

    #!/bin/bash
    # This is a bash script
    echo "Hello World!"

W bashu można normalnie używać wszystkich komend, których używałoby się w naszym shellu czyli można zrobić np. taki skrypt

    #!/bin/bash
    # This is a bash script
    mkdir Folder
    cd Folder
    touch plik.txt
    echo "Hello World!" >> plik.txt
    cat plik.txt
    rm -rf plik.txt
    cd ..
    rm -rf Folder

> Oczywiście aby plik .sh się wywołał trzeba dodać mu uprawnienia wykonania czyli:   chmod +x plik.sh
    
W Bashu można także tworzyć zmienne a następnie je wywoływać poprzez znak $ 

    #!/bin/bash
    # Assign a value to a variable
    name="World"
    echo "Hello, $name!"

W Bashu można także wywoływać operacje arytmetyczne i na słowach

    #!/bin/bash
    
    greeting="Hello, "
    name="World"
    echo "$greeting$name"

    # Arithmetic
    num1=5
    num2=10
    sum=$((num1 + num2))
    echo "The sum is $sum"

W bashu mamy także Listy

    #!/bin/bash
    fruits=("apple" "banana" "cherry")
    for fruit in "${fruits[@]}"; do
      echo $fruit
    done

    echo ${fruits[0]} # wypiszę 1 element w liscie
    fruits[1]="Mango" # nadpiszę wartość
    

Występują także struktury klucz:wartość

    #!/bin/bash
    declare -A colors
    colors[apple]="red"
    colors[banana]="yellow"
    colors[grape]="purple"
    unset colors[banana]
    echo ${colors[apple]} # red
    echo ${colors[grape]} # purple

## mamy w bashu także wiele operatorów
<img width="244" height="152" alt="image" src="https://github.com/user-attachments/assets/373253e6-baac-4c2a-bad1-15d55b4f6c15" />
<img width="338" height="101" alt="image" src="https://github.com/user-attachments/assets/edd99cbc-fbc5-4cd8-8d90-72a2ca821db0" />
<img width="417" height="153" alt="image" src="https://github.com/user-attachments/assets/78177186-ce91-430e-851d-a75623bc2d87" />
<img width="148" height="75" alt="image" src="https://github.com/user-attachments/assets/d5313ea1-7962-448a-9e0e-1208fbc7841f" />
<img width="273" height="98" alt="image" src="https://github.com/user-attachments/assets/963aeeab-aa4e-4ee5-8834-3ad9ac28ab5f" />


mamy także w bashu if ,else ,elif statmenty

    #!/bin/bash
    num=10
    if [ $num -gt 10 ]; then
      echo "Number is greater than 10"
    elif [ $num -eq 10 ]; then
      echo "Number is exactly 10"
    else
      echo "Number is less than 10"
    fi

mamy także w bashu pętle for

    for i in {1..5}; do
      echo "Iteration $i"
    done

mamy także pętle while

    count=1
    while [ $count -le 5 ]; do
      echo "Count is $count"
      ((count++))
    done

mamy także pętle Until ( podobne do while ale kończą się jak condition w nawiasach kwadratowych jest prawdziwy )

    count=1
    until [ $count -gt 5 ]; do
      echo "Count is $count"
      ((count++))
    done

mamy także w bashu w pętlach break, continue 

    for i in {1..5}; do
      if [ $i -eq 3 ]; then
        continue
      fi
      echo "Number $i"
      if [ $i -eq 4 ]; then
        break
      fi
    done

mamy także w bashu funkcję

    my_function() {
      echo "Hello, World!"
    }

    my_function() # wywoła

możemy także dać argumenty funkcji 

    greet() {
      local name=$1
      echo "Hello, $name!"
    }
    
    greet "Alice" # wywoła

mozna też w bashu dodawać parametry przy wywoływaniu skryptów.

    #!/bin/bash
    for i in {1..5}; do
        useradd $1$i
    done
> ten skrypt tworzy 5 użytkowników w formacie -> Zmienna1 , Zmienna2 , Zmie.... w zależności od podanej zmiennej 
sudo ./users.sh harry - wywołanie 























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
Aby otworzyć plik należy zrobić na nim prawoklik i kliknąć 'Uruchom jako administrator'
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
Aby uruchomić ten skrypt należy go dwukrotnie kliknąć
***
Edytujemy plik2.bat

    @echo off
    copy C:\Wsadowe\dane\*.%1 C:\Wsadowe\archiwum2\
***
Aby go uruchomić należy wpisać w cmd 'plik2.bat txt'
***
Edytujemy plik3.bat

    @echo off
    echo Nowy wpis w dniu: >> C:\Wsadowe\dane\informacje.txt
    date /t >> C:\Wsadowe\dane\informacje.txt
    dir C:\ >> C:\Wsadowe\dane\informacje.txt
***
Aby uruchomić ten skrypt należy go dwukrotnie klikąć

<img width="1191" height="441" alt="image" src="https://github.com/user-attachments/assets/59ca4c35-8ed2-4aa7-bc16-d3496447aab5" />
Rozwiązanie:
<br>
Tworzymy plik systemowy powitanie.bat bezpośrednio na dysku C:\

***
Edytujemy plik powitanie.bat

    @echo off
    cls
    set /p imie="Podaj imie: "
    echo Witaj %imie%
    pause
***

Aby wykonać plik powitanie.bat należy na niego dwukrotnie kliknąć
