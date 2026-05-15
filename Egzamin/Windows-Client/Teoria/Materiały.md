<img width="1247" height="550" alt="image" src="https://github.com/user-attachments/assets/84314586-78ce-4279-b385-a1507bba03f9" /># Teoria

Windows nie jest teoretycznie trudny, ponieważ nie musimy na nim zapamiętywać rzeczy na pamięć. Wystarczy, że wiemy jak się do nich doklikać. Oczywiście nadal trzeba umieć komendy w terminalu Windowsa ale jest ich o wiele mniej niż na linuxie.

Bez dwóch zdań najgorzą rzeczą w Windowsie jest to, że wszystkie funkcję systemu są tak rozproszone, że truno jest znaleść to czego szukamy jeśli nie mamy wstępnej informacji gdzie to może się znajdować.

Zagadnienia:
- Terminal w windowsie
- usługi i zakładki .msc
- Programy na Windowsie
- Windows jako client, któremu są świadczone usługi ( Windows Server )
- Odpowiedzi na pytania z egzaminów

## Komendy w Windowsie ( dodać sprawdzanie parametrów systemowych ) 

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

<img width="1209" height="845" alt="image" src="https://github.com/user-attachments/assets/19543b1e-18cc-444d-8be8-c4d5dfd09fcf" />

To zbiorcza konsola narzędzi administracyjnych, która łączy w sobie m.in. zarządzanie dyskami, usługami i użytkownikami w jednym oknie. Pozwala nam na wejście w wiele przystawek systemowych - nie dodaję nic do nich.

**<strong>devmgmt.msc</strong>** — Menedżer urządzeń.

<img width="775" height="563" alt="image" src="https://github.com/user-attachments/assets/9a33e760-6061-4d66-87d9-06f31a87ddb1" />
<img width="376" height="72" alt="image" src="https://github.com/user-attachments/assets/f5487c6b-8441-434a-a9b1-8496447a7b68" />
<img width="773" height="564" alt="image" src="https://github.com/user-attachments/assets/a13d73f5-2d1b-4108-baf9-503554322391" />

Pozwala na zarządzanie sprzętem oraz sterownikami wszystkich komponentów zainstalowanych w komputerze. 

Zakładka porty COM pozawla nam sprawdzić jakie porty COM są dostępne na naszym komputerze w celu połączenie się przez Konsole do jakiegoś urządzenia.

Zakładki takie jak 'Karty Graficzne' lub 'Procesory' mogą nam także pomóc w identyfikacji parametrów systemowych

**<strong>diskmgmt.msc</strong>** — Zarządzanie dyskami.

<img width="1205" height="595" alt="image" src="https://github.com/user-attachments/assets/15b91a10-496f-44fd-af0e-cde7b6487cb0" />

nardzędzie podobne do DISKPARTA ale w GUI pozwala nam na zmienianie właściwości partycji, voluminów na naszym systemie.

Przystawka ta w kontekscie egzaminu jest bardzo ważna. Na wielu arkuszach praktycznych pojawiają się zadania z diskmgmt.msc \

>TODO : Dodać Opis ( W GUI ) Jak działa diskmgmt.msc

**<strong>eventvwr.msc</strong>** — Podgląd zdarzeń.

<img width="1513" height="942" alt="image" src="https://github.com/user-attachments/assets/8eb1be83-79be-460c-8f3a-32ea07d5b4e8" />

Umożliwia przeglądanie dzienników systemowych, w których zapisywane są informacje o błędach, ostrzeżeniach i sukcesach aplikacji oraz usług.

**<strong>gpedit.msc</strong>** — Edytor lokalnych zasad grup (tylko wersje Pro/Enterprise).

<img width="1059" height="658" alt="image" src="https://github.com/user-attachments/assets/895500ca-33d9-441b-add1-36115abea0fc" />

Narzędzie do konfiguracji zaawansowanych ustawień systemu i użytkownika poprzez zasady (polisy), które nie są dostępne w zwykłym panelu sterowania

Na egzaminie jest także badzo ważną pzystawką. To tutaj robimy takie rzeczy jak wyłączamy dostęp do panelu sterowania i podobne.  


<strong>Zarządzanie Restrykcjami Użytkownika</strong>

Konfiguracja użytkownika -> Szablony administracyjne.

<img width="1316" height="791" alt="image" src="https://github.com/user-attachments/assets/ef3904cf-76f4-49fa-bcf3-b729f20b2a1f" />

Przykłady eksploatacji:
```
Panel Sterowania: można tutaj całkowicie zablokować dostęp do Panelu sterowania i Ustawień lub ukryć tylko konkretne ikony.
Pulpit: Zablokowanie zmiany tapety, ukrycie ikon systemowych (np. Kosza) lub zablokowanie dodawania/usuwania skrótów.
Menu Start i Pasek zadań: Usunięcie przycisku "Zamknij system" (użytkownik nie będzie mógł wyłączyć komputera przyciskiem programowym), ukrycie zegara lub listy programów.
System: Blokada dostępu do Wiersza poleceń (cmd.exe), edytora rejestru (regedit.exe) lub menedżera zadań.
```
<strong>Konfiguracja Zabezpieczeń (Sekcja Systemowa)</strong>

Konfiguracja komputera -> Ustawienia systemu Windows -> Ustawienia zabezpieczeń.

<img width="950" height="407" alt="image" src="https://github.com/user-attachments/assets/b86b7304-fd59-4cdf-9e72-e2a3f19c5b78" />

Przykłady eksploatacji:
```
Zasady haseł: Wymuszenie minimalnej długości hasła (np. 8 znaków), wymuszenie złożoności (duże litery, cyfry) oraz ustawienie ważności hasła (użytkownik musi zmienić hasło co 30 dni).
Zasady blokady konta: Ustawiasz tu, po ilu nieudanych próbach logowania konto ma zostać zablokowane i na jak długo (np. 3 błędne próby = blokada na 15 minut).
Prawa użytkownika: Przypisywanie konkretnych uprawnień, np. "Kto może zmieniać czas systemowy" lub "Kto może logować się lokalnie".
```

<strong>Skrypty Logowania i Wylogowywania</strong>

Ustawienia systemu Windows -> Skrypty (Logowanie/Wylogowanie)

<img width="1247" height="550" alt="image" src="https://github.com/user-attachments/assets/6b77cb39-bf7e-4919-9165-1742ca596e19" />

Przykłady eksploatacji:
```
można tu dodać pliki .bat lub .ps1, które uruchomi się automatycznie po wylogowaniu lub zalogowaniu do systemu.
```

<strong>Zarządzanie Aktualizacjami i Składnikami Windows</strong>

<img width="1351" height="2138" alt="image" src="https://github.com/user-attachments/assets/f60d11cd-a4fc-4629-a8bf-423f68759bfb" />

Przykłady eskploatacji:

```

Windows Update: Możesz całkowicie wyłączyć automatyczne aktualizacje lub skonfigurować godziny, w których system ma prawo się restartować.
Windows Defender: Możliwość wyłączenia antywirusa lub skonfigurowania harmonogramu skanowania.
Instalator Windows: Blokowanie możliwości instalowania nowego oprogramowania przez użytkowników bez uprawnień administratora.

```

<strong>Blokowanie dostępu do napędów wymiennych</strong>

Konfiguracja komputera -> Szablony administracyjne -> Składniki systemu Windows

<img width="1204" height="1308" alt="image" src="https://github.com/user-attachments/assets/d46d6f89-ba5f-4078-9226-1838cf96ba64" />


Przykłady eksploatacji:

```

Dyski wymienne: Odmów dostępu do zapisu (użytkownik może czytać z pendrive, ale nie może nic na niego skopiować).
Dyski wymienne: Odmów dostępu do odczytu (całkowita blokada USB).

```

### Podsumowując: gpedit.msc to narzędzie, które "mówi systemowi, co użytkownikowi wolno, a czego nie"


***


**<strong>lusrmgr.msc</strong>** — Użytkownicy i grupy lokalne.

<img width="941" height="716" alt="image" src="https://github.com/user-attachments/assets/d2d84e6e-62e5-41d5-ba77-28344046e000" />
<img width="396" height="448" alt="image" src="https://github.com/user-attachments/assets/3ba3f31e-e174-4f68-a7bd-ccf93ec9e789" />
<strong>właśnie tutaj można zmieniac niektóre z ważnych ustawień hasła na egzaminie.</strong>

Narzędzie do zarządzania lokalnymi kontami użytkowników oraz grupami, umożliwiające m.in. zakładanie nowych kont, zmianę haseł czy przypisywanie osób do grup (np. Administratorzy).


**<strong>services.msc</strong>** — Zarządzanie usługami systemowymi (Usługa to program działający w tle).

<img width="1071" height="515" alt="image" src="https://github.com/user-attachments/assets/465a1a2e-0c0f-4610-83bb-5d28a71c160f" />

Narzędzie służące do zarządzania usługami systemowymi, które umożliwia ich uruchamianie, zatrzymywanie oraz wybór trybu startu

**<strong>taskschd.msc</strong>** — Harmonogram zadań.

<img width="1346" height="872" alt="image" src="https://github.com/user-attachments/assets/6f549f8e-86a1-471e-9b4b-0c8f9396016e" />

Narzędzie pozwalające na automatyczne uruchamianie programów lub skryptów o określonych godzinach lub w odpowiedzi na konkretne zdarzenia systemowe

**<strong>WF.msc</strong>** — Zaawansowane zabezpieczenia zapory Windows. ( poprostu ustawienia zapory ) 

<img width="1371" height="728" alt="image" src="https://github.com/user-attachments/assets/a7421a9c-1581-462e-8e4d-7d9479e4ec08" />

Zaawansowana konsola zarządzania Zaporą Windows, która pozwala na tworzenie precyzyjnych reguł przychodzących i wychodzących dla konkretnych portów, programów lub adresów IP

<img width="268" height="30" alt="image" src="https://github.com/user-attachments/assets/93b7d0fd-61d1-4b5a-b0e6-96fde3116391" />

Po wejściu tutaj można zmienić stany wszystkich profilów zapory ( na egzaminie może być zadanie aby wyłączyć wszystkie profile zapory aby przeszedł ping ) 

<img width="395" height="471" alt="image" src="https://github.com/user-attachments/assets/42ce591b-d1b5-41bd-abe7-da77eb534427" />


**<strong>secpol.msc</strong>** — Ustawienia zabezpieczeń lokalnych (podzbiór gpedit.msc).

<img width="1200" height="949" alt="image" src="https://github.com/user-attachments/assets/a33aacbb-963d-4b9c-84a2-d1fcb7689676" />

ta przystawka Pozwala na WIELE operacji na kontach, jest podzbiorem gpedit.msc ( wyciętą częścią ), po przeklikaniu w tej zakładce da się znaleśc wszystko dotyczące pytań o kontach.

**<strong>tpm.msc</strong>** — Zarządzanie modułem Trusted Platform Module.

<img width="999" height="679" alt="image" src="https://github.com/user-attachments/assets/ecf713a5-5d40-4055-8ea3-bcf8f97028ba" />

Nie jest przydatny na egzaminie praktycznym INF02

jest Narzędziem służący, do sprawdzania statusu i zarządzania modułem zaufanej platformy (Trusted Platform Module) na płycie głównej.

**<strong>printmanagement.msc</strong>** — Zarządzanie drukowaniem (serwer druku, sterowniki).

<img width="945" height="719" alt="image" src="https://github.com/user-attachments/assets/2bb9592d-ea93-4ef3-915d-8baa3b967d2b" />

Narzędzie do kompleksowego zarządzania infrastrukturą druku, pozwalające na monitorowanie kolejek wydruku, serwerów oraz sterowników drukarek w jednym miejscu

**<strong>fsmgmt.msc</strong>** — Zarządzanie folderami udostępnionymi.

<img width="783" height="684" alt="image" src="https://github.com/user-attachments/assets/9d106fbd-3bf1-42d8-ad9c-b5d86446eba5" />

Narzędzie umożliwiające zarządzanie wszystkimi zasobami udostępnionymi w sieci lokalnej, bieżącymi sesjami użytkowników oraz otwartymi plikami

**<strong>rsop.msc</strong>** — Pokazuje, jakie zasady grupy faktycznie działają na użytkowniku.

<img width="834" height="542" alt="image" src="https://github.com/user-attachments/assets/d8c7adf3-ab30-4fba-9270-369177b87e07" />

Kompletnie bezuzyteczny - pozwala sprawdzić, jakie konkretnie zasady grupy (GPO) są aktualnie zastosowane do danego użytkownika i komputera

**<strong>perfmon.msc</strong>** — Monitor wydajności (również jako .exe).

<img width="1339" height="922" alt="image" src="https://github.com/user-attachments/assets/b68e80cf-c9d3-49e3-b9de-e1113d8d25a5" />

Narzędzie służące do monitorowania wydajności komputera w czasie rzeczywistym - Kompletnie bezużyteczny na egzaminie praktycznym INF02

<strong>panel sterowania</strong>

<img width="1122" height="620" alt="image" src="https://github.com/user-attachments/assets/d12875ab-e120-4d20-b044-203b2d64ddf8" />

Święty gral Windowsa gdzie można znaleść niemal wszystkie ustawienia systemu. Wiekszość ustawień w panelu sterowania jest dosyć prosta i można do nich łatwo dojść przeklikując zakładki w nim zawarte.

TODO: Stworzyć detailed guide po panelu sterowania.


<strong>ustawienia</strong>

<img width="1176" height="939" alt="Zrzut ekranu 2026-05-15 200226" src="https://github.com/user-attachments/assets/1aa8d514-aa33-426c-9a0b-561e4b6a6d09" />

Podobnie jak w przypadku panelu sterowania w ustawieniach można znaleść niemal wszystko jeśli tylko pomyślimy logicznie i wystarczająco je przeklikamy.

TODO: Stworzyć detailed guide po ustawieniach.


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


regedit


> dodać normy EN 50174


## Programy na Windowsie 

## Windows jako Klient

## Zadania praktyczne.





