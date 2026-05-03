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


### Podstawy Sieci
Zanim przejdziemy do omówienia głównego wątku musimy się cofnąć i odpowiedzieć na pytanie co umożliwia nam sieć kpmputerowa ? - według [definicji](https://pl.wikipedia.org/wiki/Sie%C4%87_komputerowa) <em>'sieć umożliwia łatwy i szybki dostęp do – jak również otwiera techniczną możliwość tworzenia i korzystania ze – wspólnych zasobów informacji i zasobów danych.'</em>

