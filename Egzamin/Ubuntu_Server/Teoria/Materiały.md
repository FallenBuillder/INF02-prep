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

Pierwszym krokiem otwarcie go w edytorze tekstowym takim jak vim lub nano - dla przykładu użyjemy nano 

<strong>UWAGA: Formatowanie w pliku 50-cloud-init.yaml jest bardzo wybredne i każda spacja się liczy</strong>


Komendy potrzebne do konfiguracji Sieci.
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

# krok2.

edycja pliku etc/bind/named.conf.options

<img width="820" height="413" alt="image" src="https://github.com/user-attachments/assets/9143d93e-e123-420b-ad70-37f84a41a54d" />

# krok3.

edycja pliku /etc/bind/named.conf.local 

<img width="822" height="382" alt="image" src="https://github.com/user-attachments/assets/7de1dd1d-7090-40b3-8b0c-8481de2804a7" />


















