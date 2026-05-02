<img width="269" height="21" alt="image" src="https://github.com/user-attachments/assets/df0cad84-4b31-4a92-8805-fe56c3632f16" />W każdym egzaminie praktycznym pojawia się konfiguracja switcha , czasami jest łatwa bo wystarczy zrobić jedną rzecz i można iść dalej a czasami może się zdażyć że spotkamy się z nieco trudniejszym zadaniem typu np. stworzenie trunka , naszczęście switch jest jedną z najprostszych rzeczy na egzaminie a więc nauczenie się dosłownie paru zagadnień może dać nam łatwe punkty


ta sekcja jest podzielona na dwie części GUI, CLI - Naszczęście na egzaminie mamy wybór przezc co chcemy konfigurować naszego switcha dlatego radzę zawsze robić przez GUI żeby sobie nie pokomplikować ale można też przez CLI jeśli się czuje pewnym 

część GUI ,CLI zawiera następujące zagadnienia
- Konfiguracja adresu IP, maski podsieci, bramy domyślnej
- Konfiguracja VLANów (tworzenie, nadawanie ID, ustawianie tagowania, przypisywanie portów)
- wyłączenie portu na switchu
- Konfiguracja trunków ( tutaj egzamin2023-Styczeń-zad.03,04 , egzamin2023-Czerwiec-zad.-02 , egzamin2024-czerwiec-zad.01)
- włączenie 802.1q
- włączenie trybu access
- przypisanie ostatniego możliwego adresu z podsieci
- ( dodać rzeczy z 2026 zima )

### GUI  
w przypadku połączenia się do switcha przez GUI ( Graphical User Interface ) chcemy abyśmy byli switchem w tej samej podsieci abyśmy mogli z nim rozmawiać.
oznacza to ,że nasz adres IP na karcie sieciowej która jest podłączona .do jednego z interfejsów switcha ( zazwyczaj najlepiej przy konfiguracji podłaczać się do pierwszego portu ponieważ wiemy wtedy ,że się połączymy a podłączenie urządzeń jest i tak najczęściej w dalszych etapach egzaminu ) 
czy to jesteśmy na Windowsie czy na Linuxie , adres IP trzbea zmienić 
wszystkie switche na egzaminie powinny mieć adres IP 192.168.0.1/24 - oznacza to ,że abyśmy byli w tej samej podsieci musimy nasz adres IP zmienić na np, 192.168.0.19/24 ( ostatnia liczba nie ma zabardzo znaczenia wystarczy poprostu ,że ostatni oktet nie jest taki sam jak u switcha - czyli poprostu nie mogą mieć takich samych adresów IP ) 

krok 1. 

Zmiana adresu IP w windowsie 

aby zmienić adres IP na windowsie wystarczy kliknąć przycisk start ( ikonka windowsa ) a następnie wpisać 'sieciowe' i powinno wyskoczyć okienko 'Wyświetl połączenia sieciowe' po kliknięciu w to okienko pojawia się nam takie okienko:
<img width="1120" height="297" alt="image" src="https://github.com/user-attachments/assets/5be86496-d09c-4294-be3f-6a8f02298d68" />
> na egzaminie powinny zawsze być tylko dwie karty sieciowe
- następnie możemy sobie podłączyć lub odłączyć przewód ethernet aby zobaczyć ikonke pod kartą.
- jeśli przy jakiejś karcie pojawi się X lub przestanie się pokazywać to oznacza ,że będziemy konfigurować włąśnie tą kartę
<img width="355" height="440" alt="image" src="https://github.com/user-attachments/assets/c898cf38-b303-4e33-88a5-cac498e58a04" />
po kliknięciu na karte pojawia się nam menu w którym klikamy właściwości
<img width="358" height="462" alt="image" src="https://github.com/user-attachments/assets/9dec03b1-a02a-4a7a-8b74-a51a6a096dcf" />
następnie w tym okienku scrollujemy na dół
<img width="246" height="20" alt="image" src="https://github.com/user-attachments/assets/924bed37-f099-460c-bf16-dfdc80485d4d" />
klikamy dwa razy tą opcje
<img width="390" height="451" alt="image" src="https://github.com/user-attachments/assets/820e8684-3f48-4b79-8f9a-c8d33a18a952" />
i możemy skonfigurować nasz adres IP czyli:
- zmieniamy sekcje Adres IP: na jakiś z podsieci w której jest fabrycznie nasz switch , w masce podsieci wpisujemy maske /24 ( taka jest defaultowo ) czyli: 255.255.255.0
Po zakończeniu klikamy wszędzie przycisk ok aby opcje się zapisał i wychodzimi z połączeń sieciowych

Zmiana adresu IP w linuxie 

krok 2.

- należy podłaczyć się do pierwszego portu w switchu

krok 3.

- Należy wejść do przeglądarki i wpisać adres IP naszego switcha - czyli jeśli łączymy się na egzaminie do niego po raz pierwszy w przeglądarce wpisujemy '192.168.0.1'
<img width="1246" height="25" alt="image" src="https://github.com/user-attachments/assets/1615345a-6dad-4b7f-a0cc-7a7bde4180fa" />

krok 4.

- Powinniśmy teraz dostać monit o zalogowanie się na switchach na egzaminie jeśli hasło nie ani użytkownik nie są wcześniej podane wpisujemy poprostu
User Name: admin
Password: admin

<img width="379" height="176" alt="image" src="https://github.com/user-attachments/assets/2045b45d-be78-43a5-8d78-6a93ff7bd00f" />
i na koniec klikamy guzik login

<img width="1434" height="930" alt="image" src="https://github.com/user-attachments/assets/5200f861-d658-440e-a269-d4c4385c3295" />
Jak widać połączyliśmy się do switcha 




### CLI 
	
