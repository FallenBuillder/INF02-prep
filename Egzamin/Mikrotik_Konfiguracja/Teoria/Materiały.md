# Teoria 

Na egzaminie Praktycznym INF02 router ( jak i switch ) pojawiają się w każdym arkuszu jaki napotkamy. Czasami zadania z nim związane są dosyć łatwe a czasami trochę bardziej bogmatwane

W tej sekcji skupimy się na routerze Mikrotikowym i metodami dzięki którymi możemy go skonfigurować przez GUI 
> Konfiguracja Mikrotika przez CLI jest bardzo trudna i wymagałaby dużej znajomości dokumentacji a więc nie ma jej tutaj.

Zagadnienia 

- jak się połączyć ? && Resetowanie Routera
- Podstawowy przykład konfiguracji na podstawie najprostszego egzaminu
- Konfiguracja Wszystkiego przez Quick Seta ( łatwa metoda zdająca się tylko jak serwer DHCP jest wyłączony )
- Konfiguracja serwera DHCP
- Podstawy Sieci
- Konfiguracja Wi-FI
- Konfiguracja Router-on-a-stick - zarządzanie trunkami
  

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




















