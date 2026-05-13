# Teoria

W każdym egzaminie praktycznym pojawia się konfiguracja switcha , czasami jest łatwa bo wystarczy zrobić jedną rzecz i można iść dalej a czasami może się zdażyć że spotkamy się z nieco trudniejszym zadaniem typu np. stworzenie trunka , naszczęście switch jest jedną z najprostszych rzeczy na egzaminie a więc nauczenie się dosłownie paru zagadnień może dać nam łatwe punkty


ta sekcja jest podzielona na dwie części GUI, CLI - Naszczęście na egzaminie mamy wybór przezc co chcemy konfigurować naszego switcha dlatego radzę zawsze robić przez GUI żeby sobie nie pokomplikować ale można też przez CLI jeśli się czuje pewnym 

część GUI ,CLI zawiera następujące zagadnienia
- jak się połączyć (GUI , CLI) ?
- Konfiguracja adresu IP, maski podsieci, bramy domyślnej
- Konfiguracja VLANów (tworzenie, nadawanie ID, ustawianie tagowania, przypisywanie portów)
- wyłączenie portu na switchu
- Konfiguracja trunków
- przypisanie ostatniego możliwego adresu z podsieci ( było kiedyś takie zadanie na egzaminie ,że trzeba było jeszcze przypisać Adres IP bazując na obecnej konfiguracji sieciowej i wybrać ostatni adres IP z danej sieci. Więcej o tym w folderze 'Sieci')


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

Dokładne obliczanie adresów siecowych , rozgłoszeniowych , podsieci , masek itd jest zrobiony w pliku 'Materiały' w Folderze 'Sieci'
<img width="405" height="638" alt="image" src="https://github.com/user-attachments/assets/0b426e5e-e27c-43ed-8dba-390b1597e1d6" />

Finalny Wynik powinien wyglądać tak:
<img width="659" height="307" alt="image" src="https://github.com/user-attachments/assets/794292f6-c6c2-4f44-ae2b-689b16236e8e" />

Nie mozna oczywiście zapomniąć żeby na końcu zawszę kliknąć guzik który pozwoli nam zapisać naszę zmiany - w tym przypadku Apply 
<img width="64" height="26" alt="image" src="https://github.com/user-attachments/assets/3d56dddd-f6eb-49ff-bedd-ff552a939fe2" />









## Konfiguracja VLANów (tworzenie, nadawanie ID, ustawianie tagowania, przypisywanie portów)
Skonfigurowanie VLANów przez GUI jest dosyć proste i wszystkie ustawienia które trzeba skonfigurować są dosyć intuicyje a więc nie powinno być z tym jakiegoś większego problemu.

Tym razem z naszego panelu zakładek klikamy VLAN i pokazują nam się następujące opcję 
<img width="170" height="492" alt="image" src="https://github.com/user-attachments/assets/9543cffe-a2e2-4538-b9eb-676e419e57f5" />
klikamy w pierwszą opcje '802.1Q VLAN' - jest to jedyna opcja która nam się tutaj przyda.
<img width="161" height="109" alt="image" src="https://github.com/user-attachments/assets/65d0b159-39f3-473b-b8d1-d88b170d8c9f" />
Od wejścia zakładka wygląda tak
<img width="902" height="222" alt="image" src="https://github.com/user-attachments/assets/3de77f27-8491-439d-9622-3475a552104b" />

po wejściu do tej zakładki możemy zauważyć dwie nowe w których będziemy głównie operować:
- VLAN config ( w tej zakładce będziemy dodawać VLANY , przypisywać im nazwy , id , porty )
- Port Config ( w tej zakładce będziemy zmieniać mode ( tryb ) portów )


Zaczynając od zakładki VLAN config 
<img width="731" height="213" alt="image" src="https://github.com/user-attachments/assets/eb561a2b-3374-4f91-8ffc-f59a50629c30" />

Aby stworzyć nowego VLANa należy kliknąć guzik 'Create'
Następnie wyskoczy nam okienko w którym będziemy dodawać VLAN 
Mogę wytłumaczyć poszczególne opcje które tutaj się znajdują poprzez wykonanie zadania z egzaminu.
<img width="628" height="622" alt="image" src="https://github.com/user-attachments/assets/de6af861-b646-4eca-b278-15b5af36fa14" />
<img width="1805" height="147" alt="image" src="https://github.com/user-attachments/assets/31853aa4-4cc2-4ace-8c2a-82795e151b29" />
Z polecenia wynika ,że mamy skonfigurować VLAN który ma:
- ID = 100
- nazwa = VLAN100
- 3 porty = 1, 2, 3 ( które nie są tagowane )

Oznacza to ,że do pola description dajemy nazwe VLANa , do pola ID dajemy jego ID a następnie wybieramy porty do których ma należeć poprzez wybieranie checkboxów

Konfiguracja tego zadania wyglądałaby Następująco 
<img width="611" height="610" alt="image" src="https://github.com/user-attachments/assets/4a341f7d-e69a-41a6-a93c-345e3f656c42" />
> do tego zadanie nie potrzebowaliśmy tym razem drugiej zakładki ponieważ wszystkie porty są defaultowo nie tagowane

Na koniec klikamy Apply i nasz VLAN jest gotowy.
<img width="64" height="27" alt="image" src="https://github.com/user-attachments/assets/eed2eea7-8283-4d90-b3f6-9610e60a437f" />


### Włączenie tagowania
jeśli na egzaminie jest gdzieś napisane ,że mamy włączyć tagowanie dla VLANu do w takim razie będziemy musieli użyć drugiej karty ' Port Config ' 
<img width="616" height="493" alt="image" src="https://github.com/user-attachments/assets/b4d41215-5ac7-4cbf-8ce7-dacbcce94395" />
W tej karcie możemy zmienić tryb konfiguracji portów na jeden z trzech 
- Trunk ( będzie omówiony zachwilę )
- Access ( to jest defaultowy tryb w każdym VLANie który nie pozwala nam na zmienienie tagowania ) 
- General ( ten tryb pozwoli nam na włączenie tagowania )
<img width="585" height="208" alt="image" src="https://github.com/user-attachments/assets/ba2ab60a-b91a-4835-beed-2afdbe8519c0" />
dla przykładu, gdyby było na egzaminie żeby włączyć tagowanie na portach 1,2,3 
Musimy najpierw wybrać wszystkie porty ,które chcemy skonfigurować a następnie z Dropdowna wybrać Link Type General
<img width="589" height="429" alt="image" src="https://github.com/user-attachments/assets/08a02b9d-bb21-4109-bc43-ae1d89d9d6a1" />
po kliknięciu guzika apply ta opcja sprawi ,że będziemy mogli teraz w pierwszym menu 'VLAN Config' wybrać czy chcemy tagować czy nietagowac porty
<img width="610" height="158" alt="image" src="https://github.com/user-attachments/assets/ebf42dc7-e971-48a0-93d9-44d229d058c9" />
Po kliknięciu na dropdowna i wybraniu, że chcemy tagować podane przez nas porty ustawienie tagowanie jest skończone i możemy kliknąć apply aby zapisać nasze ustawienia.
<img width="62" height="21" alt="image" src="https://github.com/user-attachments/assets/398f0c41-c44a-4874-a61c-345b19771a7f" />
<img width="602" height="395" alt="image" src="https://github.com/user-attachments/assets/fed68e2b-d45f-4fff-bdae-c4c3f1e1c945" />


### przypisanie SVI do danego VLANa
jeśli na egzaminie jest napisane ,że mamy konfigurować switcha tylko przez np. VLAN100 to trzeba wtedy wejść w konfiguracje 'Default VLAN'
<img width="694" height="39" alt="image" src="https://github.com/user-attachments/assets/653418b8-cb35-45a9-963e-934615fa11bc" />
kliknąć przycisk 'Edit' i następnie sprawić ,że wybrane są tylko te porty które należą do VLANa o którym mowa czyli np. wybieramy tutaj wszystkie porty VLANA100 i klikamy Apply 
<img width="629" height="617" alt="image" src="https://github.com/user-attachments/assets/364b2bdc-84cd-460c-8cf9-0c436599475a" />
> Alternatywnie na Switchach typu L3 można jeszcze to zrobić inaczej ( Arkusz 2 zima 2026 ) ale to już trzeba by było sprawdzić samemu  - tam w nawiasie jest napisane '(dla przełącznika L3 adres IP przypisany do VLAN o ID = 2)' lecz jest to trochę dziwne patrząc na fakt ,że nie kojarze żeby ktoś miał na egzaminie switcha L3


## Wyłączenie portu z użytku 
może się na egzaminie pojawić pytanie aby np. wyłączyc pozostałe porty ,których nie używamy, aby to zrobić należy najpierw wejść do zakładki Switching i ją rozwinąć a następnie wybrać opcje 'Port'
<img width="127" height="382" alt="image" src="https://github.com/user-attachments/assets/f204f635-af8c-4af6-8e60-9103e6ac3505" />
Następnie w pierwszej zakładce należy kliknąć na jakiś port i z dropdowna status wybrać Disable
<img width="792" height="574" alt="image" src="https://github.com/user-attachments/assets/680ddda5-b31c-4d57-be99-f4da51827de6" />
Jak widać po kliknięciu Apply port został wyłączony
<img width="698" height="23" alt="image" src="https://github.com/user-attachments/assets/9aa3d800-2129-4924-bc56-4b6ed80356cc" />


## Zapisywanie 
Zawsze przed wyjściem z Switcha należy zapisać to co już zrobiliśmy - lecz nie chodzi mi tu o guzik 'Apply' w różnych zakład lecz chodzi mi tutaj o zaznaczenie opcji 'Save Config' na samym dole menu z zakładkami.
<img width="168" height="483" alt="image" src="https://github.com/user-attachments/assets/d3230cbc-c655-4947-92a1-7aef6d88916d" />
Wygląda tak
<img width="130" height="26" alt="image" src="https://github.com/user-attachments/assets/19faa240-fe93-4bf2-bd48-ac954308a463" />
Po kliknięciu Przycisku , zaakceptowaniu monitu przez kliknięcie guzika Ok mamy teraz 100% pewność ,że zapisaliśmy nasz progress



## Skonfigurowanie Trunka
Trunk w kontekście egzaminu praktycznego jest najtrudniejszym elementem jeśli chodzi o switcha.
Naszczęście jest dosyć rzadki , ponieważ był tylko na 4 egzaminach praktycznych i jak już jest to odejmuje się wtedy raczej jedno zadanie z egzaminu na jego rzecz lub reszta egzaminy jest trochę łatwiejsza.
Trunk był na tych egzaminach:
- egzamin2023-Styczeń-zad.03,04 
- egzamin2023-Czerwiec-zad.02 
- egzamin2024-czerwiec-zad.01
Tutaj niestety jak dostanie się trunka to będzie trzeba wtedy skonfigurować ustawienia z nim związane i na routerze i na switchu.
<img width="717" height="627" alt="image" src="https://github.com/user-attachments/assets/73681880-d598-4717-86ec-a1946a647195" />
<img width="713" height="462" alt="image" src="https://github.com/user-attachments/assets/cf6f582d-1557-4f78-bf66-13a81ea1e19f" />
> robienie Trunka na Mikrotiku jest wytłumaczone w folderze 'Mikrotik_Konfiguracja'

### Krok1. Tworzenie VLANów
Wchodzimy do zakładki VLAN-> 802.1Q VLAN -> Create -> Tworzymy nowy VLAN 
<img width="895" height="483" alt="image" src="https://github.com/user-attachments/assets/dcb1c79d-dc23-40e5-827c-be94527e532d" />

<img width="631" height="620" alt="image" src="https://github.com/user-attachments/assets/0b6b038d-b5af-4c5b-a8fa-06f157673fe6" />

> Nie musimy tworzyć VLANa o ID 1 bo fabrycznie jest nieusuwalny i już go mamy.

<img width="627" height="643" alt="image" src="https://github.com/user-attachments/assets/5aecd802-26ea-41a1-8245-0de51a6bcf20" />

<img width="718" height="229" alt="image" src="https://github.com/user-attachments/assets/4d336ee8-008e-4659-9305-d55d34b28431" />

Mamy Teraz trzy VLANy każdy z portami, które ma mieć. ( nie przejmujemy się, że Defauly VLAN ma wszystkie porty nie zmienimy tego. )

### Krok2. Zmienienie Portu nr 1. na Link-type 'Trunk'
przechodzimy do zakłądki 'Port Config'->Kliamy w pierwszy interfejs->Zmieniamy go na 'Link Type' Trunk

<img width="620" height="499" alt="image" src="https://github.com/user-attachments/assets/c22b9ba3-9ef6-4429-b388-0609383ce3fe" />

<img width="585" height="428" alt="image" src="https://github.com/user-attachments/assets/17d5c695-8789-4711-b503-969305e0f01b" />

Konfiguracja powinna wyglądać tak:

<img width="589" height="421" alt="image" src="https://github.com/user-attachments/assets/780ffe24-a95b-4097-87ff-dc4cf1114c2e" />

> Port 2,3 powinny być ustawione na 'Link Type' Access

### Krok3.
Wchodzimy teraz do każdego VLANa z osobna klikając guzik 'Edit' i upewniamy się czy Egress Rule dla Portu 1. Jest wszędzie Tagged a dla portów 2,3 Untagged - ponadto dodajemy do vlanów 2,3 port 1 po to aby kiedy pakiety idą do naszego VLANa będą one następnie przekazywane przez port1 jako tagowane do routera.

<img width="618" height="556" alt="image" src="https://github.com/user-attachments/assets/3f0ed11e-bfc6-4cc6-89ca-29bdb46889c8" />

<img width="628" height="624" alt="image" src="https://github.com/user-attachments/assets/dc0d95f2-86d8-4c39-895e-8a80648010d3" />

<img width="635" height="643" alt="image" src="https://github.com/user-attachments/assets/305a72cd-6e1e-4254-9cc3-f59deb89c252" />

Skończona konfiguracja powinna wyglądać tak:

<img width="705" height="183" alt="image" src="https://github.com/user-attachments/assets/005e3b78-b283-4de4-9868-6dbf84100d5d" />


Na koniec zmieniamy jeszczę Adres IP switcha według zadania.

<img width="860" height="466" alt="image" src="https://github.com/user-attachments/assets/9e614ae5-f0b4-4b14-a466-cef3dd94814e" />


Ethernet adapter Karta-USB:

   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : f220::32ba:dc86:3211:d2232%26
   IPv4 Address. . . . . . . . . . . : 192.168.0.254
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.0.1

Jak widać kiedy wszystko jest podłączone otrzymałem adres IP!







<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>








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

## Podstawowe komendy
Konfigurowanie przez CLI jest dosyć proste ponieważ mamy wsumie tylko 2 główne tryby w których operujemy a tak pozatym to nic zabardzo specjalnego tutaj nie ma ( oprócz zapamiętania na pamięc komend oczywiście ) 
Po podłączeniu się do Switcha pierwsze co widzimy na egzaminie to tryb nieuprzywilejowany - oznacza to ,że nic zabardzo nic możemy w nim robić - aby z niego wyjść należy wpisać komende 'enable'
<img width="164" height="60" alt="image" src="https://github.com/user-attachments/assets/80a66b01-7e93-4036-88db-ac541421965b" />
po wykonaniu tej komendy wchodzimy w tryb uprzywilejowany w którym możemy zacząć już coś robić.

mianiowicie możemy tutaj wydać komendy takie jak:

show running-config                     wyświetli obecną konfigurację 
<img width="650" height="425" alt="image" src="https://github.com/user-attachments/assets/e74663dc-afa1-4e23-80d0-0e2724bca252" />
show startup-config                     wyświetli konfigurację która automatycznie ładuje się przy starcie 
show vlan brief                         pokaże obecną konfiguracje VLANów - który port jest przypisany do czego
<img width="626" height="172" alt="image" src="https://github.com/user-attachments/assets/89fd7853-d66f-4113-a2f4-2a3b2da35fd1" />
show interfaces status                  pokaże obecny stan każdych interfejsów 
<img width="534" height="406" alt="image" src="https://github.com/user-attachments/assets/c3f1afed-84da-484e-aaa2-d294ba99a317" />
ping [adres_IP]                         wykona test komunikacji ( ta sama składnia jak na więkoszości urządzeń ) 
show interfaces trunk                   pokaże nam informację o trunkach w CLI                                                         ( jeszcze sprawdzić bo mój model nie obsługuje tej komendy ) 
< aby wyjść z jakiegoś trybu uprzywilejowania do tego pod nami należy to wykonać komendą 'exit'
<img width="199" height="52" alt="image" src="https://github.com/user-attachments/assets/3aa31d8b-927b-4f99-9b2e-1e6ac0fc5497" />

< aby usuwać w konsoli tekst jak coś źle wpisaliśmy powinniśmy przy usuwaniu słów trzymać SHIFT 

jeśli chcemy zobaczyć jakie komendy można wpisać do konsoli powinno się poprostu w nią wpisać znak zapytania - '?'

albo wpisać znak zapytania '?' po jakiejś komendzie aby otzymać informację o dopełnieniu jej czyli np.
<img width="508" height="76" alt="image" src="https://github.com/user-attachments/assets/5dd383f1-df72-4fb0-b9c9-712bac4686cc" />




### Zapisanie informacji 
Zpisać informacje możemy dzięki tym dwóm komendom 
- copy running-config startup-config ( w skrócie 'copy run start' )
- write ( w skrócie 'wr' )
obydwie te komendy robią dokładnie to samo i zapisują konfigurację tak ,że jak wyjdziemy z konsoli , wejdziemy do niej zpowrotem nasz progress się zapiszę.



## Konfiguracja Switcha 
Aby pójść krok dalej i zacząć konfigurować te rzeczy ,które są na egzaminie musimy wpisać komendę:

configure terminal ( w skrócie conf t )
<img width="244" height="25" alt="image" src="https://github.com/user-attachments/assets/e2787f0b-75c1-45ca-a97a-d3494b766189" />
tutaj mamy już większą swobode , możemy zacząć konfigurować interfejsy , Adresy IP , VLANy , trunki itd..

### konfiguracja adresu IP , maski podsieci , bramy domyślnej

TL-SG3424(config)# interface vlan 1                              --- to pozwoli nam wejść do konfiguracji VLANu który zawiera adres IP ( default vlan 1 )

TL-SG3424(config-if)# ip address 192.168.0.1 255.255.255.0       --- ta komenda pozwoli nam przypsać adres IP - pierwsze pole , maske sieciową - drugie pole do switcha

TL-SG3424(config-if)# exit                                       --- wychodzimy do ogólnej konfiguracji

TL-SG3424(config)# ip default-gateway 192.168.0.2                --- ta komenda pozwala nam ustawić brame domyślną switcha na dany adres 

### konfiguracja VLANów 
<img width="906" height="71" alt="image" src="https://github.com/user-attachments/assets/6e98fc91-4471-4124-989e-4ba71fa23004" />
( zrobimy to samo zadanie co wcześniej )

TL-SG3424# configure terminal

TL-SG3424(config)# vlan 100                                     --- wejście do konfiguracji vlana o ID 100

TL-SG3424(config-vlan)# name VLAN100                            --- nadanie mu nazwy ( description w GUI )

TL-SG3424(config-vlan)# exit                                    

TL-SG3424(config)# interface range fastEthernet 0/1-3           --- Wejście do intefejsów który będziemy zarządzać tutaj może być np.    interface range GigabitEthernet 0/1-3 jeśli porty są gigabitowe

> TL-SG3424(config)# interface fastEthernet 0/1                 --- Jeśli konfigurujemy jeden interfejs

TL-SG3424(config-if-range)# switchport mode access              --- Nadanie im trybu zarządzania na access

TL-SG3424(config-if-range)# switchport access vlan 100          --- połączenie portów z VLANem o ID 100 

TL-SG3424(config-if-range)# no shutdown                         --- sprawienie że porty są napewno włączone

TL-SG3424(config-if-range)# exit

TL-SG3424(config)# exit

TL-SG3424# copy running-config startup-config                   --- Zapisanie postępów 


### Tutaj mamy konfigurację tego samego co do góry ale tym razem z włączonym tagowaniem na wszystkich trzech portach 


TL-SG3424# configure terminal

TL-SG3424(config)# vlan 100                                     --- wejście do konfiguracji vlana o ID 100

TL-SG3424(config-vlan)# name VLAN100                            --- nadanie mu nazwy ( description w GUI )

TL-SG3424(config-vlan)# exit

TL-SG3424(config)# interface range fastEthernet 0/1-3           --- Wejście do intefejsów którymi będziemy zarządzać

TL-SG3424(config-if-range)# switchport mode general             --- Nadanie trybu zarządzanie na general ( aby było obsługiwane tagowanie )

TL-SG3424(config-if-range)# switchport general allowed vlan 100 tagged        --- połączenie portow z VLANem o ID 100 , włączenie tagowania

TL-SG3424(config-if-range)# no shutdown                         --- sprawienie że porty są napewno włączone

TL-SG3424(config-if-range)# exit

TL-SG3424(config)# exit

TL-SG3424# copy running-config startup-config                   --- Zapisanie postępów 
 
> Szybka powtórka z masek podsieci bo czemu nie

<img width="83" height="195" alt="image" src="https://github.com/user-attachments/assets/6fb1f550-db2b-408e-95f0-4709c99e8fa5" />


### wyłączenie portów
Aby wyłączyć port wystarczy wpisać w komendy 

TL-SG3424# configure terminal

TL-SG3424(config)# interface fastEthernet 0/1                   --- Wejście do intefejsów którymi będziemy zarządzać

TL-SG3424(config-if-range)# shutdown                            --- wyłączy port 

### UWAGA

to zależy od switcha ale na jednych switchach jest szansa ,że jak przez CLI wybieramy interfejsy to będziemy musieli wpisać przed numerem interfejsu jedynkę aby wybrać 'Numer switcha w stosie' - Nie trzeba tego wiedzieć na egzamin tylko trzeba poprostu wiedzieć ,że takie coś istnieje i można dostać z tym model.

przy wybieraniu interfejsu mamy 2 typy nazewnictwa portów zależących od modelu switcha 

- 1/0/1
lub
- 0/1

no chyba że robimy zakres to wtedy 

- 1/0/1-3
lub
- 0/1-3

żeby sprawdzić jakie nazwenictwo mają naszę porty należy wykonać ponownie komendę 'show interface status' w trybie uprzywilejowanym
<img width="536" height="405" alt="image" src="https://github.com/user-attachments/assets/11d423e2-8f18-46ba-b63b-3a3a3bfd6000" />
z obrazka dokładnie widać ,że w tym switchu stosuje się nazwenictwo z 1 na tyle czyli:

 Gi1/0/1

 ## Konfiguracja Trunka przez CLI 

> Do zrobienia ! ( nie sądze, że ktoś to przez CLI zrobi ale zrobię to gdzieś 15.05.2026 )


















	
