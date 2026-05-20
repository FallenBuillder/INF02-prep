# Teoria 

Ubuntu Server. Bez dwóch zdań jedna z gorszych rzeczy, które są do skonfigurowania na egzaminie.. W tym dziale będę omawiał jak Ubuntu server działa , Usługi z nim związane oraz teorie związaną z eksploatacją / konfiguracją ów servera.

> [!CAUTION]
> Podstawowe komendy związane z linuxem nie będą omawiane w tym dziale jeśli ktoś czuje się niepewny z komendami ,CLI i generalnie linuxem niech najlepiej przeczyta najpierw dział 'Ubuntu_Client'.

będą w tym dziale omawiał jedynie komendy ściśle związane z Ubuntu Server, które są potrzebne do jego eksploatacji.

Zagadnienia:

- Podstawowe polecenia w Linuksie związane z Ubuntu Server ( na końcu ) 
- Serwer DHCP w Ubuntu Server
- Routing i NAT w Ubuntu Server 
- Serwer DNS w Ubuntu Server 
- Serwer SAMBA w Ubuntu Server
- Serwer WWW - Apache w Ubuntu Server ( podstawy do egzaminu )
- Serwer FTP w Ubuntu Server
- SSH w Ubuntu Server

## 50-cloud-init.yaml

Plik '/etc/netplan/50-cloud-init.yaml' służy nam do konfiguracji interfejsów sieciowych servera Ubuntu.

Jak go Skonfigurować ?

Pierwszym krokiem jest otwarcie go w edytorze tekstowym takim jak vim lub nano - dla przykładu użyjemy nano 

<strong>UWAGA: Formatowanie w pliku 50-cloud-init.yaml jest bardzo wybredne i każda spacja się liczy</strong>


Komendy potrzebne do konfiguracji naszego pliku.
```
sudo nano /etc/netplan/50-cloud-init.yaml
sudo netplan try
sudo netplan apply
```

po wpisaniu komendy 'sudo nano /etc/netplan/50-cloud-init.yaml' przechodzimy do konfiguracji pliku.

Tak wyglądałaby przykładowa pełna konfiguracja netplana:

<img width="350" height="538" alt="image" src="https://github.com/user-attachments/assets/52f093f8-4e6a-424e-ad32-d17a493c6e4b" />

Wytłumaczenie 
```



network: – Główny kontener (korzeń) całej konfiguracji sieciowej. Mówi systemowi: „tutaj zaczynają się ustawienia sieci”.

version: 2 – Określa wersję formatu Netplan. Obecnie standardem jest wersja 2.

ethernets: – Sekcja, w której definiuje się przewodowe karty sieciowe (karty Ethernet).



1. Pierwsza karta sieciowa: enp0s3 ( NIC1 )
Ta karta pełni rolę głównego połączenia z Internetem (bramy domyślnej).

enp0s3: – Identyfikator systemowy pierwszej karty sieciowej.

addresses:

- "10.15.0.19/24" – Przypisuje karcie statyczny adres IP 10.15.0.19. /24 to maska podsieci (odpowiednik 255.255.255.0), co oznacza, że karta działa w sieci lokalnej od 10.15.0.1 do 10.15.0.254.

nameservers: – Sekcja konfiguracji serwerów DNS (odpowiedzialnych za tłumaczenie nazw stron, np. google.com, na adresy IP).

addresses: – Lista adresów DNS:

- 8.8.8.8 – Główny DNS (publiczny serwer Google).

- 1.1.1.1 – Zapasowy DNS (publiczny serwer Cloudflare).

search: [] – Lista wyszukiwania domen lokalnych (pusta, czyli brak domyślnego dopisywania sufiksów domenowych).

routes: – Sekcja definiująca routing (ścieżki ruchu sieciowego).

- to: "default" – Określa trasę domyślną (czyli gdzie wysyłać cały ruch wychodzący poza sieć lokalną, np. do Internetu).

via: "10.15.0.1" – Adres IP bramy sieciowej (routera), przez który ten ruch ma przechodzić.

match: – Reguła dopasowania sprzętowego. Służy do upewnienia się, że te ustawienia trafią na właściwą fizyczną/wirtualną kartę.

macaddress: 08:00:27:CD:54:13 – System powiąże tę konfigurację tylko z kartą, która ma dokładnie taki adres sprzętowy MAC (unikalny identyfikator VirtualBox).

set-name: NIC1 – Zmienia systemową nazwę tej karty na własną: NIC1 (łatwiejszą do identyfikacji).


2. Druag Karta sieciowa: enp0s8 ( NIC2 )

Więkoszość ustawień w tej karcie jest identyczne oprócz dodania

optional: true - lecz ta linijka nie jest potrzebna na egzaminie jest tutaj tylko ze względu, że jestem na maszynioe wirtualnej 


```
# Server DHCP

Instalacja

> Na Egzaminie pakiet jest już zainstalowany.

Przed Instalacją należy upewnić się, czy ma się połączenie z internetem

<img width="444" height="89" alt="image" src="https://github.com/user-attachments/assets/1c929e30-b61e-4c8f-8e4a-44e6514fb001" />


```
sudo apt update && sudo apt upgrade -y    - pobranie najowszych pakietów i pobranie nowych wersji rzeczy w naszym systemie.
sudo apt install isc-dhcp-server          - Instalacja Usługi.
```


Komendy do zarządzania Usługą isc-dhcp-server.

```
sudo systemctl status isc-dhcp-server    -  Sprawdza czy server DHCP działa poprawnie
sudo systemctl restart isc-dhcp-server   -  restartuje server pod nową konfigurację
sudo systemctl start isc-dhcp-server     -  Sprawia, że server DHCP włączy się ponownie po wyłączeniu i włączeniu Servera 
man 5 dhcpd.conf                         -  manual usługi 
```

pliki do konfiguracji Usługi isc-dhcp-server.

```
/etc/default/isc-dhcp-server             -  Wybranie interfejsu na, którym wystawiona będzie usługa.
/etc/dhcp                                -  folder z konfiguracją Servera DHCP
/etc/dhcp/dhcpd.conf                     -  konfiguracja działania serera oraz jego ustawienia.

```


## Konfiguracja

## Krok1. Ustawienie Interfejsu na, którym wystawione będzie usługa.

<img width="833" height="307" alt="image" src="https://github.com/user-attachments/assets/77719ca1-19f0-438e-b1a2-c442fc848aee" />

Po użyciu komendy 'ip a' sprawdzamy nazwę interfejsu LAN naszego servera i ją zapamiętujemy . 

Następnym krokiem jest zmodyfikowanie pliku.

<img width="1280" height="803" alt="image" src="https://github.com/user-attachments/assets/ee0a5719-36bc-400e-b213-33d02f1ef5bb" />

<br>

## krok2. Konfiguracja Servera 

UWAGA: Warto zrobić kopię pliku konfiguracyjnego przed tym jak zaczniemy w nim grzebać ale nie trzeba tego robić.
```
cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf-kopia
```

Wchodzimy do pliku /etc/dhcp/dhcpd.conf oraz odkomentuwojemy #authoritative; - ponieważ nasz server jest jedynym, głównym serverm DHCP w naszej sieci.

<img width="1273" height="799" alt="image" src="https://github.com/user-attachments/assets/df0072aa-9b3e-4949-a6b0-42db27e86f28" />

Po zjechaniu w dół widzimy faktyczną konfigurację servera, należy ją odkomentować.

<img width="486" height="187" alt="image" src="https://github.com/user-attachments/assets/ed2d915a-9495-4592-a8d3-a4c751a1bec6" />

<img width="505" height="185" alt="image" src="https://github.com/user-attachments/assets/0d01a64c-2c90-4392-8012-6958957e0b45" />

Następnie wypełniamy konfigurację parametrami, które zostały nam podane na egzaminie. - W tym przypadku wypełnie konfigurację przykładowymi wartościami.

<img width="508" height="183" alt="image" src="https://github.com/user-attachments/assets/ff1526d4-7545-4f15-8134-6cf60ba71583" />

Znaczenia poszczególnych parametrów
```
subnet 192.168.10.0    -    oznacza adres sieciowy w naszego interfejsu LAN
netmask 255.255.255.0  -    oznacza maskę posieci naszego interfejsu LAN
range 192.168.10.50 192.168.10.100 - oznacza zakres adresów IP, które są dawane przez server DHCP
option domain-name-server 192.168.10.1 - oznacza server DNS jaki otrzyma klient jeśli otrzymywanie servera DNS jest ustawione jako automatyczne
option domain-name "internal.example.org" - Ustawia przyrostek (sufiks) lokalnej domeny. Jeśli klient spróbuje wyszukać hosta o nazwie server, automatycznie dołączy ten przyrostek i wyśle zapytanie o server.internal.example.org.
option routers 192.168.10.1 - wkazuje adres IP bramy domyślnej jaką otrzyma host
option broadcast-address 192.168.10.255 - adres rozgłoszeniowy interfejsu LAN servera
default-lease-time 600 - czas w sekundach w jakim klient trzyma swój adres IP ( defaultowy ) 
max-lease-time 7200 - maksymalny czas jaki klient może mieć adres IP przypisany przez server DHCP.
```

## krok3. Utworzenie Statycznej Dzierżawy adresu dla klienta.

Scrollujemy w dół

Odkomentuwojemy tą sekcję.

<img width="312" height="75" alt="image" src="https://github.com/user-attachments/assets/9403c1f7-7187-4174-a483-107585f70a98" />

<img width="324" height="67" alt="image" src="https://github.com/user-attachments/assets/79884479-a9f0-42a8-b9e8-fea32377080e" />

Wypełniamy konfigurację

<img width="325" height="68" alt="image" src="https://github.com/user-attachments/assets/4ef733ac-97e7-4fcf-89d3-f9b97b9a3600" />

Znaczenia poszczególnych parametrów 
```
host harry123                        - definiuje unikalną nazwę (identyfikator) dla rezerwacji hosta w pliku konfiguracyjnym
hardware ethernet 08:00:27:2C:74:3E  - Określa fizyczny adres MAC (08:00:27:2C:74:3E) karty sieciowej typu Ethernet należącej do tego konkretnego klienta.
fixed-address 192.168.10.150;        - Wskazuje stały adres IP (192.168.10.150), który serwer DHCP ma zawsze przypisywać urządzeniu o dopasowanym wyżej adresie MAC.
```

## krok4. Zresetowanie / sprawdzenie działania usługi.

Wpisujemy komendę :
```
sudo systemctl restart isc-dhcp-server
```
aby zapisać zmiany, które dokonaliśmy na serverze.

Nastepnie wpisujemy komendę :
```
sudo systemctl status isc-dhcp-server
```
Aby sprawdzić czy konfiguracja została wykonana prawidłowo.

<img width="993" height="401" alt="image" src="https://github.com/user-attachments/assets/5020a525-adcc-4499-bf61-5c1029b1b95d" />

Jeśli wszystko jest zielone powinno być OK, lecz jeśli pojawi się czerwony tekst a usługa wejdzie w stan 'Failed' oznacza to, że mam błąd w konfugracji lub adresacji.

Po zmianię karty na DHCP oraz sprawdzeniu adresu IP otrzymaliśmy statyczny Lease ( Adres IP ) od servera.

<img width="740" height="483" alt="image" src="https://github.com/user-attachments/assets/ec2f88c0-74d7-4d3e-a6be-5bcd8d13dc7a" />

<img width="1021" height="245" alt="image" src="https://github.com/user-attachments/assets/22cab411-5c2d-4279-8080-bfca6ec01adb" />





# Routing / NAT

pliki do konfiguracji Usługi routingu.

```
/etc/sysctl.conf
```

komendy potrzebne do konfiguracji usługi routingu.

```
sudo sysctl -p
sudo iptables -t nat -o enp0s3 -A POSTROUTING -j MASQUERADE         - gdzie '-o' odnosi się do nazwy intefejsu WAN karty sieciowej Servera.
sudo iptables-save
```

## Krok1.

edycja pliku /etc/sysctl.conf 

<img width="1272" height="799" alt="image" src="https://github.com/user-attachments/assets/ae336961-7aaf-4fd1-86dd-50da6d6bf990" />

jedyną zmianą w tym pliku jest odkomentowanie net.ipv4.ip_forward=1. Po to aby server zaczoł zachowywać się jak router i przekazywał dalej pakiety.

wpisujemy następnie komendę:

```
sudo sysctl -p 
```

Aby zapisać zmiany w pliku.

## krok2.

Wpisujemy komendę 
```
sudo iptables -t nat -o enp0s3 -A POSTROUTING -j MASQUERADE
```
wpisanie tej komendy pozwala uruchomić na naszym interfejsie WAN maskarade (MASQUERADE), czyli najpopularniejszą odmianę NAT (Network Address Translation). Pozwalającą urządzeniom z naszej sieci wewnętrznej na korzystanie z internetu za pośrednictwem serwera, który konfigurujemy.

Aby zapisac zmiany spowodowane przez powyższą komendę wpisujemy komendę

```
sudo iptables-save
```

<img width="696" height="226" alt="image" src="https://github.com/user-attachments/assets/ff64c8cc-5c36-48bb-b772-60a62492c16c" />


Konfiguracja Routingu jest zakończona. Mamy teraz dostęp do internetu. ( Nie ma jeszcze usługi DNS )

<img width="635" height="313" alt="image" src="https://github.com/user-attachments/assets/27c2cfaa-9257-4f87-900b-ba98e46b3b15" />



# Server DNS

Na egzaminie Konfiguracja servera DNS nie jest aż tak trudna niż na lekcjach ponieważ trzeba zrobić o wiele mniej.

pliki do konfiguracji usługi DNS

```
/etc/bind                  -    miejsce z plikami konfiguracyjnymi servera

- db.127                   - konfiguracja strefy przeszukiwania do tyłu
- db.local                 - konfiguracja strefy przeszukiwania do przodu
- named.conf               - globalna konfiguracja DNS
- named.conf.default-zones - domyślne strefy przeszukiwania ( plik , określenie mastera )
- named.conf.local         - lokalna konfiguracja DNS
- named.conf.options       - konfiguracja serwera DNS

/etc/resolv.conf           - wybranie, którego servera DNS ma używać nasz server
```
Komendy potrzebne do konfiguracji usługi DNS

```
sudo apt install -y bind9 bind9utils bind9-doc dnsutils   -  instaluje usługę
dig
nslookup
ping
```


## Krok1. Oznajomienie się z konfiguracją.

<img width="539" height="245" alt="image" src="https://github.com/user-attachments/assets/870c467c-19c0-44f1-b275-d51485436667" />

Po wypisaniu plików konfiguracyjnych bind9 pliki, których będziemy potrzebowali są następujące 

- db.127 - przykładowa konfiguracja strefy przeszukiwania wstecznego
- db.local - przykładowa konfiguracja strefy przeszukiwania do przodu
- named.conf - globalna konfiguracja DNS
- named.conf.default-zones - domyślne strefy przeszukiwania
- named.conf.local - lokalna konfiguracja DNS
- named.conf.options - konfiguracja serwera DNS

<strong>UWAGA: Nie należy wchodzić do plików konfiguracyjnych bez sudo bo nie będziemy potem w stanie ich zapisać !</strong> 

## krok2.

edycja pliku etc/bind/named.conf.options

<img width="682" height="405" alt="image" src="https://github.com/user-attachments/assets/d3caa2a2-2cfb-437d-9400-6d6a5f82f280" />


wpisujemy w tym pliku adres IP jakiegoś serwera DNS. ( jakiegokolwiek, który jest wystawiony w necie np. 8.8.8.8 lub 1.1.1.1 lub 8.8.4.4)

## krok3.

edycja pliku /etc/bind/named.conf.local 

<img width="973" height="302" alt="image" src="https://github.com/user-attachments/assets/77b93a7d-ec2a-4837-b4ba-d68a8bfad814" />

## krok4. 

Edycja strefy przeszukiwania do Przodu

sudo nano /etc/bind/db.local

W tym pliku po każdej jego edycji zmieniamy numer seryjny (Serial) pliku o 1. DOKONUJEMY TEGO ZAWSZE PO KAŻDORAZOWEJ ZMIANIE TEGO PLIKU. Jest to istotne, gdyż wtedy informujemy serwer DNS, że strefa uległa zmianie. 

Znak @ oznacza serwer.

Rekordy to są poszczególne wpisy w strefie, które mapują odpowiednie informacje. Typów rekordów jest wiele jednak takimi najpopularniejszymi są:
- A - mapuje nazwę domenową na adres IP
- NS - informuje o serwerach DNS
- CNAME - mapuje nazwę domenową na nazwę domenową
- MX - informuje o serwerze poczty
- AAAA - mapuje nazwę domenową na adres IPv6
- TXT - przechowuje czysty tekst. Używany przez chociażby przez Google do autoryzacji właściciela

<img width="1130" height="333" alt="image" src="https://github.com/user-attachments/assets/3323e3e8-dc94-490b-ae1b-2de734ab6bae" />


## krok5. 

Edycja strefy przeszukiwania do Tyłu ):

sudo nano /etc/bind/db.127

W tym pliku ( podobnie jak w poprzednim ) po każdej jego edycji zmieniamy numer seryjny (Serial) pliku o 1. DOKONUJEMY TEGO ZAWSZE PO KAŻDORAZOWEJ ZMIANIE TEGO PLIKU. Jest to istotne, gdyż wtedy informujemy serwer DNS, że strefa uległa zmianie. 

Znak @ oznacza serwer.

Rekordy są powyżej (:

<img width="1116" height="295" alt="image" src="https://github.com/user-attachments/assets/be64dc4f-908d-4590-80ac-fb937e785f37" />

## krok6.

Ustawienie obecnego servera DNS jako domyślnego servera DNS dla Klienta i  Servera. 

Edytujemy /etc/resolv.conf na serverze:

<img width="816" height="406" alt="image" src="https://github.com/user-attachments/assets/4c0d798f-4025-43a0-87b9-aca5850af3eb" />

Edytujemy /etc/resolv.conf na Kliencie:

<img width="1042" height="922" alt="image" src="https://github.com/user-attachments/assets/e003b757-3b18-4826-bedb-b111295d1f0e" />


## krok7.

Diagnostyka !

<img width="689" height="150" alt="image" src="https://github.com/user-attachments/assets/1c9ff101-d1a4-4bff-b9e9-2009f007159a" />

Te komendy sprawdzą po kolei czy:
- Skonfigurowaliśmy dobrze plik, który określa śćieżki do stref wyszukiwania
- plik z rekordami dotyczącymi strefy wyszukiwania do przodu
- plik z rekoradmi dotyczącymi strefy wyszukiwania do tyłu


Jeśli nie żadnych błędów jak powyżej można następnie wykonać komendy

```
sudo systemctl restart bind9
sudo systemctl start bind9
sudo systemctl status bind9
```


należy także sprawdzić czy netplan jest dobrze skonfigurowany

<img width="325" height="491" alt="image" src="https://github.com/user-attachments/assets/aeadbe92-559a-40a0-aa21-7ca55264fbf3" />


Następnie należy sprawdzić komendą nslookup na kliencie czy wszystkie rzeczy napewno się dobrze resolvują

<img width="591" height="468" alt="image" src="https://github.com/user-attachments/assets/0a24fe03-3072-487c-97b8-aa34dbd9d3e7" />

<img width="718" height="519" alt="image" src="https://github.com/user-attachments/assets/111bfe44-20c1-49a3-a11a-c5dbb2f43d2c" />

# Apache2

Apache jest generalnie najłatwięjszą usługą na egzaminie a więc nie musimy się go obawiać.

plliki, które są nam potrzebne

```
/var/www/html/index.html      -      defaultowe miejsce gdzie przesiaduje stronka
/etc/apache2                  -      tutaj znajdują się wszystkie pliki konfiguracyjne stronki
/etc/apache2/sites-available/000-default-conf   -  tutaj zmieniamy port / miejsce w, którym jest stronka ( na serverze )
/etc/apache2/ports.conf                         -  tutaj zmieniamy port na, którym znajduję się stronka
/etc/apache2/apache2.conf                       -  tutaj zmieniamy miejsce w, którym jest stronka ( na serverze )
/etc/apache2/mods-available/dir.conf            -  tutaj dodajemy dopuszczalne nazwy dla stronki

```

Komendy, które są nam potrzebne

```
sudo apt install apache2 -y      -    Instalacja

sudo systemctl restart apache2           
sudo systemctl status apache2
sudo systemctl start apache2

--- Diagnostyczne ---  ( niepotrzebne )

sudo apache2 -version
sudo apache2 app list
sudo ufw app info 'Apache Full'
```

Bez zastanowienia przechodzimy do konfiguracji ponieważ wiemy, że defaultowo po instalcji dostaniemy tą piekną stronkę defaultową

<img width="805" height="603" alt="image" src="https://github.com/user-attachments/assets/fedfcdc9-88e6-472a-811e-bdff50546bd0" />

## Krok1. - Modyfikacja portu na, którym jest stronka 

Edytujemy plik /etc/apache2/ports.conf

<img width="470" height="215" alt="image" src="https://github.com/user-attachments/assets/413b9d79-16f9-451e-ac06-b15a7127b7b8" />

<img width="735" height="239" alt="image" src="https://github.com/user-attachments/assets/b2951390-3a08-4913-801f-ddce848416f6" />

Zmieniliśmy Port w pierwszymn pliku na '6767' ( losowa liczba )

Edytujemy plik /etc/apache2/

<img width="761" height="489" alt="image" src="https://github.com/user-attachments/assets/ef3a929e-3396-4bfa-8e26-e1c55f0fc964" />

Zmieniliśmy Port w drugim pliku na '6767'

Restartujemy usługe i widzimy ,że strona jest teraz pod portem 6767

<img width="667" height="24" alt="image" src="https://github.com/user-attachments/assets/983bd66c-1c0d-4ce1-8003-ef4034c81e40" />

<img width="800" height="606" alt="image" src="https://github.com/user-attachments/assets/fa4be42a-6650-48e6-aade-30174051cb0e" />

## Krok2. - Modyfikacja Pliku w, którym znajduję się strona oraz jego nazwy.

Tworzmy folder 'harry' w katalogu / komendą 'sudo mkdir /harry'

<img width="561" height="505" alt="image" src="https://github.com/user-attachments/assets/6978bc37-7224-46a5-8ae7-1bebb6888281" />

Edytujemy plik /etc/apache2/sites-available/000-default.conf i zmieniamy DocumentRoot na /harry

<img width="661" height="495" alt="image" src="https://github.com/user-attachments/assets/2891040b-8ef6-43c5-8dfb-3fb49facb64d" />

Edytujemy plik /etc/apache2/apache2.conf i zmieniamy directory na 'harry'

<img width="664" height="461" alt="image" src="https://github.com/user-attachments/assets/c3662b64-0d94-434e-b35f-b4e795b7085d" />

Edytujemy plik /etc/apache2/mods-available/dir.conf i dodajemy w nim 'index_harrego.html'

<img width="940" height="101" alt="image" src="https://github.com/user-attachments/assets/8af930a9-ce96-4f30-8bc3-b84a04172a7b" />

Na końcu przenosimy plik z /var/www/html o nazwie index.html do pliku /harry i zmieniamy jego nazwę na index_harrego.html ( z sudo )

<img width="764" height="121" alt="image" src="https://github.com/user-attachments/assets/238ba242-85c1-499d-8d04-32a51d3390e7" />

Następnie restartujemy usługę i stronka będzie działać !

<img width="795" height="596" alt="image" src="https://github.com/user-attachments/assets/169cb083-91ca-4aec-873c-dfb134baa2a7" />

Na końcu można jeszcze sobie zedytować naszą stronkę jak chcemy bo wkońcu jest to plik .html

<img width="832" height="265" alt="image" src="https://github.com/user-attachments/assets/140d1e6b-4dfe-4cce-aaef-0c6edc96190c" />

<img width="731" height="269" alt="image" src="https://github.com/user-attachments/assets/0f5a725c-a7cd-4bf7-ab6b-1c34aec3f7fd" />


# Samba

# FTP 

Komendy, które będą nam potrzebne
```
sudo apt install vsftpd -y
sudo systemctl restart vsftpd
sudo systemctl status vsftpd
sudo systemctl start vsftpd


```
Pliki, które będą nam potrzebne
```
/etc/vsftpd.conf   -    główna konfiguracja servera FTP
```

## Zapoznanie się z ustawieniami

Naszym celem będzie:
- Możliwość zalogowania się przez użytkownika anonimowego
- Możliwość zalogowania się użytkownika systemowego
- Sprawienie, że użytkownicy mogą tylko być w swoich katalogach domowych
- stowrzenie banera 
- Dodatkowe ustawienia..

## Najbardziej podstawowa konfiguracja servera FTP ( tylko odkomentowuwyjemy )

po otwarciu pliku vsftpd.conf pierwsza aby stworzyc podstawową konfigurację 
- Zmienieniamy anonymous_enable=NO na anonymous_enable=YES
Odkomentowuwyjemy
- #write_enable=YES
- anon_upload_enable=YES
- anon_mkdir_write_enable=YES

aby te zmiany miały jakikolwiek sens należy teraz stworzyć katalog dla użytkownika anonimowego aby mógł pobierać i wysyłać pliki (:.

```
cd /srv
sudo mkdir -p /srv/ftp/public_folder_for_anonymous
sudo chown -R ftp:ftp  /srv/ftp/public_folder_for_anonymous
sudo chmod -R 775 /srv/ftp
```

W tej konfiguracji przedstawionej na górze użytkownik anonimowy po zalogowaniu się zobaczy folder 'public_folder_for_anonymous' po wejściu do niego będzie w stanie pobierać i zapisywać pliki.

dlatego, że użytkownik ftp działa jak użytkownik anonymous to kiedy użytkownik anonymous wcieli się w role użytkownika ftp to według uprawnień które ustawiliśmy plikowi public_folder_for_anonymous ( 775 ) według nich grupa,użytkownik ma pełne uprawnienia do pliku. a przez to, nasz folder ma takie uprawnienia jakie ma to skoro uzytkownik anonymous = użytkownik ftp będziemy mogli teraz i zapisywac i odczytywac i wykonywać ALE tylko w tym folderze 

<img width="465" height="403" alt="image" src="https://github.com/user-attachments/assets/b31681ab-edc6-4ee3-8c6e-274dfa11e785" />

<img width="629" height="767" alt="image" src="https://github.com/user-attachments/assets/80c40a13-fa14-47c4-8a77-64c91c2fb2e0" />

Następnie Odkomentowuwyjemy
- ftpd_banner= ( wpisujemy cokolwiek )
- chroot_local_user=YES
- chroot_list_enable=YES
- chroot_list_file=/etc/vsftpd.chroot_list
UWAGA: Dopisujemy allow_writeable_chroot=YES aby nie dostać tego błędu:

Następnie należy utworzyć plik vsftpd.chroot_list komendą

sudo touch /etc/vsftpd.chroot_list

Następnie należy go zedytować i dopisać naszego użytkownika. w moim przypadku użytkownik to 'highsec'.

sudo nano /etc/vsftpd.chroot_list    -    dopisujemy naszego użytkownika.

przez to, że dopisaliśmy użytkownika highsec do tego pliku będzie on mógł po zalogowaniu na niego wyjść z opisanego dla niego katalogu.

Gdyby teraz wejść na server FTP i zalogowac się np. z uzytkownika harry123 z hasłem harry1234 to ten użytkownik nie mógł by przejść 'w tył' i utknołby swoim katalogu domowym i tam mógłby wykonywać jakieś operację.

<img width="679" height="31" alt="image" src="https://github.com/user-attachments/assets/57103218-9cac-414d-9416-de6831e32ba2" />

<img width="687" height="759" alt="image" src="https://github.com/user-attachments/assets/91902655-c571-4d51-852e-9e34fd1f8239" />


Na końcu resetujemy nasz server FTP

sudo systemctl restart vsftpd
sudo systemctl status vsftpd

<img width="798" height="229" alt="image" src="https://github.com/user-attachments/assets/3cc2a7a2-62ec-473a-ac23-1c78bc641f8e" />

testujemy działanie Servera na kliencie poprzez komendę 'ftp' ( można oczywiście też przez GUI co jest wytłumaczone w sekcji 'Ubuntu_Klient' )

wpisujemy komendę 
```
ftp 192.168.10.1   
użytkownik: highsec
hasło: ( hasło użytkownika highsec ) 
```
możemy robić teraz wszystko.
```
ftp 192.168.10.1
użytkownik: anonymous 
hasło: ( BRAK - klikamy enter )
```
cd Public_folder_for_anonymous

możemy teraz robić wszystko ale TYLKO w tym folderze.

## Komenda FTP.
```
ftp 192.168.10.1 – Łączy się z serwerem. ( Podajesz użytkownika i hasło )

dir/ls – Pokazuje pliki na serwerze w obecnym katalogu.

pwd – Pokazuje, w jakim folderze jesteś na serwerze.

cd folder – Wchodzi do folderu na serwerze.

cd .. – Wraca folder wyżej na serwerze.

lcd /home/user – Zmienia folder na Twoim komputerze z którego pobieramy pliki.

mkdir Folder_Harrego – Tworzy nowy folder na serwerze.

put harry.txt – Wysyła plik z Twojego PC na serwer.

get harrongo.txt – Pobiera plik z serwera na Twój PC.

delete plik.txt – Usuwa plik z serwera.

bye (lub quit / exit) – Rozłącza i zamyka FTP.
```




## Dodatkowe ustawienia.

oprócz tego co już mamy możemy zrobić jeszcze więcej!

Dodatkowe ustawienia

```
anon_root=/srv/ftp/public_folder_for_anonymous - sprawi, że po zalogowaniu się z użytkownika anonymous odrazu przejdziemy do tego folderu, gdzie możemy robić co chcemy.
hide_ids=YES - ta opcja jest po to, aby nie było widać właścicieli danego zasobu na serwerze;

userlist_enable=YES - ta opcja mówi serwerowi, że uruchomiona jest lista użytkowników;
userlist_file=/etc/vsftpd.user_list - ta opcja ustawia lokalizację tej listy;
userlist_deny=NO - ta opcja natomiast mówi serwerowi, że ta lista zawiera użytkowników, którzy MOGĄ wejść na serwer, a nie tych którzy nie mogą. Gdybyśmy to ustawili na YES to ta lista byłaby to klasyczna blacklist. W naszym przypadku jest to whitelist;
```

Przykładowa edycja tej listy:

<img width="470" height="110" alt="image" src="https://github.com/user-attachments/assets/4f0e5549-3391-4632-b114-bbb258e87edf" />

Nie będziemy wchodzić w uprawnienia dla danych użytkowinków w innych folderach. To co tutaj jest wyczerpało i tak server FTP. Server FTP nie pojawił się jeszcze nigdy na egzaminie INF02 ale jeśki się pojawi to napewno będzie zawierał uproszczoną powyższą konfigurację i np. zamiast 3 rzeczy będzie trzeba zrobić jedną 












# Server SSH

sudo apt install openssh-server       - Instaluje usługe

sudo systemctl status ssh             - Sprawdza status usługi

sudo systemctl start ssh              - Sprawia, że usługa włącza się po restarcie kompa

ssh highsec@192.168.10.10 -p 22       - Komenda służąca do połączenia się do servera wystawiającego uśługę SSH      highsec - użytkownik na serverze   @      192.168.10.10 - adres IP servera   -p 22    -  port na, którym jest server ( niewymagane ) 






















