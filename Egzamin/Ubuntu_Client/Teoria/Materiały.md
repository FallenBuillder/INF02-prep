# Teoria

Linux jest bardziej skomplikowany niż Windows ponieważ w windowsie możemy sobie coś tam przeklikać i nawet jak nic nie wiemy to można dojść do celu. Na linuxie jest inaczej ponieważ jeśli chcemy cośz robić musimy znać do tego komendę.

Zagadnienia:

- Podstawowe Komendy w linuxie
- Sprawdzanie parametrów systemowych w Linuxie 
- Linux jako client, któremu są świadczone usługi

## Komendy w linuxie

Jeśli nie mamy skonfigurowanego pod nas środowiska to aby coś zrobić w linuxie trzeba znać w nim komendy. Niektóre komendy są proste i będziemy ich używać niemal ciągle podczas konfiguracji systemu z linuxem a niektóre rzadziej jeśli mamy zrobić jakąś konkretną rzecz.

## Podstawowe Polecenia

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


    
    

    Ctrl+C - przerwanie działania programu
    Ctrl+Z - wstrzymanie programu (można wznowić bg/fg)
    Ctrl+D - koniec pliku EOF / wylogowanie
    Ctrl+L - czyszczenie ekranu (jak komenda clear)
    Tab - autouzupełnianie
    Ctrl+R - wyszukiwanie w historii komend
    !! - powtórzenie ostatniej komendy
    !n - wykonanie n-tej komendy z histor
    
























    

    

  


