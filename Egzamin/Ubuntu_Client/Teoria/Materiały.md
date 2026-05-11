# Teoria

Linux jest bardziej skomplikowany niż Windows ponieważ w windowsie możemy sobie coś tam przeklikać i nawet jak nic nie wiemy to można dojść do celu. Na linuxie jest inaczej ponieważ jeśli chcemy cośz robić musimy znać do tego komendę.

Zagadnienia:

- Podstawowe Komendy w linuxie
- Sprawdzanie parametrów systemowych w Linuxie 
- Linux jako client, któremu są świadczone usługi
- Komendy związane z Linux Clientem, Serverem na egzaminie INF02

## Komendy w linuxie

Jeśli nie mamy skonfigurowanego pod nas środowiska to aby coś zrobić w linuxie trzeba znać w nim komendy. Niektóre komendy są proste i będziemy ich używać niemal ciągle podczas konfiguracji systemu z linuxem a niektóre rzadziej jeśli mamy zrobić jakąś konkretną rzecz.

## Podstawowe Polecenia
    

    man ls - wyświetla manual komendy
    ls --help - wyświetla pomoc dla jakiejś komendy 
    ls -h - robi to samo co powyższa komenda ( skrócony zapis )
    
    pwd - wyświetla bieżący katalog (print working directory) 
    cd - zmiana katalogu
    cd /home - przejście do katalogu /home
    cd .. - przejście o jeden katalog w górę
    cd ~ - przejście do katalogu domowego użytkownika

    ls - wyświetlanie zawartości katalogu
    ls -l - szczegółowy widok (długi format)
    ls -la - widok wszystkich plików (także ukrytych)
    ls -la | grep nazwa - filtrowanie wyników
    ls -l - wyświetla uprawnienia w formacie rwxrwxrwx

    mkdir nazwa - tworzenie nowego katalogu

    touch nazwa_pliku - tworzenie pustego pliku

    cp plik1 plik2 - kopiowanie pliku
    cp -r katalog1 katalog2 - kopiowanie katalogu rekursywnie

    mv plik1 plik2 - przenoszenie/zmiana nazwy pliku

    rm plik - usuwanie pliku
    rm -rf katalog - usuwanie katalogu rekursywnie

    rmdir katalog - usuwanie pustego katalogu

    cat plik - wyświetlenie całej zawartości pliku
    
    less plik - przeglądanie pliku strona po stronie
    
    head plik - pierwsze 10 linii pliku
    
    tail plik - ostatnie 10 linii pliku

    grep "wzorzec" plik - wyszukiwanie wzorca w pliku

    chmod 755 plik - rwxr-xr-x (pełne dla właściciela, odczyt+wykonanie dla grupy i innych)
    chmod 644 plik - rw-r--r-- (odczyt+zapis dla właściciela, odczyt dla grupy i innych)
    chmod 777 plik - rwxrwxrwx (pełne uprawnienia dla wszystkich)
    chmod 600 plik - rw------- (odczyt+zapis tylko dla właściciela)

    chmod u+x plik - dodanie uprawnienia wykonania dla właściciela
    chmod g-w plik - odebranie uprawnienia zapisu grupie
    chmod o=r plik - ustawienie tylko odczytu dla innych
    chmod a+rwx plik - dodanie wszystkich uprawnień dla wszystkich

    4 = odczyt (r)
    2 = zapis (w)
    1 = wykonanie (x)

    chown użytkownik plik - zmiana właściciela pliku
    chown użytkownik:grupa plik - zmiana właściciela i grupy
    chown -R użytkownik:grupa katalog - zmiana rekursywna dla katalogu

    chgrp grupa plik - zmiana grupy pliku

    sudo useradd nazwa_użytkownika - dodanie nowego użytkownika
    sudo useradd -m nazwa_użytkownika - dodanie użytkownika z katalogiem domowym
    sudo adduser nazwa_użytkownika - interaktywne dodanie użytkownika

    sudo passwd nazwa_użytkownika - zmiana hasła użytkownika
    passwd - zmiana własnego hasła

    sudo usermod -aG grupa użytkownik - dodanie użytkownika do grupy
    sudo usermod -s /bin/bash użytkownik - zmiana powłoki użytkownika
    sudo usermod -l nowa_nazwa stara_nazwa - zmiana nazwy użytkownika

    sudo userdel użytkownik - usunięcie użytkownika
    sudo userdel -r użytkownik - usunięcie użytkownika wraz z katalogiem domowym

    sudo groupadd nazwa_grupy - tworzenie nowej grupy
    sudo groupdel nazwa_grupy - usuwanie grupy
    groups użytkownik - wyświetlenie grup użytkownika
    id użytkownik - wyświetlenie UID, GID i grup użytkownika

    whoami - wyświetla nazwę aktualnego użytkownika
    who - lista zalogowanych użytkowników
    w - szczegółowe informacje o zalogowanych użytkownikach
    last - historia logowań
    su - użytkownik - przełączanie na innego użytkownika
    sudo -u użytkownik komenda - wykonanie komendy jako inny użytkown

    ifconfig - wyświetlenie/konfiguracja interfejsów sieciowych
    ifconfig -a - wszystkie interfejsy (także nieaktywne)
    ifconfig eth0 192.168.1.10 netmask 255.255.255.0 up - konfiguracja IP
    ip a - nowoczesna alternatywa dla ifconfig
    ip addr show - wyświetlenie adresów IP
    ip link show - wyświetlenie interfejsów sieciowych

    ip addr add 192.168.1.10/24 dev eth0 - dodanie adresu IP
    ip link set eth0 up - włączenie interfejsu
    ip route show - wyświetlenie tabeli routingu
    ip route add default via 192.168.1.1 - dodanie domyślnej bramy

    ping adres - test dostępności hosta
    
    ping -c 4 google.com - ping z ograniczoną liczbą pakietów
    traceroute adres - śledzenie trasy do hosta
    nslookup domena - zapytanie DNS
    dig domena - zaawansowane zapytania DNS
    host domena - proste zapytania DNS

    netstat -tuln - otwarte porty i połączenia
    netstat -rn - tabela routingu
    ss -tuln - nowoczesna alternatywa dla netstat
    ss -t - połączenia TCP
    lsof -i - pliki otwarte przez sieć

    get http://example.com/plik - pobieranie pliku
    curl http://example.com - pobieranie zawartości URL
    curl -O http://example.com/plik - pobieranie pliku z zachowaniem nazwy

    sudo systemctl start usługa - uruchomienie usługi
    sudo systemctl stop usługa - zatrzymanie usługi
    sudo systemctl restart usługa - restart usługi
    sudo systemctl reload usługa - przeładowanie konfiguracji
    systemctl status usługa - status usługi
    systemctl is-active usługa - sprawdzenie czy usługa jest aktywna

    sudo systemctl enable usługa - włączenie autostartu
    sudo systemctl disable usługa - wyłączenie autostartu
    systemctl list-unit-files --type=service - lista usług

    edytor Nano 
    
    nano plik - otwarcie pliku
    Ctrl+O - zapisanie
    Ctrl+X - wyjście
    Ctrl+K - wycięcie linii
    Ctrl+U - wklejenie


    tar -czf archiwum.tar.gz katalog/ - utworzenie archiwum gzip
    tar -xzf archiwum.tar.gz - rozpakowanie archiwum gzip
    tar -tf archiwum.tar.gz - wyświetlenie zawartości archiwum


    zip -r archiwum.zip katalog/ - utworzenie archiwum zip
    unzip archiwum.zip - rozpakowanie zip
    unzip -l archiwum.zip - wyświetlenie zawartości zip


    history - wyświetlenie historii komend
    history | grep nazwa - wyszukiwanie w historii


    /etc/passwd - informacje o użytkownikach
    /etc/group - informacje o grupach
    /etc/shadow - hasła użytkowników (zaszyfrowane)


    /etc/network/interfaces - konfiguracja sieciowa Debian/Ubuntu)
    /etc/sysconfig/network-scripts/ - konfiguracja sieciowa RedHat/CentOS
    /etc/resolv.conf - konfiguracja DNS
    /etc/hosts - lokalne mapowanie nazw na adresy IP


    find /ścieżka -name "nazwa" - wyszukiwanie plików po nazwie
    find /ścieżka -type f -size +100M - wyszukiwanie dużych plików
    
    locate foo.txt                             # Find a file
    locate --ignore-case                       # Find a file and ignore case
    locate f*.txt                              # Find a text file starting with 'f'
    
    which komenda - lokalizacja pliku wykonywalnego komendy
    whereis komenda - lokalizacja plików związanych z komendą


    diff plik1 plik2 - porównanie dwóch plików
    cmp plik1 plik2 - porównanie plików binarnych


    env - wyświetlenie wszystkich zmiennych środowiskowych
    echo $PATH - wyświetlenie zmiennej PATH
    export ZMIENNA=wartość - ustawienie zmiennej środowiskowej


    date - wyświetla aktualną datę i godzinę
    date +%F - wyświetla datę w formacie RRRR-MM-DD
    date +%T - wyświetla aktualny czas (GG:MM:SS)
    date "+%d-%m-%Y %H:%M:%S" - wyświetla datę i czas w formacie (DD-MM-RRRR GG:MM:SS)

    date -s "2026-05-11 14:45:00" - ustawia systemową datę i czas (wymaga sudo)
    date -u - wyświetla czas uniwersalny (UTC)

    %d - dzień miesiąca (01-31)
    %m - miesiąc (01-12)
    %Y - rok (np. 2026)
    %H - godzina (00-23)
    %M - minuta (00-59)
    %S - sekunda (00-59)

    Exit - wychodzi z obecnie zalogowanego użytkownika

    hostname - wyświetla aktualną nazwę systemową komputera
    hostname -f - wyświetla pełną nazwę domenową (Fully Qualified Domain Name)
    hostname -d - wyświetla nazwę samej domeny DNS

    sudo nano /etc/hostname - edycja pliku zawierającego główną nazwę komputera
    sudo nano /etc/hosts - edycja pliku lokalnego mapowania nazw na adresy IP (pozwala przypisać nazwę do konkretnego adresu IP bez udziału serwera DNS)


    sudo chage -l admin01 - wyświetla szczegółowe dane o ważności konta i hasła
    sudo chage -E 2026-03-21 admin01 - ustawia konkretną datę wygaśnięcia konta
    sudo chage -E -1 admin01 - wyłącza wygasanie konta (konto bezterminowe)
    sudo chage admin01 - tryb interaktywny (pozwala ustawić parametry po kolei)

    passwd --help - wyświetla listę opcji zmiany haseł
    sudo passwd -S admin01 - sprawdza status hasła (czy jest ustawione, zablokowane itp.)
    sudo passwd -l admin01 - blokuje hasło użytkownika (uniemożliwia logowanie)
    sudo passwd -u admin01 - odblokowuje hasło użytkownika

    Alias adres =’ip a’  - tworzy alias dla jakieś komendy 

    Ctrl+C - przerwanie działania programu
    Ctrl+Z - wstrzymanie programu (można wznowić bg/fg)
    Ctrl+D - koniec pliku EOF / wylogowanie
    Ctrl+L - czyszczenie ekranu (jak komenda clear)
    Tab - autouzupełnianie
    Ctrl+R - wyszukiwanie w historii komend
    !! - powtórzenie ostatniej komendy
    !n - wykonanie n-tej komendy z histori
    
> Zmiana adresu IP, bramy domyślnej, maski sieciowej, serverów DNS w Linuxie opartym na Ubuntu jest zawarta w Teorii w folderze 'TP-link_Konfiguracja'

## Podstawowe Polecenia służące do diagnostyki na linuxie.
    
    uname -a - wyświetla kompletne informacje o jądrze (kernel), nazwie hosta i architekturze
    lsb_release -a - czytelne informacje o dystrybucji (np. Ubuntu 22.04)
    sudo nano /etc/lsb-release - podgląd pliku konfiguracyjnego wersji systemu
    sudo lspci -v - szczegółowa lista urządzeń podłączonych do szyny PCI
    sudo lscpu - wyświetla parametry procesora (liczba rdzeni, wątków, cache)
    sudo lshw - ogólne informacje o całym sprzęcie (hardware)
    sudo lshw -short - uproszczona, krótka lista podzespołów
    sudo lshw -c memory - wyświetla szczegółowe dane tylko o pamięci RAM

    ╰─○ dmidecode -t
    dmidecode: option requires an argument -- 't'
    Type number or keyword expected
    Valid type keywords are:
          bios
          system
          baseboard
          chassis
          processor
          memory
          cache
          connector
          slot
  
    sudo dmidecode -t baseboard - szczegółowe dane o płycie głównej pobrane z BIOS/UEFI
    sudo lshw -c memory | grep -i size - wyciąga tylko linie dotyczące rozmiaru pamięci
    sudo lshw -short > sprzet.txt - zapisuje listę sprzętu do pliku (nadpisuje plik)
    sudo lscpu | grep -i core >> ram.txt - dopisuje dane o rdzeniach na koniec istniejącego pliku
    

    Jak uzyskać informację o poszczególnych rzeczach na egzamin.


    Informacje o procesorze
        lscpu - szczegółowe informacje o procesorze
        cat /proc/cpuinfo - informacje o procesorze z pliku proc
        sudo dmidecode -t processor - informacje o procesorze z DMI
        
    Informacje o pamięci RAM
        free -m - informacje o pamięci w MB
        free -h - informacje o pamięci w GB
        sudo dmidecode -t memory - szczegółowe informacje o pamięci
        lshw -c memory - informacje o pamięci
        hwinfo --memory - informacje o pamięci (może wymagać instalacji)
        
    Informacje o dyskach
        lsblk - lista urządzeń blokowych
        fdisk -l - lista partycji dyskowych
        sudo fdisk -l | grep -i "disk" - lista dysków
        lshw -c disk - informacje o dyskach
        hdparm -i /dev/sda - informacje o dysku twardym
        
    Informacje o karcie graficznej
        lspci | grep -i vga - informacje o karcie graficznej
        lshw -c display - szczegółowe informacje o karcie graficznej
        
    Informacje o płycie głównej
        sudo dmidecode -t baseboard - informacje o płycie głównej
        sudo dmidecode -t system - informacje o systemie
        
    Informacje o karcie sieciowej
        lspci | grep -i network - lista kart sieciowych
        lshw -c network - szczegółowe informacje o kartach sieciowych


    free -h - pokazuje zużycie pamięci RAM i SWAP w formacie czytelnym dla człowieka (np. GB, MB)
    sudo nano /proc/meminfo - wgląd w surowe dane systemowe o pamięci
    top - klasyczny, tekstowy monitor procesów w czasie rzeczywistym
    htop - nowoczesny, kolorowy i interaktywny monitor procesów

    whoami - wyświetla nazwę aktualnie zalogowanego użytkownika
    users - wyświetla listę wszystkich zalogowanych obecnie użytkowników
    w - pokazuje kto jest zalogowany oraz co aktualnie robi (jakie procesy uruchomił)

    ps - lista procesów aktualnego terminalu
    ps aux - lista wszystkich procesów systemu
    ps -ef - alternatywny format listy procesów

    kill PID - zakończenie procesu o danym PID
    kill -9 PID - wymuszenie zakończenia procesu
    killall nazwa_procesu - zakończenie wszystkich procesów o danej nazwie
    pkill nazwa - zakończenie procesów na podstawie wzorca nazwy

    hostnamectl - informacje o systemie (systemd)
    df -h - informacje o przestrzeni dyskowej
    du -sh katalog - rozmiar katalogu
    uptime - czas działania systemu i obciążen

## Linux Jako Klient, któremu świadczone są usługi
Wszystko w linuxie da się zrobić przez CLI, nie potrzeba GUI lecz czasami kiedy sprawdzamy czy nasz server działa lub kiedy go testujemy to GUI się przydaję - szczególnie do serverów [ ftp , samba , Apache ] ( rzeczy takie jak DHCP, NAT, SSH, DNS będą sprawdzane przez CLI i będą omówione w sekci związanej z Linux Serverem lub Windows Serverem zależnie od usługi )

## Komendy na linuxie na egzaminach INF02
Nie każdy egzamin ma linuxa, dlatego więc nie w wszystich egzaminach trzeba się z nim męczyć czasami na egzaminach mamy połączenie Windows Servera z Linux Clientem lub np. połączenie Linux Servera z Linux Clientem - ( może być wiele opcji ) naszczęście dlatego, że duża część usług wystawianych na windows serverze potrzebuje clienta w systemie Windows linuxa jest trochę mniej - co nie oznacza, że się wogóle nie pojawia.

# Zadania z diagnostyką na linuxie 
<img width="698" height="302" alt="image" src="https://github.com/user-attachments/assets/91f0733c-0745-44db-8e27-0aacdce00cd6" />
<img width="696" height="321" alt="image" src="https://github.com/user-attachments/assets/63fb9abb-6eb4-4d17-ab5a-ac9c3be7ca06" />




# Zadania z ogólną eksploatacją na linuxie 
<img width="717" height="350" alt="image" src="https://github.com/user-attachments/assets/c59615d6-0c71-4640-ace5-857de6187875" />
<img width="699" height="294" alt="image" src="https://github.com/user-attachments/assets/99618095-097a-4263-89b0-0679d7278e88" />
<img width="708" height="261" alt="image" src="https://github.com/user-attachments/assets/ab4d8965-12ab-4723-8c96-bf62c73534ac" />
<img width="709" height="272" alt="image" src="https://github.com/user-attachments/assets/542061ce-1f6b-4322-87b5-7934f8e609e4" />
<img width="699" height="243" alt="image" src="https://github.com/user-attachments/assets/41f35f30-b167-41ed-9bcf-fc9f6cf5fee0" />
<img width="686" height="363" alt="image" src="https://github.com/user-attachments/assets/9cb6c43f-3bf8-4105-9cc7-9737e76a12f5" />
<img width="707" height="277" alt="image" src="https://github.com/user-attachments/assets/c6840e55-1551-4dad-80be-6963b43996c4" />
<img width="694" height="199" alt="image" src="https://github.com/user-attachments/assets/ee925c5a-6bb8-4884-90fb-b327d6432918" />
<img width="704" height="498" alt="image" src="https://github.com/user-attachments/assets/08bdad9b-7a6c-4d44-8ec8-8474a58f5556" />
2023 czerwiec zad 2 







*robić od 2022 styczeń zad 1    




















    

    

  


