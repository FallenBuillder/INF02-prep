# Teoria

Windows nie jest teoretycznie trudny, ponieważ nie musimy na nim zapamiętywać rzeczy na pamięć. Wystarczy, że wiemy jak się do nich doklikać. Oczywiście nadal trzeba umieć komendy w terminalu Windowsa ale jest ich o wiele mniej niż na linuxie.

Bez dwóch zdań najgorzą rzeczą w Windowsie jest to, że wszystkie funkcję systemu są tak rozproszone, że truno jest znaleść to czego szukamy jeśli nie mamy wstępnej informacji gdzie to może się znajdować.

Zagadnienia:
- Terminal w windowsie
- usługi i zakładki .msc
- Programy na Windowsie
- Windows jako client, któremu są świadczone usługi ( Windows Server )
- Odpowiedzi na pytania z egzaminów

## Komendy w Windowsie ( tak z 30% zrobione do dokończenia )

```
UWAGA:

Za wszystkimi komendami można wpisać /? aby uzyskać o nich pomoc.

--- Przechodzenie przez strukturę folderów ---
cls                                               - czyści konsole 
exit                                             - wychodzi z terminala 
color                                            - zmienia kolor tekstu / tyłu konsoli

mkdir harry                                      - tworzy folder 'harry'
mkdir -p Harry/Harry2/Harry3/Harry4              - tworzy strukturę folderów
rmdir harry                                      - usuwa folder 'harry'
md harry                                         - Tworzy folder 'harry'
rename harry harry3                              - zmienia nazwe folderu 'harry' na 'harry3'
type harry4.txt                                  - wyświetla zawartośc pliku tekstowego
type nul > harry_123.txt                         - tworzy plik tekstowy o nazwie 'harry_123.txt'
del harry4.txt                                   - usuwa plik harry4.txt
copy harry1 harry2/                              - kopiuje folder harry1 do folderu harry2
xcopy harry/* harry123/ -e -y                    -  kopiuje wszystkie pliki i foldery z harry do harry123 (-e: kopiuje wszystko, -y: nie pyta o potwierdzenie)
move harry1/harry2.txt harry2/                   - przeniesie plik 'harry2.txt' znajdujący się w folderze 'harry1' do folderu 'harry2'
tree                                             - pokazuje obecną strukturę folderów w formie drzewa
icacls "plik_harrowy.txt" /grant Harry:(OI)(CI)F - nadaje uprawnienia plikom/folderom

```

<img width="234" height="86" alt="image" src="https://github.com/user-attachments/assets/77d3fea6-facf-49a1-9063-d2b18bfc0927" />

> pokazało by pełną scieżke gdzie dokładnie znajduję się plik ale się ucieło.


```

attrib +h tajny_harry.txt - sprawia, że plik tajny_harry.txt znika z widoku ( staje się hidden ) - polecenie attrib jest w stanie zmieniać atrybuty danego pliku.
attrib /? - pokazuje wszystkie atrybuty jakie możemy dać plikom np. ( +r sprawia, że plik jest read-only albo np. +s sprawia, że plik jest systemowy )
---                                          ---

--- Tworzenie, modyfikowanie użytkowników ---

net user - Wypisuje listę kont 
net user harry /add            - doda użytkownika o nazwie harry
net user harry haslo123 /add   - doda użytkownika o nazwie harry z hasłem haslo123
net user harry * /add          - doda użytkownika o nazwie harry i poprosi o wpisanie dla niego hasła ( wyświetli monit )
net user harry /del            - usunie użytkownika o nazwie harry

net localgroup Miasto_Harrych /add                - doda grupę o nazwię 'Miasto_Harrych'
net localgroup Miasto_Harrych /del                - usunię grupę o nazwię 'Miasto_Harrych'
net localgroup "Miasto_Harrych" harry123 /add     - doda użytkownika 'harry123' do grupy 'Miasto_Harrych'
net localgroup "Miasto_Harrych" harry123 /del     - usuwa użytkownika 'harry123' z grupy 'Miasto_Harrych'
net localgroup "Miasto_Harrych" /comment:"tutaj żyje harry" - Dodaje opis/komentarz do grupy
net localgroup "Miasto_Harrych"                   - Wyświetla listę wszystkich członków grupy


net user harry *                    - Zmienia hasło (wpisujesz je niewidocznie)
net user harry /active:no           - Blokuje konto (użytkownik nie może wejść)
net user harry /active:yes          - Odblokowuje konto
net user harry /passwordchg:no      - Zabrania użytkownikowi zmiany hasła
net user harry /passwordchg:yes     - Pozwala użytkownikowi na zmianę hasła
net user harry /logonpasswordchg:yes - Wymusza zmianę hasła przy następnym logowaniu 
net user harry /passwordreq:yes     - Wymusza, aby konto musiało mieć hasło
net user harry /expires:18/05/2026  - Konto wygaśnie i "zniknie" (stanie się nieaktywne) w dacie, która jest wyżej ustalona
net user harry /times:Pn-Pt,08-16   - Pozwala na logowanie tylko w dni robocze 8-16
net user harry /times:all           - Usuwa ograniczenia godzin logowania
net user harry /comment:"jest słodki" - Dodaje krótki opis do konta
net user harry /fullname:"H.Potter" - Ustawia pełną nazwę wyświetlaną
net user harry                      - Wyświetla wszystkie szczegóły o harry'm


--- Komendy sieciowe ---

ipconfig              - Wyświetla konfigurację kart sieciowych (adres IP, maska podsieci).
ipconfig /all         - Wyświetla dokładnąkonfigurację kart sieciowych (adres IP, maska podsieci).
ipconfig /flushdns    - Czyści pamięć podręczną DNS
ipconfig /release     - Puszcza obecny adres DHCP
ipconfig /renew       - Żąda nowego adresu DHCP
ping 8.8.8.8          - sprawdza połączenie z innym hostem
tracert 8.8.8.8       - sprawdza ścieżke do innego hosta 
netstat               - wyśeietkla aktywne połączenia / porty
nslookup 8.8.8.8      - sprawdza rekordy DNS dla danej domeny 
getmac                - sprawdza adresy MAC wszystkich kart sieciowych w komputerze
netsh                 - Zaawansowane narzędzie do konfiguracji interfejsów sieciowych ( lepiej używać ustawień albo 'Wyświetl Połączenia sieciowe')
net share             - wyświetla zasoby udostępnione w sieci
arp -a                - Wyświetla tablicę translacji adresów IP na MAC.
pathping 8.8.8.8      - Połączenie ping i tracert ( nie używany już )
hostname              - Wyświetla nazwę komputera.
net view              - wyświetla listę komputerów w sieci lokalnej.
net use               - Mapuje dyski sieciowe.

--- zaawansowane komendy sieciowe --- 
netsh interface ip set address "Ethernet1" static 192.168.1.10 255.255.255.0 192.168.1.1   -   ręczne ustawianie adresu IP, maski podsiec, bramy domyślnej z konsoli 
netsh interface ip set dns "Ethernet1" static 8.8.8.8                                      -   ręczne ustawienie servera DNS dla danej karty 
netsh advfirewall set allprofiles state off                                            -   całkowicie wyłącza zapore. ( można przez GUI )

--- Zarządzanie systemem i procesami ---

tasklist              - Wyświetla listę wszystkich uruchomionych procesów.
taskkill              - Zamyka proces (np. taskkill /IM notepad.exe /F).
shutdown              - wyłącza komputer
shutdown /r           - restartuje komputer
gpupdate              - wymusza aktualizacje zasad grup.
gpresult              - Wyświetla wynikowe zasady grupy dla użytkownika/komputera.
whoami                - Wyświetla nazwę zalogowanego użytkownika.
logoff                - Wylogowuje użytkownika.
driverquery           - Wyświetla listę zainstalowanych sterowników.
net start [usługa]    - Uruchamia usługę.
sc query              - Wyświetla status usług systemowych.
net stop [usługa]     - Zatrzymuje usługę.
logoff                - wylogowuje danego użytkownika



--- Dodatkowe / nichowe ---

assoc                      - Wyświetla powiązania rozszerzeń plików z aplikacjami
set                        - Wyświetla lub ustawia zmienne środowiskowe.
path                       - Wyświetla/ustawia ścieżki przeszukiwania dla plików wykonywalnych.
echo                       - wyświetla tekst w konsoli
clip                       - Przekierowuje wynik polecenia do schowka (np. dir | clip)
fc harry1.txt harry2.txt   - Porównuje dwa pliki i wyświetla różnice między nimi.
winget                     - instalator programów zewnętrznych
timeout 2                  - Czeka określoną liczbę sekund ( tutaj 2 sekundy )
ver                        - Wyświetla wersję systemu Windows.
find "plik_tekstowy_o_nazwie_harry" C:\Users\Harry\ – Wyszukuje ciąg znaków w pliku.
powershell -command "[kod]"- Wykonuje komendę PowerShell bezpośrednio z poziomu zwykłego CMD.
title harry                - Zmienia tytuł okna konsoli na harry.
```

<img width="248" height="33" alt="image" src="https://github.com/user-attachments/assets/471c2241-40a8-405e-b755-1792e185dcd1" />

```
choice                    – Pozwala użytkownikowi wybrać opcję (T/N) w skrypcie.
calc                      - kalkulator
notepad                   - uruchamia notatnik
time                      - pokazuje i ustawia czas
wusa                      - zarządza aktualizacjami Windows
winsat disk-seg-read/write-drive C - testuje prędkość dysku C pod względem odczytu/zapisu
mode                      - służy do konfiguracji urządzeń systemowych
sc                        - otwiera zarządzanie usługami
winh132                   - aplikacja otwiera pliki pomocy
sfc                       - skanuje pliki systemowe i wyświetla te błędne


---DISKPART---
DISKPART jest narzędziem służącym do zarządzania Dyskami, partycjami, voluminami 

DISKPART                              - wchodzi do diskparta ( z poziomu CMD )
?                                     - wyświetla dostępne komendy
list disk                         - wyświetla wszystkie dostepne dyski

```

<img width="435" height="91" alt="image" src="https://github.com/user-attachments/assets/ecae4b7b-29b0-42fa-bf9f-cbccedc7cd33" />

```

select disk 0                         - wybiera dysk 0 ( jako ten, którym na, którym chcemy operować )

PRZYKŁAD:
DISKPART> select disk 0                                                                                                                  Disk 0 is now the selected disk.

list partition                        - wyświetla partycje

```

<img width="413" height="131" alt="image" src="https://github.com/user-attachments/assets/a2b35c08-9eaa-4a9a-b4e1-8085d071c6ca" />

```

select partition 4                    - wybiera partycje czwartą ( jako tą na, której chcemy operować )

create partition primary size=50000   - tworzy partycje mającą 50GB
delete partition 4                    - usuwa partycje czwartą
format fs=ntfs quick label="MojeDane" - formatuje partycje / volumin
extend size=10000                     - powiększa partycję o wydzieloną wielkość ( w tym przypadku o 10GB )
shrink desired=5000                   - zmniejsza partycję o 50GB
assign letter=G                       - przypisuje litere partycji

---CMD(dyski)---

format       - Formatuje partycję. ( proszę spojrzeć na format /? ponieważ format jest dość ważnym poleceniem. )
sfc /scannow - Skanuje i naprawia uszkodzone pliki systemowe Windows.
chkdsk       - Sprawdza dysk pod kątem błędów systemu plików.
dism         - Naprawa obrazu systemu Windows.
label        - Zmienia etykietę woluminu.
vol          - Wyświetla etykietę i numer seryjny dysku.
defrag       - defragmentuje dyski

```

## Sprawdzanie parametrów systemowych w Windowsie przy urzyciu Komend systemowych

```
systeminfo   - wyświetli Kompletny raport o systemie (wersja OS, BIOS, czas pracy, zainstalowane poprawki).
wmic         - (Windows Management Instrumentation) Potężne narzędzie do zapytań o konkretne parametry sprzętu.

```

## Usugi, Przystawki w Windowsie

Przed przejściem do przystawek chciałbym tylko powiedzieć o skrócie Windows+R, który jest bardzo przydatny kiedy chcemy zaoszczędzić czas na egzaminie. Dzięki niemu można bardzo łatwo wejść do jakiejś przystawki. 

<img width="401" height="205" alt="image" src="https://github.com/user-attachments/assets/36faaf38-845c-4e31-b474-f3632ef5788b" />

Uruchomi się takie okienkio w, którym wpisujemy np. cmd albo diskmgmt.msc i łatwo możemy wchodzić do przystawek, programów w ten sposób.

***

( Usunąć potem niech narazie zostanie )

``` 
certmgr.msc – Certyfikaty użytkownika.
compmgmt.msc – Zarządzanie komputerem (zbiorcza konsola)
devmgmt.msc – Menedżer urządzeń.
diskmgmt.msc – Zarządzanie dyskami.
eventvwr.msc – Podgląd zdarzeń 
gpedit.msc – Edytor lokalnych zasad grup (tylko wersje Pro/Enterprise).
lusrmgr.msc – Użytkownicy i grupy lokalne.
perfmon.msc – Monitor wydajności (również jako .exe).
resmon.msc – Monitor zasobów (CPU, RAM, Sieć) 
services.msc – Zarządzanie usługami systemowymi ( Usługa to program działający w tle  )
taskschd.msc – Harmonogram zadań.
WF.msc – Zaawansowane zabezpieczenia zapory Windows.
secpol.msc – Ustawienia zabezpieczeń lokalnych (podzbiór gpedit.msc dotyczący bezpieczeństwa).
tpm.msc – Zarządzanie modułem Trusted Platform Module (szyfrowanie/bezpieczeństwo).
printmanagement.msc – Zarządzanie drukowaniem (serwer druku, sterowniki).
fsmgmt.msc – Zarządzanie folderami udostępnionymi
rsop.msc – (Resultant Set of Policy) Pokazuje, jakie zasady grupy faktycznie działają na danym użytkowniku.
access.cpl – Centrum ułatwień dostępu.
appwiz.cpl – Programy i funkcje (dodawanie/usuwanie).
desk.cpl – Ustawienia ekranu.
firewall.cpl – Zapora systemu Windows (podstawowa).
hdwwiz.cpl – Kreator dodawania sprzętu / Menedżer urządzeń.
inetcpl.cpl – Właściwości internetowe.
intl.cpl – Ustawienia regionalne i językowe
joy.cpl – Kontrolery gier (joysticki)
main.cpl – Właściwości myszy.
mmsys.cpl – Dźwięk (odtwarzanie, nagrywanie).
powercfg.cpl – Opcje zasilania.
sysdm.cpl – Właściwości systemu (nazwa komputera, zmienne środowiskowe).
timedate.cpl – Data i godzina.
ncpa.cpl – Otwiera natychmiast okno 'Wyświetl połączenia sieciowe'
cleanmgr.exe – Oczyszczanie dysku.
control admintools – Folder narzędzi administracyjnych.
control mouse – Alternatywa dla main.cpl.
dfrgui.exe – Optymalizacja dysków (poprawiona nazwa z dfrgiu.exe).
dxdiag.exe – Narzędzie diagnostyczne DirectX.
netplwiz.exe – Zaawansowane konta użytkowników (hasła).
optionalfeatures.exe – Funkcje systemu Windows (włącz/wyłącz).
osk.exe – Klawiatura ekranowa.
regedit.exe – Edytor rejestru.
msconfig.exe – Konfiguracja systemu (zarządzanie rozruchem/boot).
taskmgr.exe – Menedżer zadań.
msinfo32.exe – (Dodatek do Twojej listy .exe) To najważniejsze
certutil.exe – Zarządzanie certyfikatami, ale też potężne narzędzie do liczenia sum kontrolnych plików (np. certutil -hashfile plik.exe SHA256)
mrt.exe – Microsoft Removal Tool

```






### **SEKCJA .MSC (Microsoft Management Console)**

**<strong>certmgr.msc</strong>** — Certyfikaty użytkownika.

<img width="804" height="608" alt="image" src="https://github.com/user-attachments/assets/d21c3964-b996-4de7-8c29-581ece85873f" />

Służy do zarządzania certyfikatami cyfrowymi zalogowanego użytkownika, umożliwiając ich przeglądanie, importowanie oraz eksportowanie. Pozwala na weryfikację zaufanych głównych urzędów certyfikacji oraz zarządzanie kluczami prywatnymi używanymi do szyfrowania lub podpisu.

**<strong>compmgmt.msc</strong>** — Zarządzanie komputerem (zbiorcza konsola).

[ZDJĘCIE]


**<strong>devmgmt.msc</strong>** — Menedżer urządzeń.

[ZDJĘCIE]


**<strong>diskmgmt.msc</strong>** — Zarządzanie dyskami.

[ZDJĘCIE]


**<strong>eventvwr.msc</strong>** — Podgląd zdarzeń.

[ZDJĘCIE]


**<strong>gpedit.msc</strong>** — Edytor lokalnych zasad grup (tylko wersje Pro/Enterprise).

[ZDJĘCIE]


**<strong>lusrmgr.msc</strong>** — Użytkownicy i grupy lokalne.

[ZDJĘCIE]


**<strong>perfmon.msc</strong>** — Monitor wydajności (również jako .exe).

[ZDJĘCIE]


**<strong>resmon.msc</strong>** — Monitor zasobów (CPU, RAM, Sieć).

[ZDJĘCIE]


**<strong>services.msc</strong>** — Zarządzanie usługami systemowymi (Usługa to program działający w tle).

[ZDJĘCIE]


**<strong>taskschd.msc</strong>** — Harmonogram zadań.

[ZDJĘCIE]


**<strong>WF.msc</strong>** — Zaawansowane zabezpieczenia zapory Windows.

[ZDJĘCIE]


**<strong>secpol.msc</strong>** — Ustawienia zabezpieczeń lokalnych (podzbiór gpedit.msc).

[ZDJĘCIE]


**<strong>tpm.msc</strong>** — Zarządzanie modułem Trusted Platform Module.

[ZDJĘCIE]


**<strong>printmanagement.msc</strong>** — Zarządzanie drukowaniem (serwer druku, sterowniki).

[ZDJĘCIE]


**<strong>fsmgmt.msc</strong>** — Zarządzanie folderami udostępnionymi.

[ZDJĘCIE]


**<strong>rsop.msc</strong>** — Pokazuje, jakie zasady grupy faktycznie działają na użytkowniku.

[ZDJĘCIE]


---


### **SEKCJA .CPL (Control Panel Items)**

**<strong>access.cpl</strong>** — Centrum ułatwień dostępu.

[ZDJĘCIE]


**<strong>appwiz.cpl</strong>** — Programy i funkcje (dodawanie/usuwanie).

[ZDJĘCIE]


**<strong>desk.cpl</strong>** — Ustawienia ekranu.

[ZDJĘCIE]


**<strong>firewall.cpl</strong>** — Zapora systemu Windows (podstawowa).

[ZDJĘCIE]


**<strong>hdwwiz.cpl</strong>** — Kreator dodawania sprzętu / Menedżer urządzeń.

[ZDJĘCIE]


**<strong>inetcpl.cpl</strong>** — Właściwości internetowe.

[ZDJĘCIE]


**<strong>intl.cpl</strong>** — Ustawienia regionalne i językowe.

[ZDJĘCIE]


**<strong>joy.cpl</strong>** — Kontrolery gier (joysticki).

[ZDJĘCIE]


**<strong>main.cpl</strong>** — Właściwości myszy.

[ZDJĘCIE]


**<strong>mmsys.cpl</strong>** — Dźwięk (odtwarzanie, nagrywanie).

[ZDJĘCIE]


**<strong>powercfg.cpl</strong>** — Opcje zasilania.

[ZDJĘCIE]


**<strong>sysdm.cpl</strong>** — Właściwości systemu (nazwa komputera, zmienne).

[ZDJĘCIE]


**<strong>timedate.cpl</strong>** — Data i godzina.

[ZDJĘCIE]


**<strong>ncpa.cpl</strong>** — Otwiera natychmiast okno 'Wyświetl połączenia sieciowe'.

[ZDJĘCIE]


---


### **SEKCJA .EXE I POZOSTAŁE NARZĘDZIA**

**<strong>cleanmgr.exe</strong>** — Oczyszczanie dysku.

[ZDJĘCIE]


**<strong>control admintools</strong>** — Folder narzędzi administracyjnych.

[ZDJĘCIE]


**<strong>control mouse</strong>** — Alternatywa dla main.cpl.

[ZDJĘCIE]


**<strong>dfrgui.exe</strong>** — Optymalizacja dysków.

[ZDJĘCIE]


**<strong>dxdiag.exe</strong>** — Narzędzie diagnostyczne DirectX.

[ZDJĘCIE]


**<strong>netplwiz.exe</strong>** — Zaawansowane konta użytkowników (hasła).

[ZDJĘCIE]


**<strong>optionalfeatures.exe</strong>** — Funkcje systemu Windows (włącz/wyłącz).

[ZDJĘCIE]


**<strong>osk.exe</strong>** — Klawiatura ekranowa.

[ZDJĘCIE]


**<strong>regedit.exe</strong>** — Edytor rejestru.

[ZDJĘCIE]


**<strong>msconfig.exe</strong>** — Konfiguracja systemu (zarządzanie rozruchem/boot).

[ZDJĘCIE]


**<strong>taskmgr.exe</strong>** — Menedżer zadań.

[ZDJĘCIE]


**<strong>msinfo32.exe</strong>** — Pełne informacje o systemie i sprzęcie (najważniejsze).

[ZDJĘCIE]


**<strong>certutil.exe</strong>** — Zarządzanie certyfikatami i liczenie sum kontrolnych.

[ZDJĘCIE]


**<strong>mrt.exe</strong>** — Microsoft Removal Tool (usuwanie wirusów).

[ZDJĘCIE]


**<strong>winver</strong>** — Sprawdzanie dokładnej wersji systemu Windows.

[ZDJĘCIE]



> dodać normy EN 50174


## Programy na Windowsie 

## Windows jako Klient

## Zadania praktyczne.





