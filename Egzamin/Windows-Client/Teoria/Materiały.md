# Teoria

Windows nie jest teoretycznie trudny, ponieważ nie musimy na nim zapamiętywać rzeczy na pamięć. Wystarczy, że wiemy jak się do nich doklikać. Oczywiście nadal trzeba umieć komendy w terminalu Windowsa ale jest ich o wiele mniej niż na linuxie.

Bez dwóch zdań najgorzą rzeczą w Windowsie jest to, że wszystkie funkcję systemu są tak rozproszone, że truno jest znaleść to czego szukamy jeśli nie mamy wstępnej informacji gdzie to może się znajdować.

Zagadnienia:
- Terminal w windowsie
- usługi i zakładki .msc
- Windows jako client, któremu są świadczone usługi ( Windows Server ) 
- Odpowiedzi na pytania z egzaminów

## Komendy w Windowsie ( tak z 30% zrobione do dokończenia )

```

--- Przechodzenie przez strukturę folderów ---
cls - czyści konsole 
exit - wychodzi z terminala 
color - zmienia kolor tekstu / tyłu konsoli

mkdir harry - tworzy folder 'harry'
rmdir harry - usuwa folder 'harry'
md harry - Tworzy folder 'harry'
rename harry harry3 - zmienia nazwe folderu 'harry' na 'harry3'
type harry4.txt - wyświetla zawartośc pliku tekstowego
type nul > harry_123.txt - tworzy plik tekstowy o nazwie 'harry_123.txt'
del harry4.txt - usuwa plik harry4.txt
copy harry1 harry2/ - kopiuje folder harry1 do folderu harry2
xcopy harry/* harry123/ -e -y    -  kopiuje wszystkie pliki i foldery z harry do harry123 (-e: kopiuje wszystko, -y: nie pyta o potwierdzenie)
move harry1/harry2.txt harry2/ - przeniesie plik 'harry2.txt' znajdujący się w folderze 'harry1' do folderu 'harry2'
tree - pokazuje obecną strukturę folderów w formie drzewa

```

<img width="234" height="86" alt="image" src="https://github.com/user-attachments/assets/77d3fea6-facf-49a1-9063-d2b18bfc0927" />

```

attrib +h tajny_harry.txt - sprawia, że plik tajny_harry.txt znika z widoku ( staje się hidden ) - polecenie attrib jest w stanie zmieniać atrybuty danego pliku.
attrib /? - pokazuje wszystkie atrybuty jakie możemy dać plikom np. ( +r sprawia, że plik jest read-only albo np. +s sprawia, że plik jest systemowy )
---                                          ---

--- Tworzenie, modyfikowanie użytkowników ---

net user - Wypisuje listę kont 
net user harry /add - doda użytkownika o nazwie harry
net user harry haslo123 /add - doda użytkownika o nazwie harry z hasłem haslo123
net user harry * /add - doda użytkownika o nazwie harry i poprosi o wpisanie dla niego hasła ( wyświetli monit )
net user harry /del - usunie użytkownika o nazwie harry

net localgroup Miasto_Harrych /add - doda grupę o nazwię 'Miasto_Harrych'
net localgroup Miasto_Harrych /del - usunię grupę o nazwię 'Miasto_Harrych'
net localgroup "Miasto_Harrych" harry123 /add - doda użytkownika 'harry123' do grupy 'Miasto_Harrych'
net localgroup "Miasto_Harrych" harry123 /del - usuwa użytkownika 'harry123' z grupy 'Miasto_Harrych'
net localgroup "Miasto_Harrych" /comment:"tutaj żyje harry" - Dodaje opis/komentarz do grupy
net localgroup "Miasto_Harrych" - Wyświetla listę wszystkich członków grupy


net user harry *                    - Zmienia hasło (wpisujesz je niewidocznie)
net user harry /active:no           - Blokuje konto (użytkownik nie może wejść)
net user harry /active:yes          - Odblokowuje konto
net user harry /passwordchg:no      - Zabrania użytkownikowi zmiany hasła
net user harry /passwordchg:yes     - Pozwala użytkownikowi na zmianę hasła
net user harry /passwordreq:yes     - Wymusza, aby konto musiało mieć hasło
net user harry /expires:18/05/2026  - Konto wygaśnie i "zniknie" (stanie się nieaktywne) w dacie, która jest wyżej ustalona
net user harry /times:Pn-Pt,08-16   - Pozwala na logowanie tylko w dni robocze 8-16
net user harry /times:all           - Usuwa ograniczenia godzin logowania
net user harry /comment:"jest słodki" - Dodaje krótki opis do konta
net user harry /fullname:"H.Potter" - Ustawia pełną nazwę wyświetlaną
net user harry                      - Wyświetla wszystkie szczegóły o harry'm



















systeminfo - wyświetla podstawowe informacje o zainstalowanym systemie, poprawkach, wyświetla nazwę hosta, strefę czasową oraz częściową konfigurację karty sieciowej ipconfig - wyświetla aktualną konfigurację karty sieciowej
getmac - wyświetla adresy fizyczne MAC zainstalowanych kart sieciowych
netstat - wyświetla listę aktualnych połączeń sieciowych
ping onet.pl - sprawdza połączenie z daną stroną
calc- kalkulator
notepad - uruchamia notatnik
time-pokazuje i ustawia czas
shutdown - wyłącza komputer
wusa - zarządza aktualizacjami Windows
chkdisk - sprawdza dysk w poszukiwaniu błędów
winsat disk-seg-read/write-drive C - testuje prędkość dysku C pod względem odczytu/zapisu
ver-pokazuje wersję systemu operacyjnego
perfmon - służy do uruchamiania "Monitora wydajności"
vol - pokazuje nazwę dysku
history - wyświetla listę zapisanych wcześniej komend
color - ustawia kolor konsoli
tasklist - wyświetla listę procesu
defrag - służy do defragmentacji dysku (uruchamia się go z Diskpart'a)
mode - służy do konfiguracji urządzeń systemowych
sc - otwiera zarządzanie usługami
winh132 - aplikacja otwiera pliki pomocy
log off - wylogowuje danego użytkownika
mem - wyświetla informacje dotyczące pamięci RAM
format-formatowanie dysku
sfc - skanuje pliki systemowe i wyświetla te błędne nslookup - diagnostyka DNS


-------DISKPART-------
DISKPART jest narzędziem służącym do zarządzania Dyskami, partycjami, voluminami 

DISKPART - wchodzi do diskparta
? - wyświetla dostępne komendy
list disk - wyświetla wszystkie dostepne dyski
```
<img width="435" height="91" alt="image" src="https://github.com/user-attachments/assets/ecae4b7b-29b0-42fa-bf9f-cbccedc7cd33" />
```
select disk 0 - wybiera dysk 0 ( jako ten, którym na, którym chcemy operować )

PRZYKŁAD:
DISKPART> select disk 0                                                                                                                  Disk 0 is now the selected disk.

list partition - wyświetla partycje
```
<img width="413" height="131" alt="image" src="https://github.com/user-attachments/assets/a2b35c08-9eaa-4a9a-b4e1-8085d071c6ca" />
```
select partition 4 - wybiera partycje czwartą ( jako tą na, której chcemy operować )

create partition primary size=50000 - tworzy partycje mającą 50GB
delete partition 4 - usuwa partycje czwartą
format fs=ntfs quick label="MojeDane" - formatuje partycje / volumin
extend size=10000 - powiększa partycję o wydzieloną wielkość ( w tym przypadku o 10GB )
shrink desired=5000 - zmniejsza partycję o 50GB
assign letter=G - przypisuje litere partycji
```
## Usugi, Przystawki w Windowsie

## Windows jako Klient

## Zadania praktyczne.






