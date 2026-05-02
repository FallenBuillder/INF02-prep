<img width="622" height="109" alt="image" src="https://github.com/user-attachments/assets/5d0cf2f2-d85e-49f6-8360-c429f8886998" />W każdym egzaminie praktycznym pojawia się konfiguracja switcha , czasami jest łatwa bo wystarczy zrobić jedną rzecz i można iść dalej a czasami może się zdażyć że spotkamy się z nieco trudniejszym zadaniem typu np. stworzenie trunka , naszczęście switch jest jedną z najprostszych rzeczy na egzaminie a więc nauczenie się dosłownie paru zagadnień może dać nam łatwe punkty


ta sekcja jest podzielona na dwie części GUI, CLI - Naszczęście na egzaminie mamy wybór przezc co chcemy konfigurować naszego switcha dlatego radzę zawsze robić przez GUI żeby sobie nie pokomplikować ale można też przez CLI jeśli się czuje pewnym 

część GUI ,CLI zawiera następujące zagadnienia
- Konfiguracja adresu IP, maski podsieci, bramy domyślnej
- Konfiguracja VLANów (tworzenie, nadawanie ID, ustawianie tagowania, przypisywanie portów)
- wyłączenie portu na switchu
- Konfiguracja trunków ( tutaj egzamin2023-Styczeń-zad.03,04 , egzamin2023-Czerwiec-zad.-02 , egzamin2024-czerwiec-zad.01)
- przypisanie ostatniego możliwego adresu z podsieci ( Mikrotik_Konfiguracja )
- ( dodać rzeczy z 2026 zima )



### GUI  - Jak połączyć się z switchem 
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

## Konfiguracja adresu IP, maski podsieci, bramy domyślnej 

Konfiguracja adresu IP , maski podsieci , bramy domyślnej jest najprostszą rzeczą do zrobienia jeśli chodzi o switcha i dużą część egzaminów posiada tylko do zrobienia właśnie to.
Żeby zmienić adres IP switcha wystarczy przejść do zakładki System -> System Info 
<img width="170" height="40" alt="image" src="https://github.com/user-attachments/assets/4a6ecd1c-301c-44e5-a2f3-8f65047ab79d" />
Następnie należy przejść do zakłądki System IP 
<img width="662" height="308" alt="image" src="https://github.com/user-attachments/assets/4c4323e5-5715-48e2-bd98-ffdfe842b927" />
i na przykładzie egzaminu INF.02 : 2024 - czerwiec - zad. 04 możemy teraz skonfigurować tego switcha
<img width="622" height="109" alt="image" src="https://github.com/user-attachments/assets/ca4bdd99-6817-43d6-bd30-b68144c4e1af" />
Nastepnie aby zmienić Adres IP , Maske , Brame domyślną wystarczy wpisać podanę nam w egzaminie wartości do korespondujących do nich komórek czyli tych:
<img width="374" height="76" alt="image" src="https://github.com/user-attachments/assets/3709f927-9ae3-4df5-92ac-6e4679bc5ba8" />
Zakładając teraz ,że adresem bramy domyślnej routera jest 192.168.10.1 wpisujemy dane:

Maska /28 w zapisie binarym to porostu napisanie jedynek w czterach oktetach od lewej strony. - czyli maska /28 to:
11111111 11111111 11111111 11110000
Następnie tą maske trzeba przekonwertować na wartość dziesiętną czyli dodajemy do siebie wartości potęgi dwójki w przy każdej jedynce w każdym oktecie co nam da:

255.255.255.(128+64+32+16)
255.255.255.240

Dokładne obliczanie adresów siecowych , rozgłoszeniowych , podsieci , masek itd jest zrobiony w pliku 'Materiały' w Folderze 'Mikrotik_Konfiguracja'
<img width="405" height="638" alt="image" src="https://github.com/user-attachments/assets/0b426e5e-e27c-43ed-8dba-390b1597e1d6" />

Finalny Wynik powinien wyglądać tak:
<img width="659" height="307" alt="image" src="https://github.com/user-attachments/assets/794292f6-c6c2-4f44-ae2b-689b16236e8e" />

Nie mozna oczywiście zapomniąć żeby na końcu zawszę kliknąć guzik który pozwoli nam zapisać naszę zmiany - w tym przypadku Apply 
<img width="64" height="26" alt="image" src="https://github.com/user-attachments/assets/3d56dddd-f6eb-49ff-bedd-ff552a939fe2" />


## Konfiguracja VLANów (tworzenie, nadawanie ID, ustawianie tagowania, przypisywanie portów)





























### CLI - Jak połączyć się z switchem 

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

Po wejściu do programu pojawi się następujące Menu

<img width="444" height="435" alt="image" src="https://github.com/user-attachments/assets/9f76322c-052f-4e52-b281-a28002e8c1bd" />

W tym Menu należy wybrać zakładke Serial a następnie wpisać port COM który jest podłączony do naszego switcha , szybkość z którą będzie przesyłany sygnał.
- Wpisujemy port COM który znaleźliśmy w poprzednim kroku do zakładki Serial line
- Wpisujemy szybkość którą można znaleść w Dokumentacji danego Switcha która będzie na dysku USB na egzaminie.
Przykład Znalezienia Szybkości w dokumentacji:
<img width="792" height="1127" alt="image" src="https://github.com/user-attachments/assets/03fbcef6-eb4d-43a9-8082-7ef5961b15a4" />
Po wejściu do dokumentacji należy znaleść temat który brzmi w stylu jak "Accessing the CLI" albo "Connecting to the switch"
<img width="710" height="100" alt="image" src="https://github.com/user-attachments/assets/f7e59f1a-5919-43f5-8823-67d5dc3123f4" />
Jak widać istnieje taki dział - a więc idziemy do niego w dokumentacji 
<img width="670" height="964" alt="image" src="https://github.com/user-attachments/assets/46e4e0f5-e5cc-474a-993f-4243c13ed5fa" />
Jak widać na jednej z pierwszych stron dokumentacji Switcha - Dotyczącej CLI widnieje napis Baud rate 38400 bps
<img width="588" height="96" alt="image" src="https://github.com/user-attachments/assets/2ce9f4f2-dc47-411d-a3bd-960ef3e88c24" />
Oznacza to ,że szybkość którą musimy wpisać to analogicznie 38400

czyli finalne ustawienia PuTTY wyglądałby następująco:
<img width="444" height="439" alt="image" src="https://github.com/user-attachments/assets/98f7c97f-0efd-46e7-9d74-73dfc6652395" />

Na koniec należy kliknąć przycisk Open - co sprawi ,że połączymy się do switcha 
<img width="85" height="33" alt="image" src="https://github.com/user-attachments/assets/bdd37006-db80-4f13-b5c1-6a4a12bc941d" />

<img width="662" height="420" alt="image" src="https://github.com/user-attachments/assets/5b16f206-3392-41b0-a2f4-eed30f10d988" />
Kiedy pojawi się nowe okienko - wystarczy kliknąć guzik Enter i widzimi ,że możemy teraz wpisywać komendy 


## Troubleshooting


<img width="385" height="166" alt="image" src="https://github.com/user-attachments/assets/1f17e8ba-4562-402e-9086-39e7c8a30e66" />

Jeśli dostaniemy taki błąd oznacza to ,że port COM który wybraliśmy jest nie poprawny i nie die się nim połączyć do Switcha aby naprawić ten błąd należy połączyć się urzywając dobrego portu COM podłączonego do interfejsu Consolowego Switcha , do portu Serial komputera 

<img width="666" height="414" alt="image" src="https://github.com/user-attachments/assets/f9697636-13b8-45a5-aef3-4959c50aea58" />

Jeśli po podłączeniu się do switcha , kliknięciu Enter dostajemy za każdym razem takie artyfakty - oznacza to ,że szybkość przez nas wpisana jest niepoprawna i należy ją zmienić.













# CLI - Konfiguracja Switcha









	
