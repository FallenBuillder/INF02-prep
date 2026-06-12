<img width="886" height="632" alt="image" src="https://github.com/user-attachments/assets/795daea9-fb64-47d7-8eff-12db2d762ef0" />

<img width="937" height="625" alt="image" src="https://github.com/user-attachments/assets/9ce0d8fe-eff2-46c0-8888-5d37c8dab329" />

### Nie ma zdjęcia 3 strony 

Zad 1 wsadź dysk twardy do komputera

Zad 2 skonfiguruje ruter

Zad 3 skonfiguruje switcha

Zad 4 wykonaj okablowanie (połącz ruter do windows serwera, z drugiej karty sieciowej serwera połącz do switcha, że switcha do drukarki, i że switcha do stacji roboczej Linux/windows 10

Zad 5 na Linuxie sprawdź parametry monitora, wersję i nazwę dystrybucji, procesora, RAM, maksymalna rozdzielczość monitora.

Zad 6 skonfiguruj połączenie przewodowe stacji roboczej windows

Zad 7 skonfiguruj połączenie przewodowe serwera windows

Zad 8 test komunikacji serwera ze swtichem, ruterem, stacją roboczą 

Zad 9 kosztorys, trzeba dać rabat 10% na kwotę powyżej 2000zl

Drukarka drukujemy tylko stronę testową co się robi podczas dodawania jej, najlepiej dodać poprzez IP.

Ruter chyba końcowo miał IP 192.168.16.1

Switch 192.168.0.32

Stacja robocza 192.168.0.33

Serwer 192.168.0.X i na drugiej 192.168.16.12








Router

adres IP interfejsu LAN: 192.168.16.1/24

serwer DHCP:

włączony

zakres adresów: 192.168.16.12 192.168.16.20

zarezerwowany adres IP 192.168.16.12 dla interfejsu LANZ serwera.

Przełącznik

utworzone nowe sieci VLAN 802.1Q o ID = 2 oraz ID = 4

porty 1, 2 i 3 przypisane do sieci VLAN o ID = 2 bez tagowania (w trybie dostępu)

port 4 przypisany do sieci VLAN o ID = 4 bez tagowania (w trybie dostępu)

adres IP przełącznika: 192.168.0.32/24 (dla przełącznika L3 adres IP przypisany do VLAN o ID = 2)

brama domyślna: 192.168.0.X, gdzie X oznacza numer stanowiska

Windows server - drukarka przez panel sterowania i ping 

Windows - przydzialy dyskowe

Linux - diagnostyka

Kabel / Keystone / Patchpanel - brak
