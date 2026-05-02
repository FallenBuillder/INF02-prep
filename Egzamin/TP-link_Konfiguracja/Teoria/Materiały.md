<img width="621" height="625" alt="image" src="https://github.com/user-attachments/assets/70dd69c1-eb74-4005-a30b-de75c16c86fe" />W każdym egzaminie praktycznym pojawia się konfiguracja switcha , czasami jest łatwa bo wystarczy zrobić jedną rzecz i można iść dalej a czasami może się zdażyć że spotkamy się z nieco trudniejszym zadaniem typu np. stworzenie trunka , naszczęście switch jest jedną z najprostszych rzeczy na egzaminie a więc nauczenie się dosłownie paru zagadnień może dać nam łatwe punkty


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



### GUI  - Jak się połączyć z switchem 
w przypadku połączenia się do switcha przez GUI ( Graphical User Interface ) chcemy abyśmy byli switchem w tej samej podsieci abyśmy mogli z nim rozmawiać.
oznacza to ,że nasz adres IP na karcie sieciowej która jest podłączona .do jednego z interfejsów switcha ( zazwyczaj najlepiej przy konfiguracji podłaczać się do pierwszego portu ponieważ wiemy wtedy ,że się połączymy a podłączenie urządzeń jest i tak najczęściej w dalszych etapach egzaminu ) 
czy to jesteśmy na Windowsie czy na Linuxie , adres IP trzbea zmienić 
wszystkie switche na egzaminie powinny mieć adres IP 192.168.0.1/24 - oznacza to ,że abyśmy byli w tej samej podsieci musimy nasz adres IP zmienić na np, 192.168.0.19/24 ( ostatnia liczba nie ma zabardzo znaczenia wystarczy poprostu ,że ostatni oktet nie jest taki sam jak u switcha - czyli poprostu nie mogą mieć takich samych adresów IP ) 

## krok 1. 

### Zmiana adresu IP w windowsie 

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



### Zmiana adresu IP w linuxie 


Jest mała szansa ,że na egzaminie dostaniemy i linux server, linux client wtedy najlepiej skonfigurować switcha przez GUI. 
Jeśli chodzi o linuxa to wszystkie kroki są dokładnie takie same z wyjątkiem zmiany adresu IP na kliencie
analogicznie jak w przypadku Windosa będziemy chcieli zrobić to samo. Czyli zmienić nasz adres IP na 192.168.0.X/24 ( gdzie X to dowolna liczba oprócz tej która jest przypisana do switcha i nie jest adresem sieci ani rozgłoszeniowym a /24 to maska o wartości 255.255.255.0 


<img width="405" height="275" alt="image" src="https://github.com/user-attachments/assets/69671c07-fa5c-4a6a-94b1-51c4553c00f5" />
Na początku lokalizujemy ikonki w prawym górnym rogu ekranu i klikamy na nie 

<img width="61" height="48" alt="image" src="https://github.com/user-attachments/assets/faec98ed-ecfd-4077-83e2-8530f14dd414" />
Następnie klikamy w ustawienia

<img width="989" height="652" alt="image" src="https://github.com/user-attachments/assets/2ba05665-1800-46eb-b509-45e7b174aa37" />
Następnie ponownie klikamy w guzik z ustawieniami w prawym górnym rogu ( w zakłądce wired ten na górze )

<img width="755" height="589" alt="image" src="https://github.com/user-attachments/assets/42061ffb-7372-4378-a276-a7900358fae8" />
Następnie w nowym okienku wchodzimy do zakładki IPv4

<img width="661" height="107" alt="image" src="https://github.com/user-attachments/assets/4e0720c4-7a5a-47e3-8ba6-a94d16e7a342" />
klikamy opcje Manual

<img width="717" height="99" alt="image" src="https://github.com/user-attachments/assets/a424bec3-adf3-4e7a-a8af-7eee2c51f4b0" />
Następnie wpisujemy tutaj nasz adres IP , maske podsieci 

<img width="717" height="123" alt="image" src="https://github.com/user-attachments/assets/ac931750-4933-4048-ac7c-db7ab1ce7092" />
<img width="91" height="43" alt="image" src="https://github.com/user-attachments/assets/6acc1523-61a8-4597-a086-c8701878139a" />
Na koniec kliamy guzik apply w prawym górnym rogu i adresacja się zapiszę 

















## krok 2.

- należy podłaczyć się do pierwszego portu w naszym switchu ( powinno się jeszcze sprawdzić czy napewno podłączamy się dobrą kartą sieciową )

## krok 3.

- Następnie należy wejść do przeglądarki naszego wyboru i wpisać adres IP naszego switcha - oznacza to ,że jeśli łączymy się na egzaminie do niego po raz pierwszy to w przeglądarce wpisujemy '192.168.0.1'
<img width="1246" height="25" alt="image" src="https://github.com/user-attachments/assets/1615345a-6dad-4b7f-a0cc-7a7bde4180fa" />

## krok 4.

- Powinniśmy teraz dostać monit o zalogowanie się na switcha. Na egzaminie jeśli ani hasło ani użytkownik nie są wcześniej podane wpisujemy poprostu
User Name: admin
Password: admin

<img width="379" height="176" alt="image" src="https://github.com/user-attachments/assets/2045b45d-be78-43a5-8d78-6a93ff7bd00f" />
i na koniec klikamy guzik login

<img width="1434" height="930" alt="image" src="https://github.com/user-attachments/assets/5200f861-d658-440e-a269-d4c4385c3295" />
Jak widać połączyliśmy się do switcha 


# GUI - Konfiguracja Switcha 




### CLI - Jak się połączyć z switchem 

Jeśli ktoś ma ochotę skonfigurować switcha przez CLI lub jest napisane tak w arkuszu ( co wątpie no nigdy jeszcze tak nie było ) to trzeba przejśc przez 3 podstawowe kroki.

## krok 1

- Na początek należy zlokalizowac przewód Consolowy który sprawi ,że dzięki niemu będziemy mogli połaczyć się z switchem przez CLI. Wygląda on jak coś w tym stylu.
<img width="621" height="625" alt="image" src="https://github.com/user-attachments/assets/deeba806-70d6-4670-a3b0-7a2b4123b3a1" />
> kolor nie ma znaczenia

kiedy połączamy się przez konsole musimy włączyć przewód Ethernet do specjalnego portu Konsolowego zlokalizowanego na tyle lub na przodzie Switcha - będzie on wyglądać tak: 
<img width="1863" height="522" alt="image" src="https://github.com/user-attachments/assets/f93ef74c-6617-49e7-920d-20ff3f463678" />
<img width="141" height="143" alt="image" src="https://github.com/user-attachments/assets/5bb54c63-f5df-4ad7-ac53-750fb8c33e71" />
Po wpięciu naszego przewodu konsolowego do switcha następnie jego drugi koniec podłączyć do interfejsy Serial naszego komputera. 
<img width="115" height="84" alt="image" src="https://github.com/user-attachments/assets/15851750-e6fa-4858-a803-8e4e3b1ded50" /> 
> jest szansa ,że na egzaminie będzie przejściówka do USB to wtedy z niej skorzystamy , podłączymy się do interfejsy USB w komputerze.

## krok 2

Następnie klikamy   Windows + r   i wpisujemy devmgmt.msc albo wpisujemy w menu start 'Menedżer urządzeń' i do niego wchodzimi 
<img width="472" height="91" alt="image" src="https://github.com/user-attachments/assets/0deeb0b0-10f7-4708-89a9-6e3e93cccefd" />
Po wejsciu do menedżera urządzeń lokalizujemy zakładke 'Porty (COM i LPT)' , ją rozwijamy 

W tej zakładce widać jakie porty COM mamy w naszym komputerze.

na przykładzie pokazanym powyżej jest podłączony Adapter PL2303HXA - który w tym przypadku odpowiada przejściówce z Serial na USB - jeśli na egzaminie będzie jakaś przejściówka oznacza to ,że pewnie pokaże się jakaś wyjątkowa tego typu nazwa.

Jeśli na egzaminie port Serial jest wbudowany w płyte główną oznacza to ,że trzeba albo wypróbować wszystkie opcje albo na logikę zobaczyć ,że tutaj np. port COM3 , COM4 są tylko wirtualnymi portami które używa interfejs bluetooth a COM1 jest portem wbudowanym w płyte a PL2303HXA to adapter. 

Jeśli mamy Adapter to musimy w niego wejść i po kliknięciu na niego 2 razy pojawi się nam do jakiego portu COM należy.

<img width="404" height="451" alt="image" src="https://github.com/user-attachments/assets/8a6923b3-60ea-4187-9d66-df3e705839ce" />


## krok 3

z nowo znalezioną wiedzą możemy teraz przejść do faktycznego połączenia się z Switchem.

Do podłączenia się z switchem przez konsole na egzaminie użyjemy programu PuTTY - który pozwoli nam na 
- Wybranie szybkości
- Wybranie portu COM
- Wybraniu Typu połączenia 

Jeśli na egzaminie porgram Putty nie jest zainstalowany należy podłączyć dysk USB o nazwie PROGRAMY do naszego komputera i znaleść tam a następnie przeciągnąć z niego instalator tego programu i do niego wejść.




# CLI - Konfiguracja Switcha









	
