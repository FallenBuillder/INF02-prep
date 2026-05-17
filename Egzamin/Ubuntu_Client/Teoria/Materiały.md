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
 
    sudo apt update – aktualizacja listy dostępnych pakietów i ich wersji w repozytoriach, co pozwala systemowi sprawdzić dostępność nowszych wydań.
    sudo apt upgrade – ulepszenie wszystkich pakietów oraz bibliotek w systemie na nowszą wersję bez usuwania aktualnie zainstalowanych programów.
    apt list --upgradable – wypisanie rzeczy, które są do ulepszenia, co pozwala na szybki przegląd dostępnych aktualizacji przed ich pobraniem.
    
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
    traceroute adres - śledzenie trasy do hosta\
    mtr google.com - polecenie ping , traceroute w jednym ( każdy element ścieżki ) 
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

    ln -s źródło cel
    ln -s /etc skrot_do_etc - tworzy wiązanie symboliczne
    po wykonaniu komendy ls -l powinniśmy zauważyć skrot_do_etc -> /etc (skrót wskazuje na miejsce źródłowe)



    TODO : Dodać tutaj tworzenie i zarządzanie partycjami na Linuxie 



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
        lshw -class disk 
        
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






    TODO: Dodać jak robić reguły na linuxie dla usług 





    

## Linux Jako Klient, któremu świadczone są usługi
Wszystko w linuxie da się zrobić przez CLI, nie potrzeba GUI lecz czasami kiedy sprawdzamy czy nasz server działa lub kiedy go testujemy to GUI się przydaję - szczególnie do serverów [ ftp , samba , Apache ] ( rzeczy takie jak DHCP, NAT, SSH, DNS będą sprawdzane przez CLI i będą omówione w sekci związanej z Linux Serverem lub Windows Serverem zależnie od usługi )

> Zagadnienia te będą trochę krócej omówione w sekcji 'Ubuntu-Server' oraz 'Windows-Server' a więć jeśli wie się o co chodzi nie trzeba czytać tego modułu 

### Jakie usługi może świadczyć server clientowi, który jest na linuxie.
- DHCP
- Routing
- DNS
- Samba
- FTP
- WWW
- SSH

> Konfiguracja powyższych usług jest omowiona w sekcji 'Ubuntu_Server'

### jak sprawić abyśmy mieli dostęp do tych usług na Kliencie ? 

#### <strong>DHCP</strong>
DHCP - Dynamic Host Configuration Protocol - jest protokołem, który pozwala na przypisywanie jakiemuś urządzeniu dynamicznego adresu IP z góry przypisanemu klientowi przez server.
<br>
aby otrzymać adres DHCP na Ubuntu należy zmienić nasze ustawienia karty sieciowej pod takie, które sprawią, że taki adres możemy otrzymać - najlepiej to zrobić graficznie.
<img width="102" height="33" alt="image" src="https://github.com/user-attachments/assets/ae37e219-b2ce-4845-b251-46774387b7ea" />
Wchodzimy w 3 ikonki w prawym górnym rogu
<img width="414" height="465" alt="image" src="https://github.com/user-attachments/assets/9517910e-9264-4652-b3bd-ec93422b334a" />
Następnie w zakładke Wired i klikamy Wired Settings
<img width="570" height="334" alt="image" src="https://github.com/user-attachments/assets/787f6f52-ac0b-498c-86d3-e66a6fb4048d" />
Następnie klikamy w górną ikonke ustawień
<img width="762" height="587" alt="image" src="https://github.com/user-attachments/assets/bd152b57-f4b4-4878-a1f7-5afa763b16ce" />
przechodzimy do sekcji IPv4 i ustawiamy metode otzymywania dresu IP na DHCP
<img width="105" height="49" alt="image" src="https://github.com/user-attachments/assets/134a11ca-4884-414a-8d29-a68d0c4a3f21" />
Na końcu klikamy 'Apply'

Teraz przez to, że nasz adres IP jest otrzymywany przez server DHCP nasz klient powinien znaleść go w sieci i otrzymać od niego adres.

To czy otrzymaliśmy adres IP z zakresu lub dzierżawy, którą ustaliliśmy na serverze DHCP pokaże nam komenda 'ip a'
<img width="828" height="588" alt="image" src="https://github.com/user-attachments/assets/e3b7e48b-ff16-4a09-aedb-efcf6627b54d" />

#### <strong>Routing</strong>

Jako klient chcemy mieć możliwość korzystania z internetu. Aby to zrobić trzeba sprawić, że nasze zapytania do różnego typu usług, które są wystawione na innych serverach do nich docierają.

Służy do tego usługa routingu 

jako klient nie mamy zabardzo sposobu dzięki, któremu możemy otrzymać dostęp do tej usługi - jedynym sposobem jest ustawienie naszego adresu IP bramy domyślnej w komputerze na interfejs LANowy naszego servera. ( w sytuacji kiedy komputer jest bezpośrednio lub przez switcha podłączony do servera ) dzięki temu wszystkie zapytania, które będą wychodzić do internetu muszą przejść przez nasz server. Co oznacza, że jeśli na serverze skonfigurowana jest skonfigurowana obsługa routingu, będziemy mogli rozmawiać z światem zewnętrznym. 

#### <strong>DNS</strong>
DNS - Domains Name System jest to protokół, który służy do zamiany adresów IP na nazwy domenowe i odwrotnie 

Aby połączyć się do servera DNS i otrzymywać od niego adresy IP trzeba się upewnić, że ustawiliś my go jako nasz server DNS w ustawieniach karty sieciowej. Co oznacza ,że robimy to samo co przy serverze DHCP jedynie zmieniamy Adres servera DNS na server DNS w naszej lokalnej podsieci 

Zakładając, że nasz server DNS będzie pod adresem 192.168.0.1 nasza konfiguracja będzie wyglądała następująco
<img width="756" height="499" alt="image" src="https://github.com/user-attachments/assets/daccfcfa-7be7-4427-a65e-9b934f13773e" />
> Można ustawić w ustawieniach servera DHCP aby także automatycznie przypisywał nam server DNS, wtedy klikamy Automatic

#### <strong>Samba</strong>

Dzięki Sambie możemy udostępniać pliki oraz na nich pracować co sprawia, że mamy do nich łatwą dostępnosć w sieci

Aby połączyć się do servera Samba ( podobnie jak do serva FTP należy najpierw wejść do 'Eksploratora plików'
<img width="71" height="69" alt="image" src="https://github.com/user-attachments/assets/f5c1fadf-34ef-4f6b-afb4-00e92c7dbc1b" />
<img width="900" height="552" alt="image" src="https://github.com/user-attachments/assets/6effa5ca-4913-45b6-90ea-81066710c0e1" />
Po zescrollowaniu na dół widzimy Zakładke 'Other Locations' - ( po polsku będzie inaczej na INF02 ) 
<img width="895" height="549" alt="image" src="https://github.com/user-attachments/assets/b76d1e65-0501-4b2e-8e41-24810cdb1d1a" />
po kliknięciu tej zakładki pojawia się nam okienko w, którym można następnie połączyć się z serverem na, którym wystawiane są nasze pliki.
<img width="705" height="51" alt="image" src="https://github.com/user-attachments/assets/75c76876-84ab-4039-a034-56611d24fa08" />
Aby to zrobić należy wpisać w pasku na dole adres Servera z, którym chcemy się połączyć.

<strong>czyli należy poprostu wpisać na dole w pasku nazwę usługi a następnie adres IP czyli:   'Usługa'://'Adres IP' </strong>
<img width="906" height="617" alt="image" src="https://github.com/user-attachments/assets/bcdc1d76-4e9d-4fc7-894c-04a33eed309d" />
Jeśli server jest skonfigurowany będą widoczne zasoby, które tam umieściliśmy 


#### <strong>FTP</strong>

Dzięki FTP ( File Transfer Protocol ) - możemy pobierać oraz wysyłać pliki. Jedyną różnicą między FTP a sambą jest to, że Samba skupia się na wygodzie i faktycznym jej użyciu w firmach i korporacjach a FTP służy bardziej tylko jako miejsce z, którego można pobierać jakieś np. Pakiety lub aplikacje 

Aby połączyć się z serverem FTP jedyne co musimy zmienić w naszym 'pasku wyszukiwania' to nazwa usługi - w tym przypadku na ftp:// 

czyli mamy:

<img width="709" height="49" alt="image" src="https://github.com/user-attachments/assets/c2ef66bb-704b-45c2-b4dc-fa74d265d8fb" />
Jeśli server został prawidłowo skonfigurowany będziemy mogli zobaczyć na nim pliki
<img width="903" height="610" alt="image" src="https://github.com/user-attachments/assets/7ac864ba-2415-4fe2-b743-5fd956bc4177" />

#### <strong>WWW</strong>

myśle, że każdy wie jak dostać się do strony internetowej. Wystarczy wyszukać jej nazwę a nastepnie przeglądarka wypluje nam wyniki podobne do tego co wyszukaliśmy.

Jeśli chcemi się połączyć z naszą przeglądarką WWW należy poprostu w przeglądarce wpisać jej adres IP i opjonalnie numer portu na, którym jest ona wystawiona 
<img width="964" height="238" alt="image" src="https://github.com/user-attachments/assets/93f1bc1e-cc37-411c-8ede-46d5aad50e72" />

Aby zmienic port przy wyszukiwaniu jakiejś strony wystarczy po adresie IP napisać dwukropek i port na, którym wystawiliśmy wcześniej naszą stronę
<img width="193" height="33" alt="image" src="https://github.com/user-attachments/assets/33591b44-dd58-4eb6-801a-93e1b42574ab" />

#### <strong>SSH</strong>

SSH ( Secure Shell ) - jest protokołem komunikacjnym, który pozawala nam na uzyskanie stabilnej szyfrowanej powłoki z systemem, który chcemy skonfigurować. 

Aby dostać się do servera, który ma wystawioną usługe SSH jedyne co należy zrobić to wpisać w terminalu Linuxowym / Windowsowym komende

ssh Host@IP

czyli np:

ssh admin@192.168.10.10

dzięki tej komendzie, jeśli server SSH jest skonfigurowany prawidłowo i wpisaliśmy poprawne hasło użytkownika admin będziemy w stanie uzyskać szyfrowane połączenie z naszym serverem i zacząć go konfigurować.


## Komendy na linuxie na egzaminach INF02
Naszczęście nie każdy egzamin ma linuxa, może czasami być Windows i Linux a czasami Windows i Windows itd.. Naszczęście będzie raczej więcej Windowsa bo wiele usług, które są na windowsie poprostu potrzebują klienta, który też ma Windowsa 

# Zadania z diagnostyką na linuxie 
<img width="712" height="459" alt="image" src="https://github.com/user-attachments/assets/2bb45027-072c-49ba-a5e2-500c54452d1a" />
<img width="696" height="437" alt="image" src="https://github.com/user-attachments/assets/14880f2a-bea5-4026-a42f-66f1150bd38f" />
<img width="698" height="302" alt="image" src="https://github.com/user-attachments/assets/91f0733c-0745-44db-8e27-0aacdce00cd6" />
<img width="703" height="332" alt="image" src="https://github.com/user-attachments/assets/5a311d77-72b3-4d0e-8adf-e716a74c2c0e" />
<img width="707" height="277" alt="image" src="https://github.com/user-attachments/assets/c6840e55-1551-4dad-80be-6963b43996c4" />
<img width="694" height="199" alt="image" src="https://github.com/user-attachments/assets/ee925c5a-6bb8-4884-90fb-b327d6432918" />
<img width="711" height="217" alt="image" src="https://github.com/user-attachments/assets/26abac49-2eb5-42e8-97c8-dacf1bc9388d" />
<img width="699" height="56" alt="image" src="https://github.com/user-attachments/assets/6769a76c-c999-455d-8445-8e1b6ac774ef" />
<img width="705" height="587" alt="image" src="https://github.com/user-attachments/assets/ce5599e5-bbdc-483e-8b92-7f5e1d333441" />
<img width="700" height="202" alt="image" src="https://github.com/user-attachments/assets/25795e70-d830-4425-8da2-d3d9174f9db9" />
<img width="699" height="198" alt="image" src="https://github.com/user-attachments/assets/d5ebf4a5-813f-4622-908d-7d796712d790" />
<img width="689" height="173" alt="image" src="https://github.com/user-attachments/assets/c0720314-f1ef-495b-97d8-eb11309839c6" />
<img width="696" height="249" alt="image" src="https://github.com/user-attachments/assets/cfd897d7-c3c7-4add-a93e-7038a0b66325" />
<img width="703" height="176" alt="image" src="https://github.com/user-attachments/assets/9eddac39-31e2-469a-b7e8-9276713a5baf" />
<img width="701" height="288" alt="image" src="https://github.com/user-attachments/assets/0908d956-5f4c-477c-a1a5-49ef5b3d2087" />
<img width="700" height="81" alt="image" src="https://github.com/user-attachments/assets/21c3d7ef-b14b-4bb6-b10f-3ac8105a0293" />
<img width="697" height="445" alt="image" src="https://github.com/user-attachments/assets/d1562048-8f49-4db8-84fb-85af1fa4268b" />
<img width="702" height="121" alt="image" src="https://github.com/user-attachments/assets/f2bf5ae7-4adb-4036-97a2-d03f5d939105" />
<img width="695" height="247" alt="image" src="https://github.com/user-attachments/assets/c21b2306-9100-46c1-b7e3-39f34d9563d2" />
<img width="697" height="125" alt="image" src="https://github.com/user-attachments/assets/b63d84f5-5630-44f6-9b13-366b98e6d18e" />
<img width="565" height="201" alt="image" src="https://github.com/user-attachments/assets/e7399a65-b264-4897-aa65-2271566c664f" />
<img width="719" height="138" alt="image" src="https://github.com/user-attachments/assets/cbc5159a-08ac-40e2-b056-21594b59cea6" />
<img width="469" height="176" alt="image" src="https://github.com/user-attachments/assets/df1d6f76-0f62-40cf-95a1-4b7011bd0c76" />


# Zadania z ogólną eksploatacją na linuxie 
<img width="717" height="350" alt="image" src="https://github.com/user-attachments/assets/c59615d6-0c71-4640-ace5-857de6187875" />
<img width="696" height="321" alt="image" src="https://github.com/user-attachments/assets/63fb9abb-6eb4-4d17-ab5a-ac9c3be7ca06" />
<img width="699" height="294" alt="image" src="https://github.com/user-attachments/assets/99618095-097a-4263-89b0-0679d7278e88" />
<img width="708" height="261" alt="image" src="https://github.com/user-attachments/assets/ab4d8965-12ab-4723-8c96-bf62c73534ac" />
<img width="709" height="272" alt="image" src="https://github.com/user-attachments/assets/542061ce-1f6b-4322-87b5-7934f8e609e4" />
<img width="699" height="243" alt="image" src="https://github.com/user-attachments/assets/41f35f30-b167-41ed-9bcf-fc9f6cf5fee0" />
<img width="686" height="363" alt="image" src="https://github.com/user-attachments/assets/9cb6c43f-3bf8-4105-9cc7-9737e76a12f5" />
<img width="704" height="498" alt="image" src="https://github.com/user-attachments/assets/08bdad9b-7a6c-4d44-8ec8-8474a58f5556" />
<img width="701" height="190" alt="image" src="https://github.com/user-attachments/assets/5f76dcbe-7675-4d6b-8345-73d95b0b6918" />
<img width="701" height="530" alt="image" src="https://github.com/user-attachments/assets/dbd4ed2c-ba5c-4542-9ae3-0b7f9cb740b0" />
<img width="705" height="669" alt="image" src="https://github.com/user-attachments/assets/dddbdf4f-496a-40e8-ac27-62552ead13a9" />
<img width="725" height="329" alt="image" src="https://github.com/user-attachments/assets/fd19824c-d9a2-4e6b-9293-323dc207b7f9" />
<img width="693" height="341" alt="image" src="https://github.com/user-attachments/assets/e81d8b92-f127-4c23-8ac1-914e09cce2aa" />
<img width="707" height="468" alt="image" src="https://github.com/user-attachments/assets/7f1cfb42-2a5e-4665-a42f-a27912644762" />
<img width="703" height="533" alt="image" src="https://github.com/user-attachments/assets/9297bccf-ef4c-4a55-9421-304e1425dd1f" />
<img width="652" height="359" alt="image" src="https://github.com/user-attachments/assets/edc10f61-a6b4-4a1c-966f-5a3c4f5eea86" />
<img width="709" height="404" alt="image" src="https://github.com/user-attachments/assets/53b2fddd-917b-4719-b0e5-01b4c8778d6a" />
<img width="712" height="419" alt="image" src="https://github.com/user-attachments/assets/b5345f44-3287-40a4-a342-d4546ac426f8" />
<img width="701" height="413" alt="image" src="https://github.com/user-attachments/assets/2c251840-6cf3-45f9-a7db-5caaaa012fb7" />
<img width="709" height="297" alt="image" src="https://github.com/user-attachments/assets/50917ff3-692b-4374-87cb-6a334ed05984" />
<img width="714" height="231" alt="image" src="https://github.com/user-attachments/assets/fc497237-35b8-4b45-ad1d-2abac526e336" />
<img width="651" height="236" alt="image" src="https://github.com/user-attachments/assets/3649e68e-beab-407f-a8fb-93825f70d340" />
<img width="715" height="410" alt="image" src="https://github.com/user-attachments/assets/c3422d39-0269-4abf-9b08-44bad11c12c9" />
<img width="739" height="417" alt="image" src="https://github.com/user-attachments/assets/c723a697-8a24-497e-b1c2-f8fb228c86df" />
<img width="708" height="42" alt="image" src="https://github.com/user-attachments/assets/7e49cf3c-fe59-4360-b8c9-be65ddf0e0ad" />


> Dodać zadania z 2026 Zima.

> Dodać do notatki rzeczy, które pojawiły się na egzaminie związane z linuxem ale nie ma notatce.




















    

    

  


