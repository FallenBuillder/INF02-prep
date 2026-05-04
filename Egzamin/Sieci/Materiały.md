# Sieci
W niemal każdym egzaminie zawodowym INF02 znajduję się pare zadań odwołujących się do skonfigurowania interfejsów sieciowych urządzeń takich jak servery lub routery, lecz sama umiejętnośc skonfigurowania tego typu urządzeń nie jest wystarczająca. W tej sekcji będą omawiane definicje , obliczenia , zasady których znajamość pomoże nam rozwiązywyć napotkane przez nas problemy które napotkamu podczas egzaminu oraz pomoże nam zrozumiec co naprawdę robimy podczas konfiguracji, eksploitacji tego typu urządzeń.

ta sekcja jest podzielona na pare tematów gdzie każdy z nich będzie odwoływał się do innego urządzenia sieciowego oraz definicji z nim związanych.

na egzaminie zawodowym urządzenie te są podzielone na:
- Servery
- Klienci *hosty lub Stacje robocze
- Drukarki
- Routery
- Przełączniki *switche

każde z wyżej wymienionych urządzeń ma swoję zastosowania i pełni inną role na egzaminie np. 
- Servery mają za zadanie hostować usługi klientom aby klienci mieli dostęp do określonych przez servery zasobów, obiektów lub usług.
- Klienci ( hosty ) służą jako urządzenia końcowe ,które w kontekscie egzaminu będą miały na celu pozyskiwać usługi od serverów.
- Drukarki na egzaminie służą tylko jako zasoby których jedynym celem jest to aby były przez nas wyeksploitowane poprzez np. wydrukowanie strony testowej przez klienta
- Routery na egzaminie głównie służą jako Access pointy które dają nam intenet przez wifi lub jako servery DHCP, które sprawiają, że klienci jak i servery dostają adresy IP
- Switche pomagają połączyć wszystkie urządzenia razem w jedną całość używająć VLANów, trunków.

Ważną Umiejętnością więc jest wiedza co robią poszczególne elementy, które związane są z konfigurowaniem wyżej wymienionych urządzeń.

> UWAGA: materiały, które są tutaj przedstawione mają na celu tylko powtórke z sieci do egzaminu <strong>PRAKTYCZNEGO</strong> bardziej rozwinięty i zaawansowane wyjaśnienie poniższych tematów będzie wytłumaczone w osobnym repozytorium przygotowywującym nas do egzaminy Teoretycznego 

### Czym jest Sieć ?
Zanim przejdziemy do omówienia głównego wątku musimy się cofnąć i odpowiedzieć na pytanie co umożliwia nam sieć kpmputerowa ? - według [definicji](https://pl.wikipedia.org/wiki/Sie%C4%87_komputerowa) <em>'sieć umożliwia łatwy i szybki dostęp do – jak również otwiera techniczną możliwość tworzenia i korzystania ze – wspólnych zasobów informacji i zasobów danych.'</em>

Oznacza to, głównym zadaniem, Celem Sieci komputerowej jest <strong>wymiana informacji</strong> i sprawienie ,że urządzenia do niej należące mogą się z sobą komunikować.

### Jak urządzenia komunikują się z sobą w sieci ?
Aby zrozumieć jak urządzenia się z sobą komunikują musimy najpierw zrozumieć parę definicni związanych z sieciami.

<strong>adres IP</strong> - jest to liczbowy identyfikator nadawany interfejsowi sieciowemu bądź całej sieci komputerowej w protokole IP, służący identyfikacji elementów sieci w warstwie trzeciej modelu OSI – w obrębie sieci lokalnej oraz poza nią (tzw. adres publiczny).
jego najpopularniejsza wersja czyli wersja 4 ( IPv4 ) jest obecnie najbardziej powszechnie używana. 
adres IPv4 składa się z 4 oktetów liczb od 0-255 zapisywanych w systemie dziesiętnym.
np. 192.168.0.1 lub 244.31.172.12

<strong>Maska podsieci</strong> - jest liczbą służącą do wyodrębnienia w adresie IP części będącej adresem podsieci i części, która jest adresem hosta w tej podsieci. ( więcej o niej w części o dzieleniu sieci na podsieci )

<strong>Brama domyślna</strong> - oznacza router, do którego komputery sieci lokalnej mają wysyłać pakiety, o ile nie powinny być one kierowane w sieć lokalną lub do innych, znanych im routerów.

<strong>DNS</strong> - (Domain Name System ) - hierarchiczny rozproszony system nazw, który umożliwia identyfikację usług i zasobów internetowych, pozwalając urządzeniom użytkowników końcowych na korzystanie z usług routingu internetowego i usług łączności w celu dotarcia do tych usług i zasobów
jego głownym celem jest tłumaczenie zwięzłych i trudnych do zapamiętania adresów IP na domeny(i odwrotnie), które są łatwo przez nas odczytywane, używane 

<strong>LAN</strong> - (Local Area Network) - sieć komputerowa łącząca komputery na określonym obszarze

<strong>WAN</strong> - (Wide Area Network) - – sieć komputerowa znajdująca się na obszarze wykraczającym poza miasto, kraj lub kontynent

### Podsumowując

czyli w skrócie aders IP to jest nasz identyfikator, który pozwala komunikowac się z innymi urządzeniami, maska podsieci to jest nasz wyznacznik do której sieci należym, brama domyślna to jest router albo urządzenie do którego chcemy rozmawiać aby nasza informacja poszła dalej w świat do innego urządzenia , DNS jest usługą która pozwala nam tłumaczyć nazwy domenowe na adresy IP i odwrotnie , LAN i WAN to są pojęcia określające złożonośc sieci i gdzie ta sieć się znajduje w tym przypadku LAN jest naszą siecią lokalną czyli czymś małym a WAN jest już większą siecią która łączy wiele innych sieci pozwalając na komunikacje między nimi.

***

Znamy już podstawowe pojęcia związane z sieciami a resztę z nich poznamy w następnych tematach odwoływujących się już do specyfistycznych urządzeń i definicji, które są z nimi związane 


## Servery i definicje z nimi związane 
Mamy wiele różnych typów serverów i omówienie wszystkich zajeło by bardzo długi czas a więc skupimy się narazie na tym jakie usługi świadczą servery Windows , Linux ( Ubuntu ) i co one faktycznie robią.
> Nie będziemy wchodzić w szczegóły w jaki sposób urządzenia wykrywają dane usługi lub jakie pakiety , jakiej wielkości i jakie zasady są związane z ich transmisją ponieważ celem jest tutaj zrozumienie czym dana rzecz jest a następnie można rozwinąć swoją wiedze bazując na innych działach w których dana usługa jest konfigurowana lub w nadchodzącym repozytorium z teorii

<strong>Server DHCP</strong> - server DHCP służy jako usługa, której zadaniem jest rozdawanie adresów IP komputerom, które są podłączone do tej samej sieci co on i mają ustawione w swoich kartach sieciowych pozyskiwanie adresów przez właśnie przez ten server. 
Server DHCP posiada parę ustawień mianowicie można w nim ustawić:
- Pula adresów - to ustawienie mówi serverowi ile i jakie adresy IP ma rozdawać swoim klientom
- Lease time ( czas dzierżawy ) - to ustawienie oznacza ilość czasu, który ma upłynąć przed tym jak klient ma dostać nowy adres
- Rezerwacja adresów - to ustawienie pozwala serverowi zarezerwowac konkretny adres IP dla konkretnej karty sieciowej urządzenia końcowego ,które chce otrzymać od niego adres ( dostanie zawsze ten sam )

<trong>Routing</strong> - usługa routingu oznacza ,że server będzie przekazywał naszę dane dalej w świat abyśmy mogli połączyć sięz urządzeniami w innych sieciach.S

<strong>Server DNS</strong> - zadaniem servera DNS jest to aby tłumaczyć nazwy domenowe na adresy IP i odwrotnie bardziej szczegółowe wytłumaczenie jak to robi i na jakiej podstawie można znaleść w folderze "Windows-Server" , "Linux-Server" - gdzie poszczególne rekordy oraz poszczególne parametry , ustawienia tego servera są wytłumaczone

<strong>Server WWW</strong> - zadaniem servera WWW jest to aby hostować stronę internetową z, której może następnie korzystać użytkownik jeśli wpiszę jej adres IP w przeglądarce 
Server WWW posiada ustawienia takie jak:
- Port - na jakim porcie na danym serverze ma być wystwawiona jaka strona ( może być wystawione wiele stron na jednym adresie IP ale pod innym portem )
> o portach można myśleć jak o oknach w domu , im więcej okien jest otwarte to tym bardziej taki dom jest 'otwarty na świat' bo można przez te porty dotrzeć do różnych usług ( każdy port ma swój numer i zastosowanie i jest przeznaczony do danej usługi np. 67 DHCP albo 443 HTTPS - więcej o portach będzie powiadziane w innej sekcji )
- Plik domyślny - oznacza jaką ma może mieć główny plik .html strony internetowej, który ładuje się jako pierwszy przy ładowaniu strony
- Miejsce w, którym znajduję się plik domyślny - określa gdzie ma znajdować się plik domyślny.

<strong>Server SAMBA</strong> - Server SAMBA to server, którego głównym celem jest udostępnianie folderów w sieci lokalnej lub w internecie do, których potem użytkownicy końcowi mogą zapisywac dane w zależności od ich uprawnień do danego folderu. 

<strong>Server SSH</strong> - Server SSH pozwala nam na zdalne szyfrowane połączenie się z serverem, który go hostuje aby następnie można było go zdalnie skonfigurować,

<strong>Server FTP</strong> - Server FTP pozwala nam na pobieranie oraz uploadowanie danych. Działa na podstawie uprawinień, posiada konta do, których można się zalogować i można z nich wykonywać operacje na plikach. 

<strong>Server Wydruku</strong> - Server wyrduku pozwala nam udostępniać, zarządzać drukarką w sieci tak aby można było przeznaczyć do niej prawa innym użytkownikom w domenie active directory 

## Klienci - co potzebują i jak działają ?

Każde urządzenie jest z definicji klientem ponieważ każde urządzenie wysyła rządanie o jakieś dane a następnie przetwarza odpowiedzi, które dostało z tych właśnie rządań. 

Aby klient ( czyli na egzaminie komputer z Windowsem 10 albo z Ubuntu Desktopem ) mógł komunikować się z serverem albo jakiegoś typu urządzeniem sieciowym.
> [!CAUTION]
> <strong><em>musi być z tym urządzeniem w tej samej podsieci </strong></em>
Jeśli Klient, który jest podłączony do switcha będzie chciał rozmawiać z Serverem, który jest także podłączony do tego same switcha ale Server jest w INNEJ podsieci niż klient to te dwa urządzenia się z sobą nie będą w stanie komunikować.

Wyjątek pojawia się wtedy kiedy podsieci są połączone routerem ,wtedy router może tak routować pakiety przez warstę trzecią ,że komputery się dogadają. ale jeśli urządzenie są w innych podsieciach i jedynym medium połączenia jest warstwa druga ( łącza danych ) połączenia nie będzie 


### Obliczanie podsieci 

Jak już wcześniej wspomniałem aby urządzenia mogły się z sobą komunikować ,muszą być z sobą w tej samej podsieci.

żeby zrozumieć jak działają podsieci musimy najpierw się nauczyć jak się je oblicza.

załóżmy, że mamy do podzielenia sieć 192.168.1.0/24 i chcemy ją podzielić na 4 podsieci.

pierwszym krokiem, który powinniśmy wykonać jest wypisanie informacji, które dostaliśmy czyli:
- ma być 4 podsieci
- adres sieci to 192.168.1.0
- maska podsieci ( przed podziałem ) to /24 czyli 255.255.255.0

Naszym zadaniem będzie policzenie
- nowej maski podsieci
- liczby hostów w każdej podsieci
- adresów sieciowych , rozgłoszeniowych każdej podsieci
- zakresów każdej podsieci


### krok1. obliczenie maski podsieci

Aby obliczyć maskę podsieci należy znaleść <strong>nie mniejsza</strong> potęge dwójki, nie większą od liczby podsieci które finalie chcemy mieć

Korzystamy z wzoru      <strong> 2^n >= 4 </strong>         

metodą prób i błędów dochodzimy do wniosku, że aby równanie było prawdziwe największa liczba jaką możemy podstawić to 2 bo:
2^2 >= 4 
4 >= 4 - co jest prawdą

teraz dodajemy liczbę bitów, która nam wyszła w równaniu do maski podsieci czyli:
24 + 2 = 26

Co oznacza ,że nasza maska podsieci to będzie /26

### krok2. obliczenie liczby hostów, liczby użytecznych hostów w każdej podsieci.

teraz jak mamy już naszą maskę podsieci to konwertujemy ją na wartość binarną.

/26 = 11111111 11111111 11111111 11000000

> każdy osobny oktet czyli np. 11111111 jest osobną liczbą, każdy oktet jest liczony osobno.

jeśli w danym oktecie jest jedynka na jednej z 8 pozycji to zamieniamy tą jedynkę na potęgę dwójki bazując na tym gdzie ta jedynka się znajduję. Dla przykładu:

***
<img width="331" height="53" alt="image" src="https://github.com/user-attachments/assets/d9336375-1cda-4d41-a1dc-7b3787dbc8dc" />
***

następnym krokiem jest spotęgowanie dwójek tylko tam gdzie nad nimi jest jedynka i dodanie tej wartości do siebie.

2^7 + 2^6 = 128 + 64 = 192

teraz odejmujemy wartość którą dostaliśmy od liczby 256 i dostaniemy liczbę hostów na każdą podsieć

256 - 192 = 64 

żeby obliczyć faktyczną liczbę hostów dla każdej z podsieci wystarczy usunąć od wartości, którą otrzymaliśmy 2 ( ponieważ odejmujemy adres sieciowy , adres rozgłoszeniowy ) 

czyli:

64 - 2 = 62

czyli każda podsieć będzie miała 62 hostów.


### krok3. obliczenie zakresów , podsieci

Następnym krokiem będzie wyznaczenie adresów sieciowych , adresów rozgłoszeniowych i zakresów 

adres sieciowy - jest pierwszym adresem w sieci.
adres rozgłoszeniowy - jest ostatnim adresem w sieci.
zakresy - zakresy podsieci są zakresami, które mówią nam od jakiego do jakiego adresu IP jest nowa sieć  

Oznacza to ,że podzielenie na podsieci będzie wyglądało następująco

<img width="1089" height="396" alt="image" src="https://github.com/user-attachments/assets/29dbcd28-16cd-4585-a52a-59ff90733f25" />

Po co dzielimy sieci na podsieci ? - sieci dzielimy na mniejsze części z względów Bezpieczeństwa , wydajności , porządku aby np. dany wydział w firmie był w osobnej podsieci.

Czy urządzenie w innych podsieciach mogą sie komunikować ? - Tak, mogą ale tylko wtedy jak te podsieci przechodzą przez router który dzieli je na częsci 








## Drukarki 

Drukarki na egzaminach INF02 pojawiają się relatywnie często i jak już się pojawiają to głównie razem z Serverem Wydruku , Active Directory na windows Serverze. 

Myśle ,że każdy wie co to jest drukarka i tego nie trzeba wytłumaczać, jedyną rzeczą, którą trzeba doprecyzować jest to, co się wiąże z faktem, że mamy drukarke na egzaminie.

Kiedy dostajemy drukarkę na egzaminie to dostajemy jej Adres IP ponieważ bez niego nie moglibyśmy jej wykryć po adresie IP kiedy próbujemy ją znaleść podczas konfiguracji servera wydruku na windows serverze.

<img width="761" height="342" alt="image" src="https://github.com/user-attachments/assets/7343df6a-f816-47a9-98c6-5a4a0b56806f" />

Jak widać na tym fragmencie z egzaminu drukarke będziemy szukać po adresie IP, sterowniki do drukarki powinny być już wgrane w Active Directory jako jedne z tych domyślnych aby nie trzeba było ich pobierać.

Drukarka wydaję się być trochę straszna kiedy dostajemy ją na egzaminie ale tak naprawdę nie jest dużym problemem kiedy zrozumie się działanie servera wydruku ( folder 'Windows_Server' )

### Routery

Routery to urządzenia sieciowe, które pozwalają nam na dostęp do internetu i rozmawianie z innymi sieciami, podsieciami czy to w internecie czy to w naszej sieci lokalnej. Pozatym dzięki routerom ( dokładnie to Access Pointom wbudowanym w Routery ) jesteśmy też w stanie mieć dostęp do Wi-Fi

Na egzaminie praktycznym podczas konfiguracji Routera trzeba zrozumieć parę pojęć, które będą nam potrzebne aby zrozumieć co konfigurujemy i co dane ustawienie robi:


Najważniejszym zagadnieniem powiązanym z routerami są dwie rzeczy, które zostały już wcześniej omówione czyli WAN, LAN. W kontekscie routerów WANem będzie 'Internet' czyli miejsce z, którego powinniśmy dostawać internet. Na egzaminie interfejsowi WAN są przypisywane przykładowe wartości ponieważ nie możemy się faktycznie na nim połączyć do internetu. 
<img width="1243" height="773" alt="image" src="https://github.com/user-attachments/assets/6cf4bf23-6bd9-48e8-be9f-a78af4e177a4" />
Na powyższym przykładzie jest przedstawione przykładowe zadanie z jednego z arkuszy INF02

W normalnej konfiguracji gdzie docelowo mamy mieć dostęp do internetu adres IP dla interfejsu WAN byłby statyczny albo byłby dynamiczny ( zależy od umowy z naszym ISP )
<br>
Jeśli router jest częścią większej sieci to adresem IP przypisanym do interfejsu WAN byłby adres w tej samej podsieci jak intefejs LAN routera, który jest szczebel wyżej nad omawianym routerze.
<br> 

Brama domyslna intefejsu WAN w tym zadaniu oznacza adres IP konkretnego interfejsu LAN routera, który jest routerem który konfigurujemy. 

Servery DNS w tym kontekscie oznaczają servery DNS z, których nasz router będzie pobierał adresy IP.

<br>
<br>

Wzmianka o 'Adresie IP intefejsu LAN' odwołuje się do przypisania jakiemukolwiek portowi na routerze ( w quicksecie defaultowo drugiemu ) adresu IP oraz maskę podsieci taką aby ten intefejs routera był w tej samej sieci co inne urządzenia żeby mógł się z nimi komunikować.

> reszta definicji, pojęć odwołujących się do routera są wytłumaczone w folderze 'Mikrotik_Konfiguracja'


### Switche

Switche są najbardziej podstawowymi urządzeniami na egzaminie zawodowym. Ich jedynym celem jest to aby połączyć wszystkie urządzenia w sieci takie jak Hosty lub servery tak aby mogły się z sobą komunikować i żeby nie trzeba było ich połączać bezpośrednio do siebie co by było nie efektywne. Nie ma w nim za dużo konfiguracji a jak już jest to nie jest zbytnio trudna.
Switch zawiera pare konfigurowalnych ustawień, które pojawiają się na egzaminie. 
- Adres IP, brama domyślna, Maska Podsieci - kiedy musimy skonfigurować te ustawienia na naszym Switchu oznacza to, że ustawiamy je tylko do tego aby switch był zdalnie zarządzalny przez SSH lub SNMP. Naszczęście na egzaminie nie musimy zdalnie zarządzać Switchem korzystając z tych usług i musimy tylko wiedzieć jak sprawić, że switch będzie je oferował przez to, że ma adres IP
- VLANy - głównym zadaniem VLANów na egzaminie zawodowym jest to aby rozdzielić sieć na parę części tak aby jedne urządzenia nie moglby się komunikować z drugimi. Zrobione to jest przez przypisywanie poszczególnych intefejsów do określonego VLANa co sprawia ,że jeśli dwa urzązenie nie są w jednym VLANie - nie mogą się z sobą komunikować
- Trunki (porty trunk) tworzy się, aby przesyłać ruch z wielu różnych sieci wirtualnych (VLAN) przez jeden fizyczny kabel łączący dwa urządzenia sieciowe. Służą one do oszczędzania portów i okablowania, eliminując konieczność prowadzenia osobnego przewodu dla każdego VLAN-u z osobna




















































































