# Teoria 

Na egzaminie Praktycznym INF02 router ( jak i switch ) pojawiają się w każdym arkuszu jaki napotkamy. Czasami zadania z nim związane są dosyć łatwe a czasami trochę bardziej bogmatwane

W tej sekcji skupimy się na routerze Mikrotikowym i metodami dzięki którymi możemy go skonfigurować przez GUI 
> Konfiguracja Mikrotika przez CLI jest bardzo trudna i wymagałaby dużej znajomości dokumentacji a więc nie ma jej tutaj.

Zagadnienia 

- jak się połączyć ? && Resetowanie Routera
- Podstawowe ustawienia konfiguracjne w każdym arkuszu
- Konfiguracja Wszystkiego przez Quick Seta ( łatwa metoda zdająca się tylko jak serwer DHCP jest wyłączony )
- Konfiguracja serwera DHCP
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
Następnie należy włączyć program WinBox w wersji 


