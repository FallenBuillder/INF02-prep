# Teoria

Na egzaminie praktycznym INF02 router (jak i switch) pojawiają się w każdym arkuszu, jaki napotkamy. Czasami zadania z nim związane są dosyć łatwe, a czasami trochę bardziej skomplikowane.

W tej sekcji skupimy się na routerze Mikrotikowym i metodach, dzięki którym możemy go skonfigurować przez GUI.

Konfiguracja Mikrotika przez CLI jest bardzo trudna i wymagałaby dużej znajomości dokumentacji, a więc nie ma jej tutaj.

### Zagadnienia

- jak się połączyć? i Resetowanie Routera 
- Podstawowy przykład konfiguracji na podstawie najprostszego egzaminu (Quick set) 
- Konfiguracja serwera DHCP 
- Konfiguracja Wi-Fi 
- Konfiguracja Router-on-a-stick - zarządzanie trunkami 

GUI - jak połączyć się z routerem

Aby połączyć się z routerem Mikrotikowym, potrzebny jest nam program WinBox. Program ten będzie na egzaminie albo już zainstalowany na naszym komputerze, albo będziemy musieli go doinstalować, uruchamiając instalator, który znajduje się na pendrivie USB opisanym PROGRAMY.

WinBox do wykrywania urządzeń nie używa protokołu IP, lecz protokołów warstwy drugiej (L2), takich jak MNDP lub CDP (Cisco Discovery Protocol). Router rozsyła specjalne ramki rozgłoszeniowe (broadcast), które WinBox potrafi przechwycić, o ile jesteś w tej samej sieci fizycznej - oznacza to, że nie musimy zmieniać ustawień kart sieciowych, aby się do niego dostać.

Teraz, jak mamy wszystkie narzędzia i wiedzę, możemy podejść do połączenia się.

### Krok 1.

Moim zdaniem przed połączeniem się do routera powinniśmy się upewnić, że jest zresetowany, ponieważ jeśli egzaminator przypadkowo zostawił skonfigurowany router i go nie zresetował po poprzedniej osobie, jest szansa, że się do niego nie połączymy, ponieważ ktoś ustawił wcześniej takie ustawienia.

Aby zresetować fabrycznie router Mikrotikowy, należy:

- odpiąć zasilanie
- trzymać guzik resetowania, który będzie w małej dziurce, np. zapałką
- włączyć zasilanie
- odczekać 5-6 sekund do momentu migania lampeczki z tyłu (niech lampeczka mignie sobie tak z 4 razy, abyśmy byli pewni, że się na pewno zresetował)
- wyciągnąć zapałkę

#### Krok 2.

Następnie należy połączyć się przewodem Ethernet do naszego mikrotika na porcie 2 - czemu nie na 1? Na porcie pierwszym wykrywanie po adresie MAC nie działa i służy on domyślnie do podłączenia do interfejsu WAN, a nie LAN.

Trzeba się upewnić, że:

jeden koniec Ethernetu jest wpięty do portu 2+ mikrotika, a drugi koniec do naszej stacji roboczej, z której go konfigurujemy.

karta sieciowa, do której wpiąliśmy mikrotika, jest włączona

#### Krok 3.

Następnie należy włączyć program WinBox w wersji v.3.41 lub v.3.43 (byle nie v0.4, ponieważ ta wersja jeszcze nie jest wymagana do egzaminu na rok 2026-czerwiec).

Na egzaminie nie będzie zbytnio wyboru wersji - będzie tylko ta starsza.

<img width="1181" height="744" alt="image" src="https://github.com/user-attachments/assets/ef34a139-fdd4-43e2-8e3b-8b08a5ae1e19" />

Interfejs Winboxa

#### Krok 4.

Na egzaminie INF02, kiedy połączymy się do jakiegoś routera, którego świeżo co dopiero zresetowaliśmy, pojawi się on w zakładce 'Neighbours' jako pierwszy, jeśli wszystko dobrze podłączyliśmy i będzie wyglądał tak:

<img width="1150" height="60" alt="image" src="https://github.com/user-attachments/assets/15cb7651-74ca-4001-94b8-5dd59ae3177f" />

UWAGA: Router nie pojawi się od razu po zresetowaniu, ponieważ trzeba odczekać pewien czas, żeby się przygotował - w większości przypadków około 30 sekund wystarczy, aby się pojawił.


(jednak tak nie jest) UWAGA: Z tego, co testowałem, to nie da się połączyć z routerem, jeśli mamy na karcie sieciowej adres APIPA - co to jest? Adres APIPA, taki jak np. 169.254.31.184 z maską 255.255.0.0 - jeśli mamy taki adres, oznacza to, że komputer nie pobrał adresu IP od np. routera, czyli serwer DHCP nie działa.

Następnie, aby połączyć się z Mikrotikiem, musimy w programie Winbox albo wpisać jego adres MAC, domyślny login jako admin i kliknąć guzik Connect.

<img width="1263" height="113" alt="image" src="https://github.com/user-attachments/assets/4ec2c46c-b668-4ef9-bda5-f3f7bd05d035" />

Albo możemy po prostu dwukrotnie kliknąć na adres MAC routera, co nas automatycznie do niego połączy.

<img width="209" height="60" alt="image" src="https://github.com/user-attachments/assets/ed7a0437-f7ad-4f2f-ace2-afb5e4d41e59" />


UWAGA: Jeśli po zresetowaniu mikrotika pojawi się nam okienko z monitem o usunięciu konfiguracji, nie można go zignorować - klikamy wtedy w nim guzik 'Remove Configuration', co sprawi, że stracimy na chwilę połączenie z mikrotikiem, a następnie automatycznie się z nim połączymy, tym samym resetując konfigurację.

<img width="1651" height="945" alt="image" src="https://github.com/user-attachments/assets/1b9b9e90-f7bd-465f-9df4-7399e04e3b47" />

Jesteśmy teraz zalogowani do routera i możemy zacząć jego konfigurację.

UWAGA: Możemy zignorować monit o zmianie hasła, ponieważ tylko nam przeszkodzi, jeśli je zmienimy, a następnie zapomnimy (no chyba że w arkuszu jest napisane, że mamy je zmienić (co się jeszcze nigdy nie stało)).

Podstawowy przykład konfiguracji

Aby zapoznać się lepiej z Mikrotikiem przed wchodzeniem do serwera DHCP, trunków, możemy się trochę z nim zapoznać poprzez zrobienie najprostszego zadania, jakie jest na arkuszach INF02 związanego ze skonfigurowaniem mikrotika:

<img width="975" height="306" alt="image" src="https://github.com/user-attachments/assets/aff9e637-e090-4ff9-aadd-4ed72c490e8e" />

Całe to zadanie może zostać wykonane przez Quick Set - Quick Set to przyjazny interfejs, dzięki któremu możemy ustawić podstawowe opcje związane z routerem.

<img width="135" height="510" alt="image" src="https://github.com/user-attachments/assets/9034456e-6136-4be0-b826-cee41f90a738" />

Jak widać na zamieszczonym obrazku, Quick Set możemy znaleźć na samej górze wszystkich ustawień w mikrotiku.

<img width="835" height="701" alt="image" src="https://github.com/user-attachments/assets/79a5f7a2-7787-4703-abdd-69372f45846f" />

Po kliknięciu w ten guzik pojawia się nam okienko, w którym możemy rozpocząć konfigurację, ale najpierw wybierzemy typ naszego routera z dropdowna w lewym górnym rogu.

<img width="168" height="129" alt="image" src="https://github.com/user-attachments/assets/a693cec1-c5a8-408c-99e6-afb833df5ee8" />

Radzę zawsze wybierać opcję Home AP, ponieważ jest najlepsza do ustawienia większości ustawień na tym urządzeniu.

W sekcji Internet konfigurujemy nasz interfejs WAN - czyli ether1, właśnie ten interfejs łączy router z innymi sieciami.

<img width="365" height="189" alt="image" src="https://github.com/user-attachments/assets/cd906655-b450-48d8-b57c-c5ed12f1a459" />

W sekcji Local Network konfigurujemy domyślnie port drugi, lecz jeśli chcemy, to możemy wybrać opcję Bridge All LAN Ports i wtedy wszystkie interfejsy naszego routera będą miały tę samą bramę domyślną, którą ustawimy za chwilę.

<img width="360" height="161" alt="image" src="https://github.com/user-attachments/assets/c06b4648-7559-4105-ae9c-8e7cde3ef945" />

W sekcji Wireless na razie nic nie będziemy robić, ale przyda nam się potem.

<img width="366" height="277" alt="image" src="https://github.com/user-attachments/assets/e0de1f35-08a6-41f7-be3f-2bad6dd28755" />

Następnie wypełniamy pola zgodnie z poleceniem zadania.

<img width="366" height="384" alt="image" src="https://github.com/user-attachments/assets/80c227b0-49dd-44f9-9726-51014e2e76a0" />

I w taki sposób wykonaliśmy całe zadanie dotyczące routera, używając Quick Seta.

Wyjaśnienie:

Zakładka Internet

Adres IP interfejsu WAN to jest po prostu inaczej adres IP ether1, a jeszcze inaczej adres służący do połączenia się do 'internetu', a więc przy wpisywaniu danych z tabelki po prostu musimy je przepisać zgodnie z tym, co jest napisane na arkuszu do zakładki Internet.

Tak samo robimy z bramą sieciową, gdzie wpisujemy po prostu taką bramę, jaką nam podali.

I podobnie robimy z maską podsieci, gdzie w zakładce 'Netmask' wybieramy /28 z dropdowna.

Następnie wpisujemy adresy serwerów DNS - 4.4.4.4 i 7.7.7.7 (aby dodać drugi serwer DNS, należy kliknąć strzałkę w dół obok zakładki DNS Servers).

Zakładka Local Network

W zakładce 'Local Network' jedyne, co musimy zrobić, to musimy wpisać adres IP bramy domyślnej naszego routera w dobrze oznaczone pole. Jeśli maska byłaby inna, analogicznie zmieniamy ją w opcji pod adresem IP.

Na koniec nie można zapomnieć, aby kliknąć przycisk Apply, aby zmiany się zapisały.

<img width="88" height="25" alt="image" src="https://github.com/user-attachments/assets/093ff231-da61-4588-90c2-d96184b8e75c" />

Konfiguracja serwera DHCP

Na razie wszystko było dosyć proste i zrozumiałe, ponieważ wystarczyło przepisywać wartości z arkusza do quickseta. Jeśli chodzi o serwer DHCP, to tutaj mamy minimalnie trudniejsze zadanie, ale nadal nie jest to nic złego.

Tak samo jak wcześniej, konfiguracja serwera DHCP będzie przedstawiona przez konfigurowanie zadania z egzaminu praktycznego.

Czyli:

<img width="983" height="348" alt="image" src="https://github.com/user-attachments/assets/138e191e-9f9d-419a-954b-9f2dd11f8659" />

Pierwsze trzy podpunkty możemy pominąć, ponieważ można je swobodnie zrobić przez Quick Set, tak jak w poprzednim przykładzie, a resztę będziemy konfigurować w innej zakładce.

Aby skonfigurować serwer DHCP, należy wejść do zakładki IP.

<img width="116" height="19" alt="image" src="https://github.com/user-attachments/assets/f9ea893a-829d-4f3a-84d6-cf1492df2422" />

Następnie z dropdowna wybrać opcję 'DHCP Server'.

<img width="251" height="525" alt="image" src="https://github.com/user-attachments/assets/d32615bb-72a9-4629-94dc-d77cc6aa311b" />

Menu wygląda następująco:

<img width="598" height="377" alt="image" src="https://github.com/user-attachments/assets/91694e2d-9fb5-4b4e-9b3f-40d5517860fc" />

Następnie klikamy guzik DHCP Setup, aby rozpocząć konfigurację.

<img width="80" height="24" alt="image" src="https://github.com/user-attachments/assets/71683035-a902-4d3c-be46-8d1a2f9dd9c8" />

W pierwszym okienku wybieramy ether2, ponieważ nasz serwer DHCP będzie rozdawał adresy IP właśnie na tym interfejsie.

<img width="272" height="173" alt="image" src="https://github.com/user-attachments/assets/4900abe7-3d01-439e-bb60-ba6042c0ab0f" />

Sieć skonfiguruje się automatycznie, możemy przejść dalej.

<img width="272" height="171" alt="image" src="https://github.com/user-attachments/assets/8e0acd29-e6bd-47cf-8e86-526bc63eb8ef" />

Brama domyślna też skonfiguruje się sama, możemy przejść dalej.

<img width="272" height="173" alt="image" src="https://github.com/user-attachments/assets/5712a1e9-6ad6-4349-9e26-c54c8b2e1282" />

W Addresses to Give Out: Tutaj wybieramy właśnie tę pulę adresów, którą będzie używał nasz serwer DHCP i z której podłączone do niego komputery mogą brać adresy IP - zmieniamy tutaj domyślne wartości na takie, które dostaliśmy w arkuszu, czyli 172.16.10.100 ÷ 172.16.10.110.

<img width="272" height="170" alt="image" src="https://github.com/user-attachments/assets/f8ae2282-3fbb-426f-bfde-e00a35b99e14" />

W tej zakładce wybieramy serwery DNS, które będziemy używać w naszym serwerze DHCP - może być napisane w arkuszu, że serwery DNS mają być inne dla interfejsu WAN i dla interfejsu serwera DHCP, ale nie powinno tak być, a więc zostawiamy te, które ustawiliśmy.

<img width="272" height="171" alt="image" src="https://github.com/user-attachments/assets/7ca76384-74c4-4726-9155-411dd2a7f6fd" />

Lease Time oznacza, ile minut dany komputer ma trzymać adres IP przed pobraniem nowego - w tym przypadku zostawiamy to pole tak, jak jest, bo nikt nie powiedział, że mamy je zmienić.

<img width="273" height="171" alt="image" src="https://github.com/user-attachments/assets/45d6aea0-190d-45b6-b914-b2a2c499d74b" />

Pomyślnie skonfigurowaliśmy router!

<img width="191" height="102" alt="image" src="https://github.com/user-attachments/assets/95563bbe-cc20-431e-aca2-c87f2ac37203" />

Stworzenie dzierżawy (Lease)

Aby stworzyć Lease (zarezerwować jakiś adres IP danemu komputerowi po adresie MAC), należy:

Wrócić do zakładki DHCP Server, wejść w Leases.

<img width="593" height="374" alt="image" src="https://github.com/user-attachments/assets/2251a6b9-ebed-423e-b1bc-917f2aa46347" />

Tutaj klikamy guzik + i pojawia się nam to okienko.

<img width="377" height="422" alt="image" src="https://github.com/user-attachments/assets/306b9979-e7e6-4948-8ad6-8f9ccc8cc335" />

W tym okienku zmieniamy pole Address na adres, który chcemy dać komputerowi, który go rezerwuje, a w pole MAC Address wpisujemy adres MAC tego komputera, który możemy znaleźć przez wpisanie na Windowsie komendy 'ipconfig /all' w terminalu i znalezienie adresu MAC przypisanego do interfejsu połączonego do routera lub na Linuxie w terminalu wpisanie komendy 'ip a', która także pokaże nam adres MAC interfejsu połączonego do routera, który następnie wpiszemy w nasze pole.

W moim przypadku adres MAC mojej stacji roboczej widnieje na tym obrazku po wpisaniu komendy 'ipconfig /all' w terminalu Windows.

<img width="758" height="310" alt="image" src="https://github.com/user-attachments/assets/223333a1-6bb0-44d4-81f9-f722bfd54fbd" />

Po wpisaniu adresu MAC do sekcji MAC Address, możemy kliknąć Apply, OK, co sprawi, że zmiany się zapiszą.

<img width="374" height="423" alt="image" src="https://github.com/user-attachments/assets/e1a7fbe7-d8e6-494c-ab83-41b01bc777c7" />

Ethernet adapter Karta-USB:

IPv4 Address. . . . . . . . . . . : 172.16.10.105(Preferred)

Subnet Mask . . . . . . . . . . . : 255.255.255.128

Jak widać, serwer DHCP działa poprawnie.

Troubleshooting

Jeśli źle się wpisało pulę adresów do serwera DHCP, to nie trzeba usuwać całego serwera DHCP i zaczynać od początku. Wystarczy wejść do zakładki IP > Pool.

<img width="255" height="523" alt="image" src="https://github.com/user-attachments/assets/2bb6b9db-e03a-47f7-9c97-7c0baa3af6d8" />

A następnie w tej zakładce klikamy na źle utworzony Pool.

<img width="428" height="373" alt="image" src="https://github.com/user-attachments/assets/51002420-7d2b-4d13-be5a-5dec51889ebf" />

I zmieniamy jego zakres i klikamy Apply, OK.

<img width="303" height="202" alt="image" src="https://github.com/user-attachments/assets/9217e650-8703-4b99-820b-6984e3e1429d" />

Konfiguracja Wi-Fi na Mikrotiku

<img width="779" height="412" alt="image" src="https://github.com/user-attachments/assets/0fd3f5e7-33f6-4c4f-94e4-289403f21f7d" />

Aby wytłumaczyć, jak skonfigurować Wi-Fi na routerze Mikrotikowym, posłużymy się powyższym przykładem.

<img width="1302" height="269" alt="image" src="https://github.com/user-attachments/assets/fa409749-ace8-42f1-8f9c-3b428b351ec7" />

Najpierw zrobimy część zadania, którą już de facto wiemy, jak zrobić. Całą tę część da się skonfigurować za pomocą QuickSeta - lub można zrobić to manualnie, co będzie pokazane pod koniec.

<img width="1115" height="598" alt="image" src="https://github.com/user-attachments/assets/0b097896-9687-422d-a0f5-3dee79097af4" />

Jak widać przez to, że użyliśmy quickseta, adresy IP dla danych portów stworzyły się automatycznie.

<strong>Zmieniłem potem adres dla LANu z 192.168.1.128 na 192.168.1.129</strong>

<strong>Teraz możemy przejść do części z konfiguracją Wi-Fi</strong>

Zakładka, która zawiera ustawienia Wi-Fi, to czwarta zakładka, patrząc od początku.

<img width="136" height="533" alt="image" src="https://github.com/user-attachments/assets/71c60cdf-2a70-4b75-a811-0ae261f3a8e0" />

<img width="126" height="32" alt="image" src="https://github.com/user-attachments/assets/a6f111f6-84f9-45b4-a9d8-349a210def7f" />

<img width="875" height="381" alt="image" src="https://github.com/user-attachments/assets/44a4ee75-18ff-4d69-a3ac-8cf1f9dd9dbb" />

Jak widać, wyświetla się nam menu, w którym mamy interfejs 'wlan1', który będziemy konfigurować.

<img width="531" height="505" alt="image" src="https://github.com/user-attachments/assets/920dfd9c-c6e1-4774-9aa3-fa8b658b9dbe" />

Po kliknięciu w interfejs 'wlan1' pokaże się nam menu, w którym jedyną ważną zakładką, której będziemy używać, będzie zakładka 'Wireless' - to właśnie tutaj możemy zmienić nasze SSID, kanał, Security Profile, kraj.

<img width="872" height="378" alt="image" src="https://github.com/user-attachments/assets/38793098-e170-4527-9c5a-a742d1184864" />

Kluczowym elementem konfiguracji jest także zakładka 'Security Profiles'. To właśnie tutaj definiujemy politykę bezpieczeństwa naszej sieci bezprzewodowej, wybierając standard uwierzytelniania (np. WPA2) oraz konkretne algorytmy szyfrowania danych, ponadto ustawiamy tutaj także hasło służące do tego, abyśmy się dostali do naszego Wi-Fi.

<img width="891" height="490" alt="image" src="https://github.com/user-attachments/assets/1d98f427-73bb-40b1-8572-8532b2c17790" />

Po kliknięciu na domyślny security profile, który z automatu używa wlan1, widzimy wcześniej wymienione ustawienia.

W zadaniu jest napisane, abyśmy ustawili:

SSID na wifi-x (SSID jest po prostu nazwą sieci, jaka się pojawia, kiedy się z nią łączymy) - po tym poznajemy, jaka sieć jest jaka.

Klucz dostępu na stanowisko-x (klucz dostępu to inaczej po prostu hasło do naszego Wi-Fi).

Najsilniejsze możliwe szyfrowanie - oznacza to, że mamy ustawić szyfrowanie na WPA2-PSK i aes ccm - ponieważ jest to najsilniejsze szyfrowanie w tych modelach mikrotików.

Numer kanału na 7 - Wi-Fi może mieć wiele kanałów i może być ustawione na wielu kanałach. Mamy ustawić nasze Wi-Fi na inny kanał, aby nie kolidowało z innymi różnymi sieciami Wi-Fi, które są wystawione na innych kanałach.

<strong>Poprawnie skonfigurowane zadanie wyglądałoby tak:</strong>

<img width="1827" height="940" alt="image" src="https://github.com/user-attachments/assets/3cced199-bbb4-4d63-9b8a-2e55937b078e" />

Jeśli w QuickSecie nie można kliknąć apply, wystarczy po prostu wpisać to samo hasło w pole Wifi Password i następnie zapisać Quick Seta.

Na razie, jeśli będziemy chcieli połączyć się naszym telefonem do sieci, to nie otrzymamy adresu IP, ponieważ nie skonfigurowaliśmy serwera DHCP.

Konfiguracja serwera DHCP na interfejsie wlan1

<img width="728" height="548" alt="image" src="https://github.com/user-attachments/assets/991f8162-3677-4f0e-9876-37d55dd26080" />

Dla prostoty użyjemy znowu Quick Seta, tym razem w trybie 'WISP AP' - w tym trybie da się skonfigurować wszystko w prosty sposób.

<img width="312" height="130" alt="image" src="https://github.com/user-attachments/assets/ce859363-e21d-4e0c-9bda-c746f282ff84" />

<img width="839" height="704" alt="image" src="https://github.com/user-attachments/assets/287f15f7-7882-45e2-96fe-28ede4057d85" />

Teraz wystarczy po prostu wypełnić dane, które otrzymaliśmy w zadaniu dotyczące LANu i WANu.

<img width="836" height="703" alt="image" src="https://github.com/user-attachments/assets/0813429e-99d6-466c-9981-4bc2b995a627" />

Następnie wypełniamy dane dotyczące Wi-Fi.

<img width="831" height="721" alt="image" src="https://github.com/user-attachments/assets/8ff3cc9f-ec0d-41a3-a479-eeeb316476f9" />

Po kliknięciu 'Apply' interfejs wlan1 (wifi) nam się włączył.

<img width="1383" height="194" alt="image" src="https://github.com/user-attachments/assets/06417de9-2dfa-47fb-9dad-ef0ed52c5658" />

Ostatnim krokiem jest stworzenie mostu, dodanie do niego i ether2 i wlan1, przypisanie go do serwera DHCP.

<img width="1176" height="454" alt="image" src="https://github.com/user-attachments/assets/dad46734-a75f-4762-8d8a-b0869a7623b7" />

<img width="1141" height="357" alt="image" src="https://github.com/user-attachments/assets/1e31fd83-9931-4fbc-8c41-d382fe5a26b3" />

<img width="1127" height="388" alt="image" src="https://github.com/user-attachments/assets/f9c8fc02-350a-4262-827c-3ec2bfc578d4" />

<img width="597" height="293" alt="image" src="https://github.com/user-attachments/assets/26bd8ed7-ec3a-4b6a-a74d-d18c29184509" />

Przed dodaniem zmienieniem miejsca, na którym wystawiane są nasze usługi na most, trzeba najpierw dodać adres IP interfejsowi wlan1.
<br>
<img width="619" height="394" alt="image" src="https://github.com/user-attachments/assets/c26606fc-cc5e-443f-ad8c-9f97fbf182ea" />
<br>
Następnie wchodzimy do IP->DHCP Server->Klikamy na nasz obecny serwer DHCP-> zmieniamy interfejs na nasz most, czyli 'WLAN+LAN'.
<br>
<img width="386" height="502" alt="image" src="https://github.com/user-attachments/assets/fef87035-07b2-4cd4-935c-531e1e794740" />
<br>
Serwer DHCP powinien wyglądać teraz tak:
<br>
<img width="844" height="388" alt="image" src="https://github.com/user-attachments/assets/e44a5fdd-ef89-4139-a536-cc3df4440287" />
<br>
W zakładce Leases widać, że mój iPhone połączył się do serwera DHCP.
<br>
<img width="256" height="40" alt="image" src="https://github.com/user-attachments/assets/6841126e-11e1-4e8d-8ae0-ff917c94bfba" />
<br>
W tej samej zakładce (Leases) dodajemy nowy lease, klikając guzik '+'.
<br>
<img width="379" height="428" alt="image" src="https://github.com/user-attachments/assets/7de6fb1b-f825-44a6-8ae5-a4e3c4a091dc" />
<br>
Tutaj wpisujemy adres IP dla urządzenia z konkretnym adresem MAC, aby miał on ten adres za każdym razem, jak podłączy się do sieci:
<br>
<img width="380" height="424" alt="image" src="https://github.com/user-attachments/assets/e780a951-4ab9-4eb0-b623-1ea571e3b56a" />

Wszystko powinno być teraz skonfigurowane. Lecz trzeba jeszcze zwrócić uwagę na parę istotnych uwag:

Quick Set czasami miesza się z ręcznymi ustawieniami, co oznacza, że jest szansa, że jeśli coś nam nie zadziała, będziemy chcieli logicznie spróbować odbudować nasz problem. Po pierwsze, każdy interfejs urządzenia warstwy trzeciej, do którego będziemy się komunikować, musi mieć adres IP, aby z nim rozmawiać (nieważne, czy jest to adres IP jeden dla całego mostu, lub adres IP jednego interfejsu). Po drugie, serwer DHCP jest usługą, którą ustawia się na dany port. Serwer DHCP (na mikrotiku)

nie jest magiczną usługą, która będzie dawać adresy IP każdemu hostowi, jeśli jakkolwiek podłączymy się do routera. Musimy wiedzieć, jak i gdzie mamy się do niego podłączyć. Po trzecie, wszystko, co zostało tutaj przedstawione, da się także zrobić manualnie i przez zakładkę Wireless, a więc jeśli Quick Set z jakiegokolwiek powodu nie działa, zawsze można zrobić zadanie, jeśli zna się podstawy sieci.

Jeśli ktoś każe nam w zadaniu ustawić kanał na np. 7, oznacza to, że mamy +5 MHz za każdy kanał w polu Frequency (domyślnie jesteśmy na kanale 1, bo 2422-2427) - co to oznacza? Oznacza to, że jeśli ktoś powie nam, że mamy ustawić kanał na 7, to dodajemy wartość wszystkich poprzednich kanałów do domyślnego ustawienia, które jest 2422, tak abyśmy otrzymali kanał docelowy:

Kanał 1: 2412 MHz

Kanał 2: 2417 MHz

Kanał 3: 2422 MHz

Kanał 4: 2427 MHz

Kanał 5: 2432 MHz

Kanał 6: 2437 MHz

Kanał 7: 2442 MHz


Konfiguracja trunka na Mikrotiku

<img width="717" height="627" alt="image" src="https://github.com/user-attachments/assets/73681880-d598-4717-86ec-a1946a647195" />

<img width="713" height="462" alt="image" src="https://github.com/user-attachments/assets/cf6f582d-1557-4f78-bf66-13a81ea1e19f" />

<strong>Dlaczego trunk jest przydatny?</strong>

Bez trunka, aby połączyć 3 sieci VLAN między routerem a switchem, musiałbyś pociągnąć 3 osobne kable. Przy 20 VLAN-ach zabrakłoby Ci portów w urządzeniach. Trunk pozwala obsłużyć dowolną liczbę sieci przy użyciu tylko jednego kabla.

<strong>Do czego służy i jak działa?</strong>

Służy do: przesyłania ruchu z wielu odizolowanych sieci (VLAN) przez jeden fizyczny interfejs.

<strong>Jak działa</strong>: Wykorzystuje standard 802.1q. Do każdej ramki danych "doklejany" jest mały znacznik (tag) z numerem ID sieci. Gdy router wysyła dane do VLAN 2, dodaje tag "2". Przełącznik odbiera ramkę, widzi tag i wie, że ma ją wysłać tylko do portów należących do VLAN 2. Przed wysłaniem danych do komputera (tryb Access), przełącznik usuwa ten tag.

Jak skonfigurować trunka na routerze..?

To zależy od zadania, ale kiedy konfigurujemy trunka, to albo wystarczy nam sam trunk, albo będziemy musieli jeszcze dodatkowo postawić serwer DHCP na jednej z sieci trunkowych.

<img width="837" height="705" alt="image" src="https://github.com/user-attachments/assets/5e5a2951-b9a6-4341-9af2-927762a7dd71" />

Najpierw robimy to, co już wiemy, jak zrobić i przechodzimy do trudniejszej części.

Tworzenie trunka na routerze składa się z dwóch części:

Tworzenie wirtualnych vlanów

Przypisywanie wirtualnym vlanom adresów IP

Krok 1. Tworzenie wirtualnych vlanów

Aby stworzyć wirtualne vlany na mikrotiku, należy wejść do zakładki Interfaces->VLAN - tutaj będziemy tworzyć VLANy poprzez kliknięcie guzika '+'.

<img width="456" height="452" alt="image" src="https://github.com/user-attachments/assets/ce7fad2f-5a6a-4e12-b19b-33dc3ea641a3" />

Po kliknięciu guzika '+' wpisujemy następujące parametry i tworzymy pierwszą sieć VLAN.

<img width="454" height="452" alt="image" src="https://github.com/user-attachments/assets/e964034f-65d4-460e-bb6f-0da950c38d21" />

<br>
<img width="449" height="451" alt="image" src="https://github.com/user-attachments/assets/cc089507-953f-4ff0-aa5f-c238278fbaf7" />

Analogicznie tworzymy dwie dodatkowe sieci VLAN i dostajemy następującą konfigurację.

<img width="1274" height="236" alt="image" src="https://github.com/user-attachments/assets/172a4bdd-098c-4771-b7ed-c783ce428923" />

Krok 2. Przypisywanie adresów IP do vlanów

Aby dodać adresy IP do naszych wirtualnych vlanów, należy przejść do IP->Addresses.

<img width="611" height="406" alt="image" src="https://github.com/user-attachments/assets/54664e22-a137-4d1d-8f01-d45632d9fbd0" />

Po kliknięciu guzika '+' wpisujemy następujące parametry:

<img width="300" height="248" alt="image" src="https://github.com/user-attachments/assets/5a6a84ab-ace0-4a18-b7f6-f5df9cb77215" />
<br>
<img width="300" height="249" alt="image" src="https://github.com/user-attachments/assets/c72f9c51-26b9-4048-bcd2-4d4284151f94" />
<br>
<img width="297" height="244" alt="image" src="https://github.com/user-attachments/assets/01e999e7-3bbf-4424-a07b-72440933bfaf" />

Wynik powinien wyglądać tak:

<img width="350" height="390" alt="image" src="https://github.com/user-attachments/assets/8465cf2d-2262-40b5-9892-d2d22d2051e9" />

Jak się wątpi, czy routing pomiędzy tymi VLANami się automatycznie zrobił, można podejrzeć zakładkę IP->Routes
.
<img width="718" height="398" alt="image" src="https://github.com/user-attachments/assets/81b4b3b2-d12c-4055-a5cf-525c4c12e6b8" />

Krok 3. Serwer DHCP na VLANie (dodatkowy)

Następnie przejdziemy do konfiguracji serwera DHCP na jednym z wirtualnych VLANów (było takie zadanie na egzaminie) - zrobienie tego nie jest aż tak trudne, jak się wydaje, ponieważ możemy dodać serwer DHCP do wirtualnego interfejsu tak samo, jak byśmy tworzyli go dla danego portu.

Konfiguracja:

Wchodzimy w IP->DHCP Server->DHCP Setup->Wybieramy interfejs, na którym chcemy rozdawać adresy IP.

<img width="1136" height="540" alt="image" src="https://github.com/user-attachments/assets/253a7a79-59f1-42d0-bff1-eb396e152245" />
<br>

Następnie konfigurujemy serwer DHCP tak, jak byśmy konfigurowali normalny serwer DHCP.

<img width="272" height="177" alt="image" src="https://github.com/user-attachments/assets/f0283f24-7f21-4c6e-bf9a-e5d6814d6db2" />
<br>
<img width="275" height="172" alt="image" src="https://github.com/user-attachments/assets/ea05a633-b8f2-4c6a-8244-00b1d3e2444e" />
<br>
<img width="274" height="172" alt="image" src="https://github.com/user-attachments/assets/b3ee86ce-8d71-410a-a32a-526d7d62941e" />
<br>
<img width="272" height="172" alt="image" src="https://github.com/user-attachments/assets/1a7b94c0-5ccb-4f55-ae06-fc4ca94156ce" />
<br>
<img width="275" height="174" alt="image" src="https://github.com/user-attachments/assets/7faede7e-0e11-4df3-8bd7-cd4eee4663c4" />
<br>
<img width="198" height="109" alt="image" src="https://github.com/user-attachments/assets/50ece209-fb35-487d-ac1e-5997449a4734" />
<br>
Serwer DHCP powinien już nam działać.
<br>
<img width="613" height="383" alt="image" src="https://github.com/user-attachments/assets/3f448f12-bf3c-454c-8c7f-8b9c792a583c" />
Jak to działa? - Jeśli podłączymy się do VLANa o ID 3 na switchu i włączymy na naszej karcie sieciowej DHCP - powinniśmy dostać adres IP od tego serwera DHCP - jeśli połączymy się do innego VLANa o innym ID, to wtedy nie dostaniemy adresu, bo na tym VLANie nie ma serwera DHCP!

Dodatkowe zadanie z trunkiem.

<img width="1054" height="474" alt="image" src="https://github.com/user-attachments/assets/4c2dc1ff-b3cf-4d4e-9582-b76b09f6b7f2" />

<img width="1057" height="743" alt="image" src="https://github.com/user-attachments/assets/0b2fa7f9-3152-4583-82e9-74b6e79d6c43" />
