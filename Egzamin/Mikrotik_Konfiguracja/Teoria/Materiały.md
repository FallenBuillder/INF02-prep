# Teoria 

Na egzaminie Praktycznym INF02 router ( jak i switch ) pojawiają się w każdym arkuszu jaki napotkamy. Czasami zadania z nim związane są dosyć łatwe a czasami trochę bardziej bogmatwane

W tej sekcji skupimy się na routerze Mikrotikowym i metodami dzięki którymi możemy go skonfigurować przez GUI 
> Konfiguracja Mikrotika przez CLI jest bardzo trudna i wymagałaby dużej znajomości dokumentacji a więc nie ma jej tutaj.

Zagadnienia 

- jak się połączyć ? && Resetowanie Routera ✅
- Podstawowy przykład konfiguracji na podstawie najprostszego egzaminu ( Quick set ) ✅
- Konfiguracja serwera DHCP ✅
- Konfiguracja Wi-FI ❌
- Konfiguracja Router-on-a-stick - zarządzanie trunkami ❌
  

### GUI - jak połączyć się z Routerem 
Aby połączyć się z routerem Mikrotikowym potrzebny jest nam program WinBox. Program ten będzie na egzaminie albo już zainstalowany na naszym komputerze albo będziemy musieli go doinstalować uruchamiając instalator który znajduję się na Pendrivie USB opisanym PROGRAMY.
WinBox do wykrywania urządzeń nie używa protokołu IP, lecz protokołów warstwy drugiej (L2), takich jak MNDP lub CDP (Cisco Discovery Protocol). Router rozsyła specjalne ramki rozgłoszeniowe (broadcast), które WinBox potrafi przechwycić, o ile jesteś w tej samej sieci fizycznej - oznacza to ,że nie musimy zmieniać ustawień kart sieciowych aby się do niego dostać.

Teraz jak mamy wszystkie Narzędzia i wiedzę możemy podejśc do połączania się.

## krok 1.
Moim zdaniem przed połączeniem się do routera powinniśmy się upewnić ,że jest zresetowany ponieważ jeśli egzaminator przypadkowo zostawił skonfigurowany router i go nie zresetował po poprzedniej osobie jest szansa ,że się do niego nie połączymy ponieważ ktoś ustawił wcześniej takie ustawienia.
[Link do filmiku z zresetowaniem Mikrotika](https://www.youtube.com/shorts/4uuZvSC2dlU)

Aby zresetować fabrycznie Router Mikrotikowy należy:
- odpiąć zasilanie
- trzymać guzik resetowania który będzie w małej dziurce np. zapałką
- włączyć zasilanie
- odczekać 5-6 sekund do momentu migania lampeczki z tyłu ( niech lampeczka mignie sobie tak z 4 razy abyśmy byli pewni ,że się napewno zresetował )
- wyciągnąć zapałkę

## krok 2. 
Następnie należy połączyć się przewodem Ethernet do naszego mikrotika na porcie 2 - czemu nie na 1 ? na porcie pierwszym wykrywanie po adresie MAC nie działa i służy on defaultowo do podłączenia do intefejsu WAN a nie LAN.
Trzeba się upewnić ,że
- jeden koniec Ethernetu jest wpięty z do portu 2+ mikrotika a drugi koniec do naszej stacji roboczej z której go konfigurujemy.
- że karta sieciowe do której wpieliśmy mikrotika jest włączona

## krok 3.
Następnie należy włączyć program WinBox w wersji v.3.41 lub v.3.43 ( byle nie v0.4 ponieważ ta wersja jeszcze nie jest wymagana do egzaminu na rok 2026-czerwiec ) 
> na egzaminie nie będzie zabardzo wyboru wersji - będzie tylko ta starsza.
<img width="1181" height="744" alt="image" src="https://github.com/user-attachments/assets/ef34a139-fdd4-43e2-8e3b-8b08a5ae1e19" />
Interfejs Winboxa

## krok 4.
na egzaminie INF02 kiedy połączamy się do jakiegoś routera którego świeżo co dopiero zresetowaliśmy pojawi się on w zakładce 'Neighbours' jako pierwszy jeśli wszystko dobrze podłączyliśmy i będzie wyglądał tak: 
<img width="1150" height="60" alt="image" src="https://github.com/user-attachments/assets/15cb7651-74ca-4001-94b8-5dd59ae3177f" />
> UWAGA: Router nie pojawi się odrazu po zresetowaniu. ponieważ trzeba odczekać pewien czas żeby się przygotował - w więkoszości przypadków około 30 sekund wystarczy aby się pojawił

> ( jednak tak nie jest ) UWAGA: Z tego co testowałem to nie da połączyć się z routerem jeśli mamy na karcie siecowej Adres APIPA - co to jest? adres APIPA taki jak np. 169.254.31.184 z maską 255.255.0.0 jeśli mamy taki adres oznacza to ,że komputer nie porbrał adresu IP od np. Routera czyli server DHCP nie działa.

Następnie aby połączyć się z Mikrotikiem musimy w programie Winbox albo wpisać jego adres MAC , Defaultowy login jako admin i kliknąć guzik Connect
<img width="1263" height="113" alt="image" src="https://github.com/user-attachments/assets/4ec2c46c-b668-4ef9-bda5-f3f7bd05d035" />

Albo możemy poprostu dwukrotnie kliknąć na adres MAC routera co nas automatycznie do niego połączy.
<img width="209" height="60" alt="image" src="https://github.com/user-attachments/assets/ed7a0437-f7ad-4f2f-ace2-afb5e4d41e59" />
> UWAGA: Jeśli po zresetowaniu mikrotika pojawi się nam okienko z monitem o usunięciu konfiguracji nie można go zignorować - Klikamy wtedy w nim guzik 'Remove Configuration' co sprawi ,że stracimy na chwilę połączenie z mikrotikiem a następnie automatycznie się z nim połączymy tym samym resetując konfiguracje.

<img width="1651" height="945" alt="image" src="https://github.com/user-attachments/assets/1b9b9e90-f7bd-465f-9df4-7399e04e3b47" />
Jesteśmy teraz zalogowani do routera i możemy zacząć jego konfigurację

> UWAGA: Możemy zignorować monit o zmianie hasła ponieważ tylko nam przeszkodzi jeśli je zmienimy a następnie zapomnimy ( no chyba, że w arkuszu jest napisane, że mamy je zmienić ( co się jescze nigdy nie stało ))


### Podstawowy przykład konfiguracji


Aby zapoznać się lepiej z Mikrotikiem przed wchodzeniem do Serwera DHCP , trunków możemy się trochę z nim zapoznać poprzez zrobienie najprostszego zadania jakie jest na arkuszach INF02 związanego z skonfigurowaniem mikrotika:
<img width="975" height="306" alt="image" src="https://github.com/user-attachments/assets/aff9e637-e090-4ff9-aadd-4ed72c490e8e" />
Całe to zadanie może zostać wykonane przez Quick Seta - Quick Set to przyjazny interfejs dzięki któremu możemy ustawić podstawowe opcję związane z routerem.
<img width="135" height="510" alt="image" src="https://github.com/user-attachments/assets/9034456e-6136-4be0-b826-cee41f90a738" />
Jak widać na zamieszczonym obrazku Quick Seta możemy znaleść na samej górze wszytkich Ustawień w mikrotiku.
<img width="835" height="701" alt="image" src="https://github.com/user-attachments/assets/79a5f7a2-7787-4703-abdd-69372f45846f" />
po kliknięciu w ten guzik pojawia się nam okienko w którym możemy rozpocząć konfiguracje ale najpierw wybierzemy Typ naszego Routera z dropdowana w lewym górnym rogu.
<img width="168" height="129" alt="image" src="https://github.com/user-attachments/assets/a693cec1-c5a8-408c-99e6-afb833df5ee8" />
Radze zawsze wybierać opcję Home AP ponieważ jest najlepsza do ustawienia więkoszości ustawień na tym urządzeniu.


W sekcji internet konfigurujemy nasz interfejs WAN - czyli ether1 właśnie ten interfejs łączy router z innymi sieciami
<img width="365" height="189" alt="image" src="https://github.com/user-attachments/assets/cd906655-b450-48d8-b57c-c5ed12f1a459" />
W sekcji Local Network konfigurujemy domyślnie Port drugi lecz jeśli chcemy to możemy wybrać opcję Bridge All LAN Ports i wtedy wszystkie interfejsy naszego Routera będą miały tą samą brame domyślną którą ustawimy za chwilę 
<img width="360" height="161" alt="image" src="https://github.com/user-attachments/assets/c06b4648-7559-4105-ae9c-8e7cde3ef945" />
W sekcji Wireless narazie nic nie będziemy robic ale przyda nam się potem 
<img width="366" height="277" alt="image" src="https://github.com/user-attachments/assets/e0de1f35-08a6-41f7-be3f-2bad6dd28755" />

Następnie wypełniamy Pola zgodnie z poleceniem zadania 

<img width="366" height="384" alt="image" src="https://github.com/user-attachments/assets/80c227b0-49dd-44f9-9726-51014e2e76a0" />
i w taki sposób wykonaliśmy całe zadanie dotyczące Routera używając Quick Seta 

Wyjaśnienie:

Zakładka Internet

- Adres IP interfejsu WAN to jest poprostu inaczej adres IP ether1 a jeszcze inaczej adres służący do połączenia się do 'internetu' a więc przy wpisywaniu danych z tabelki poprostu musimy je przepisać zgodnie z tym co jest napisane na arkuszu do zakłądki Internet.
- tak samo robimy z Bramą sieciową gdzie wpisujemy poprostu taką bramę jaką nam podali
- i podobnie robimy z Maską podsieci gdzie w zakłądce 'Netmask' wybieramy /28 z dropdowna
- Następnie wpisujemy adresy serverów DNS - 4.4.4.4 i 7.7.7.7 ( aby dodać drugi server DNS należy kliknąć strzałke w dół obok zakładki DNS Servers )
  
Zakładka Local Network

- w zakładce 'Local Network' jedyne co musimy zrobić to musimy wpisać adres IP bramy domyślnej naszego routera w dobrze oznaczone pole. jeśli maska byłaby inna analogicznie zmieniamy ją w opcji pod adresem IP.

Na koniec nie można zapomnieć aby kliknąć przycisk Apply aby zmiany się zapisały.
<img width="88" height="25" alt="image" src="https://github.com/user-attachments/assets/093ff231-da61-4588-90c2-d96184b8e75c" />


### konfiguracja Servera DHCP 
Narazie wszystko było dosyć prostę i zrozumiałe ponieważ wystarczyło przepisywać wartości z arkusza do quickseta jeśli chodzi o server DHCP to tutaj mamy minilanie trudniejsze zadanie ale nadal nie jest to nic złego.

Tak samo jak wcześniej Konfiguracja Servera DHCP będzie przedstawiona przez konfigurowanie zadania z egzaminu praktycznego.
czyli:
<img width="983" height="348" alt="image" src="https://github.com/user-attachments/assets/138e191e-9f9d-419a-954b-9f2dd11f8659" />
pierwsze trzy podpunkty możemy pomimac ponieważ można je swobodnie zrobić przez Quick Seta tak jak w poprzednim przykłądzie a resztę będziemy konfigurować w innej zakładce.


Aby skonfigurować adres Server DHCP należy wejść do zakładki IP 
<img width="116" height="19" alt="image" src="https://github.com/user-attachments/assets/f9ea893a-829d-4f3a-84d6-cf1492df2422" />
Następnie z Dropdowna wybrać opcje 'DHCP Server'
<img width="251" height="525" alt="image" src="https://github.com/user-attachments/assets/d32615bb-72a9-4629-94dc-d77cc6aa311b" />
Menu wygląda następująco
<img width="598" height="377" alt="image" src="https://github.com/user-attachments/assets/91694e2d-9fb5-4b4e-9b3f-40d5517860fc" />
Następnie klikamy guzik DHCP Setup aby rozpocząć konfigurację.
<img width="80" height="24" alt="image" src="https://github.com/user-attachments/assets/71683035-a902-4d3c-be46-8d1a2f9dd9c8" />
W pierwszym okienku wybieramy ether2 ponieważ nasz server DHCP będzie rozdawał adresy IP właśnie na tym interfejscie.
<img width="272" height="173" alt="image" src="https://github.com/user-attachments/assets/4900abe7-3d01-439e-bb60-ba6042c0ab0f" />
Sieć skonfiguruje się automatycznie możemy przejśc dalej 
<img width="272" height="171" alt="image" src="https://github.com/user-attachments/assets/8e0acd29-e6bd-47cf-8e86-526bc63eb8ef" />
Brama domyślna też skonfiguruje się sama, możemy  przejść dalej
<img width="272" height="173" alt="image" src="https://github.com/user-attachments/assets/5712a1e9-6ad6-4349-9e26-c54c8b2e1282" />
W Adresses to Give Out: Tutaj wybieramy właśnie tą pule adresów którą będzie używał nasz server DHCP i z której podłączone do niego komputery mogą brać adresy IP - zmieniamy tutaj domyślne wartości na takie które dostaliśmy w arkuszu czyli 172.16.10.100 ÷ 172.16.10.110
<img width="272" height="170" alt="image" src="https://github.com/user-attachments/assets/f8ae2282-3fbb-426f-bfde-e00a35b99e14" />
W tej zakładce wybieramy Servery DNS które będziemy używać w naszym serverze DHCP - może być napisane w arkuszu ,że servery DNS mają byc inne dla interfejsy WAN i dla interfejsy Servera DHCP ale nie powinno tak być a więc zostawiamy te które ustawilismy.
<img width="272" height="171" alt="image" src="https://github.com/user-attachments/assets/7ca76384-74c4-4726-9155-411dd2a7f6fd" />
Lease Time oznacza ile minut dany komputer ma trzymać adres IP przed pobraniem nowego - w tym przypadku zostawiamy to pole tak jak jest bo nikt nie powiedział ,że mamy je zmienić
<img width="273" height="171" alt="image" src="https://github.com/user-attachments/assets/45d6aea0-190d-45b6-b914-b2a2c499d74b" />
Pomyślnie skonfigurowaliśmy Router!
<img width="191" height="102" alt="image" src="https://github.com/user-attachments/assets/95563bbe-cc20-431e-aca2-c87f2ac37203" />

### Stworzenie Dzierżawy ( Leaase )

aby stworzyć Lease ( zarezerwować jakiś adres IP danemu komputerowi po adresie MAC ) należy:
Wrócić do zakładki DHCP Server , wejśc w Leases.
<img width="593" height="374" alt="image" src="https://github.com/user-attachments/assets/2251a6b9-ebed-423e-b1bc-917f2aa46347" />
Turaj klikamy guzik + i pojawia się nam to okienko.
<img width="377" height="422" alt="image" src="https://github.com/user-attachments/assets/306b9979-e7e6-4948-8ad6-8f9ccc8cc335" />
W tym okienku zmienamy pole Address na adres który chcemy dać komputerowi który go rezerwuje a w pole MAC Address wpisujemy Adres MAC tego komputera który możemy znaleść przez wpisanie na windowsie komendy 'ipconfig /all' w terminalu i znaleznie adresu MAC przypisanego do interfejsu połączonego do Routera lub na Linuxie w terminalu wpisaniem komendy 'ip a' ,która także pokaże nam adres MAC interfejsu połączonego do Routera ,który następnie wpiszemy w nasze pole.

W moim przypadku Adres MAC mojej stacji roboczej widnieje na tym obrazku po wpisaniu komendy 'ipconfig /all' w terminalu Windows
<img width="758" height="310" alt="image" src="https://github.com/user-attachments/assets/223333a1-6bb0-44d4-81f9-f722bfd54fbd" />
Po Wpisaniu Adresu MAC do sekcji MAC Address możemy kliknąć Apply , OK co sprawi ,że zmiany się zapiszą 
<img width="374" height="423" alt="image" src="https://github.com/user-attachments/assets/e1a7fbe7-d8e6-494c-ab83-41b01bc777c7" />

Ethernet adapter Karta-USB:

   IPv4 Address. . . . . . . . . . . : 172.16.10.105(Preferred)
   
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   
Jak widać Server DHCP działa poprawnie 


### Troubleshooting 

Jeśli źle się wpisało Pool adresów do servera DHCP to nie trzeba usuwać całego Serwera DHCP i zaczynać od początku. Wystarczy wejśc do zakłądki IP > Pool
<img width="255" height="523" alt="image" src="https://github.com/user-attachments/assets/2bb6b9db-e03a-47f7-9c97-7c0baa3af6d8" />
a następnie w tej zakłądce klikamy na źle utworzony Pool
<img width="428" height="373" alt="image" src="https://github.com/user-attachments/assets/51002420-7d2b-4d13-be5a-5dec51889ebf" />
i zmieniamy jego zakres i klikamy Apply , OK
<img width="303" height="202" alt="image" src="https://github.com/user-attachments/assets/9217e650-8703-4b99-820b-6984e3e1429d" />


### Konfiguracja Wi-Fi na routerze 

<img width="779" height="412" alt="image" src="https://github.com/user-attachments/assets/0fd3f5e7-33f6-4c4f-94e4-289403f21f7d" />
Aby wytłumaczyć jak skonfigurować Wi-Fi na routerze Mikrotikowym posłużymy się powyższyn przykładem.
<img width="1302" height="269" alt="image" src="https://github.com/user-attachments/assets/fa409749-ace8-42f1-8f9c-3b428b351ec7" />

Najpierw zrobimy Zadanie część zadania, kórą już defakto wiemy jak zrobić. Całą tą część da się skonfigurować za pomocą QuickSeta - lub można zrobić to manualnie co będzie pokazane pod koniec.

<img width="1115" height="598" alt="image" src="https://github.com/user-attachments/assets/0b097896-9687-422d-a0f5-3dee79097af4" />

Jak widać przez to, że użyliśmy quickseta adresy IP dla danych portów stworzyły się automatycznie.

<strong>Teraz możemy przejść do części z konfiguracją Wi-Fi</strong>

Zakładka, która zawiera ustawienia Wi-Fi to czwarta zakładka patrząc od początku 
<img width="136" height="533" alt="image" src="https://github.com/user-attachments/assets/71c60cdf-2a70-4b75-a811-0ae261f3a8e0" />
<img width="126" height="32" alt="image" src="https://github.com/user-attachments/assets/a6f111f6-84f9-45b4-a9d8-349a210def7f" />
<img width="875" height="381" alt="image" src="https://github.com/user-attachments/assets/44a4ee75-18ff-4d69-a3ac-8cf1f9dd9dbb" />

Jak widać wyświetla się nam menu w, którym mamy interfejs 'wlan1', który będziemy konfigurować

<img width="531" height="505" alt="image" src="https://github.com/user-attachments/assets/920dfd9c-c6e1-4774-9aa3-fa8b658b9dbe" />

Po kliknięciu w intefejs 'wlan1' pokaże się nam menu w, którym jedyną ważną zakładką, której będziemy używać będzie zakładka 'Wireless' - to właśnie tutaj możemy zmienić naszę SSID, Kanał, Security Profile, Kraj.

<img width="872" height="378" alt="image" src="https://github.com/user-attachments/assets/38793098-e170-4527-9c5a-a742d1184864" />
Drugą zakłądką, która będzie nas interesowac jest zakładka 'Security Profiles' w, której będziemy konfigurować metode szyfrowania naszej sieci oraz 































