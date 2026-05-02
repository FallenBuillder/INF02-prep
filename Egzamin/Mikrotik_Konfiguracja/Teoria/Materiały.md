# Teoria 

Na egzaminie Praktycznym INF02 router ( jak i switch ) pojawiają się w każdym arkuszu jaki napotkamy. Czasami zadania z nim związane są dosyć łatwe a czasami trochę bardziej bogmatwane

W tej sekcji skupimy się na routerze Mikrotikowym i metodami dzięki którymi możemy go skonfigurować przez GUI 
> Konfiguracja Mikrotika przez CLI jest bardzo trudna i wymagałaby dużej znajomości dokumentacji a więc nie ma jej tutaj.

Zagadnienia 

- jak się połączyć ?
- Resetowanie Routera
- Podstawowe ustawienia konfiguracjne w każdym arkuszu
- Konfiguracja Wszystkiego przez Quick Seta ( łatwa metoda zdająca się tylko jak serwer DHCP jest wyłączony )
- Konfiguracja serwera DHCP
- Konfiguracja Wi-FI
- Konfiguracja Router-on-a-stick - zarządzanie trunkami
  

### GUI - jak połączyć się z Routerem 
Aby połączyć się z routerem Mikrotikowym potrzebny jest nam program WinBox. Program ten będzie na egzaminie albo już zainstalowany na naszym komputerze albo będziemy musieli go doinstalować uruchamiając instalator który znajduję się na Pendrivie USB opisanym PROGRAMY.
WinBox do wykrywania urządzeń nie używa protokołu IP, lecz protokołów warstwy drugiej (L2), takich jak MNDP lub CDP (Cisco Discovery Protocol). Router rozsyła specjalne ramki rozgłoszeniowe (broadcast), które WinBox potrafi przechwycić, o ile jesteś w tej samej sieci fizycznej - oznacza to ,że nie musimy zmieniać ustawień kart sieciowych aby się do niego dostać.


