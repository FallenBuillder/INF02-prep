# Sieci
W niemal każdym egzaminie zawodowym INF02 znajduję się pare zadań odwołujących się do skonfigurowania interfejsów sieciowych urządzeń takich jak servery lub routery, lecz sama umiejętnośc skonfigurowania tego typu urządzeń nie jest wystarczająca. W tej sekcji będą omawiane definicje , obliczenia , zasady których znajamość pomoże nam rozwiązywyć napotkane przez nas problemy które napotkamu podczas egzaminu oraz pomoże nam zrozumiec co naprawdę robimy podczas konfiguracji, eksploitacji tego typu urządzeń.

ta sekcja jest podzielona na pare tematów gdzie każdy z nich będzie odwoływał się do innego urządzenia sieciowego oraz definicji z nim związanych.

na egzaminie zawodowym urządzenie te są podzielone na:
- Servery
- Klienci *inaczej hosty lub Stacje robocze
- Drukarki
- Routery
- Przełączniki *inaczej switche

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



