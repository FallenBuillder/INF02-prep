# Teoria

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

<strong>ustawienia</strong>

<img width="1176" height="939" alt="Zrzut ekranu 2026-05-15 200226" src="https://github.com/user-attachments/assets/1aa8d514-aa33-426c-9a0b-561e4b6a6d09" />

Podobnie jak w przypadku panelu sterowania w ustawieniach można znaleść niemal wszystko jeśli tylko pomyślimy logicznie i wystarczająco je przeklikamy.

TODO: Stworzyć detailed guide po ustawieniach.


---


<strong>panel sterowania</strong>

<img width="1122" height="620" alt="image" src="https://github.com/user-attachments/assets/d12875ab-e120-4d20-b044-203b2d64ddf8" />

Święty gral Windowsa gdzie można znaleść niemal wszystkie ustawienia systemu. Wiekszość ustawień w panelu sterowania jest dosyć prosta i można do nich łatwo dojść przeklikując zakładki w nim zawarte.

TODO: Stworzyć detailed guide po panelu sterowania.


### **SEKCJA .CPL (Control Panel Items)**

## UWAGA - Wszystkie sekcje .cpl można znaleść w panelu sterowania NIE TRZEBA ZAPAMIĘTYWAĆ ICH NA PAMIĘĆ dlatego nie będą naraazie omawiane...

Przykład omówienia jednej sekcji panelu sterowania 

**<strong>access.cpl</strong>** — Centrum ułatwień dostępu.

<img width="1343" height="896" alt="image" src="https://github.com/user-attachments/assets/8692b1a1-6584-4eb1-8092-e9fbd5e837e8" />

<img width="403" height="199" alt="image" src="https://github.com/user-attachments/assets/71f26219-10d1-4e15-8b83-13aab514c2c1" />

Narzędzie otwierające aplet Ułatwienia dostępu w Panelu sterowania, pozwalające na konfigurację funkcji pomocniczych, takich jak klawisze trwałe - kompletnie bezużyteczny

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

<img width="372" height="466" alt="image" src="https://github.com/user-attachments/assets/405fe06f-a220-493c-ba8a-39248af4a35c" />

służy do bezpiecznego usuwania zbędnych plików systemowych, takich jak pliki tymczasowe, zawartość kosza czy pozostałości po aktualizacjach systemu Windows 

**<strong>control admintools</strong>** — Folder narzędzi administracyjnych.

<img width="405" height="207" alt="image" src="https://github.com/user-attachments/assets/5a4375ab-e313-48db-9379-6fa4dc9cdda7" />

<img width="1347" height="890" alt="image" src="https://github.com/user-attachments/assets/9bd14653-c054-41e5-94e7-044528f493bd" />

BARDZO przydatne nardzędzie jeśli nie wiemy gdzie znaleść Przystawek w Windowsie 

**<strong>dfrgui.exe</strong>** — Optymalizacja dysków.

<img width="702" height="500" alt="image" src="https://github.com/user-attachments/assets/70f0239c-3939-4588-80d7-5bf7af88b0d9" />

służy do defragmentacji dysków HDD oraz optymalizacji (wysyłania komendy TRIM) dla dysków SSD w celu przyspieszenia działania systemu.

Kompletnie bezużyteczny.

**<strong>dxdiag.exe</strong>** — Narzędzie diagnostyczne DirectX.

<img width="725" height="529" alt="image" src="https://github.com/user-attachments/assets/d452671e-ce5e-4c57-a263-dac60ddf68c7" />

Narzędzie diagnostyczne DirectX, które służy do zbierania szczegółowych informacji o komponentach multimedialnych komputera, takich jak karta graficzna, dźwiękowa oraz zainstalowane sterowniki

**<strong>netplwiz.exe</strong>** — Zaawansowane konta użytkowników (hasła).

<img width="463" height="508" alt="image" src="https://github.com/user-attachments/assets/883881a7-dae3-4d9f-a91c-db2dc0cd2d23" />

pozwala na to aby sprawić, że trzeba kliknąc Ctr+Alt+Delete przed włączeniem systemu - tak to jest bezużyteczny

**<strong>optionalfeatures.exe</strong>** — Funkcje systemu Windows (włącz/wyłącz).

<img width="415" height="365" alt="image" src="https://github.com/user-attachments/assets/80bf6cbe-9713-4156-83f6-a838de536cd7" />

Bardzo przydatny. Jeśli na egzaminie jest np. napisane "Wyłącz WSL" to będzie to właśnie tutaj 

**<strong>osk.exe</strong>** — Klawiatura ekranowa.

Włącza klawiaturę graficzną ( nie da się zrobić screena jej ) 

**<strong>regedit.exe</strong>** — Edytor rejestru.

<img width="1588" height="566" alt="image" src="https://github.com/user-attachments/assets/3bf98033-b9ad-41ee-8820-5db51746163f" />

Narzędzie Edytor rejestru, będące hierarchiczną bazą danych, w której system Windows przechowuje wszystkie ustawienia konfiguracji sprzętu, oprogramowania oraz preferencje użytkowników. Rejestr jest "mózgiem" systemu – każda zmiana wprowadzona w Panelu sterowania czy gpedit.msc ostatecznie zapisuje się jako konkretna wartość w jednym z kluczy rejestru.

RegEdit jest przepotężnym narzędziem ale znalezienie czegokolwiek w nim jest prawie co niemożliwe ponieważ jest on jagby bazą danych dla CAŁEGO systemu operacyjnego 

**<strong>msconfig.exe</strong>** — Konfiguracja systemu (zarządzanie rozruchem/boot).

HKEY_CLASSES_ROOT (HKCR): Informacje o powiązaniach plików (jaki program otwiera .txt itp.).

HKEY_CURRENT_USER (HKCU): Ustawienia aktualnie zalogowanego użytkownika (tapeta, kolory, układ klawiatury).

HKEY_LOCAL_MACHINE (HKLM): Globalne ustawienia komputera i sprzętu, wspólne dla wszystkich użytkowników.

HKEY_USERS (HKU): Profile wszystkich użytkowników na dysku.

HKEY_CURRENT_CONFIG (HKCC): Informacje o aktualnym profilu sprzętowym.



TODO: Dodać detailed guide po Edytorze Rejestru.

**<strong>taskmgr.exe</strong>** — Menedżer zadań.
<img width="1263" height="1095" alt="image" src="https://github.com/user-attachments/assets/027ef3f7-d2e6-4952-b950-a7b5f66817da" />

jest podstawowym panelem diagnostycznym systemu Windows, umożliwiającym monitorowanie procesów, wydajności oraz zarządzanie uruchomionymi aplikacjami.

W Zakładce 'Wydajnośc' można dodatkowo znaleść różnego typu parametry dotyczące systemu operacyjnego

<img width="1266" height="1087" alt="image" src="https://github.com/user-attachments/assets/b251405f-dcd0-4dfe-95b5-7fbae672a95e" />

<img width="1027" height="1037" alt="image" src="https://github.com/user-attachments/assets/3ebcd044-b2ae-4a4d-85b5-5f5a56a3ad7d" />

<img width="1263" height="1084" alt="image" src="https://github.com/user-attachments/assets/efeb3a08-8ea0-4047-a92a-8bf6cd18c7be" />

<img width="1020" height="1030" alt="image" src="https://github.com/user-attachments/assets/c0652bb0-2c6f-42a1-8f96-cdee05c78aad" />

**<strong>msinfo32.exe</strong>** — Pełne informacje o systemie i sprzęcie (najważniejsze).

<img width="2439" height="1276" alt="image" src="https://github.com/user-attachments/assets/441a5028-90f5-467c-a135-6a9c376fe2f1" />

Narzędzie Informacje o systemie, które generuje najbardziej szczegółowy raport o konfiguracji sprzętowej i programowej komputera.

Bardziej dokładne parametry o Windowsie można znaleść korzystając narzędzia wmic.
<img width="239" height="80" alt="image" src="https://github.com/user-attachments/assets/d4e01d4b-ae97-4fc0-9a2b-453c8cfbb3bc" />


**<strong>certutil.exe</strong>** — Zarządzanie certyfikatami i liczenie sum kontrolnych. ( jest narzędziem konsoli nie grafcznym ) 

Kodowanie: certutil -encode plik.exe zakodowany.txt      ( base 64 ) 
Dekodowanie: certutil -decode zakodowany.txt plik.exe    ( base 64 )
certutil -store My (wyświetla osobiste certyfikaty).
Komenda: certutil -hashfile [ścieżka_do_pliku] SHA256    - sprawdza, czy plik nie jest uszkodzony lub zmodyfikowany przez wirusa. ( raczej nie potrzebne na egzaminie )
Obsługuje też: MD5, SHA1, SHA512.


**<strong>mrt.exe</strong>** — Microsoft Removal Tool (usuwanie wirusów).

<img width="514" height="466" alt="image" src="https://github.com/user-attachments/assets/88a09378-59b4-48a6-8dfd-f301aa65a00c" />

<img width="511" height="461" alt="image" src="https://github.com/user-attachments/assets/7a6610ea-096d-44ba-9b45-b62a9e39e5d5" />

Skanuje komputer w poszukiwaniu wirusów.

**<strong>winver</strong>** — Sprawdzanie dokładnej wersji systemu Windows.

<img width="453" height="416" alt="image" src="https://github.com/user-attachments/assets/f756113b-fdf6-4091-9972-0ff958eea855" />









## Programy na Windowsie - narazie wszystko z AI przepisać / zrobić zdjęcia i zrobić dobrą notatkę.

Wszystkie programy, które są poniżej przedstawione można znaleść w folderze PROGRAMY na jednym z pendrivów podczas egzaminu zawodowego.


### cpuz_x64.exe / cpuz.exe

<img width="66" height="72" alt="image" src="https://github.com/user-attachments/assets/678cae83-da75-4493-bcd1-0095970830f8" />

<img width="406" height="402" alt="image" src="https://github.com/user-attachments/assets/f06de79e-328b-4f53-acf8-525a1190a9d7" />

<img width="398" height="401" alt="image" src="https://github.com/user-attachments/assets/8b102dbf-ca25-4194-bfdd-a6a0829c1e6b" />

<img width="401" height="401" alt="image" src="https://github.com/user-attachments/assets/a477664a-6821-465f-a4da-121d1699c6aa" />

<img width="402" height="405" alt="image" src="https://github.com/user-attachments/assets/b69c0304-16f7-4931-a43c-8bf057c05360" />

<img width="405" height="400" alt="image" src="https://github.com/user-attachments/assets/6dba9711-ada5-4a9b-8bf8-e15c5b48d8cf" />

Program CPU-Z posiada bardzo dużą ilośc informacji o procesorze, karcie graficznej, ramie ,płycie głównej - nie ma sensu omawiać wszystkich jego parametrów ponieważ na egzaminach INF02 zadania związane z tym programem każą na przykład: zrobić zdjęcie danego parametry / wypisać go w tabelce. Myśle, że można się domyślić jaki dany parametre gdzie wpisać i gdzie go znaleść ponieważ CPU-Z jest dość przyjaznym programem graficznym jeśli chodzi o znajdywanie w nim różnych parametrów.

Te rzecz, które mogą się pojawić na egzaminie to np.




<strong>Zakładka CPU (Procesor):</strong>
Name (Nazwa procesora): Pełna nazwa rynkowa (np. Intel Core i5-10400F lub AMD Ryzen 5 3600).

Code Name (Nazwa kodowa): Nazwa architektury (np. Comet Lake, Matisse).

Package (Obudowa / Gniazdo): Typ podstawki procesora (np. Socket AM4 (1331), Socket 1200 LGA).

Technology (Proces technologiczny): Litografia wyrażona w nanometrach (np. 14 nm, 7 nm).

Core Voltage (Napięcie rdzenia): Aktualne napięcie zasilania procesora (np. 1.248 V).

Core Speed (Taktowanie rdzenia): Bieżąca częstotliwość procesora (np. 3591.2 MHz).

Multiplier (Mnożnik): Wartość mnożnika procesora (np. x 36.0).

Bus Speed (Taktowanie magistrali): Częstotliwość szyny (np. 99.8 MHz).

Cache (Pamięć podręczna): Najczęściej pytają o rozmiar pamięci L3 (Third Level Cache), rzadziej L1 lub L2.

Cores / Threads (Rdzenie / Wątki): Liczba fizycznych rdzeni i wątków logicznych (np. 6 Cores / 12 Threads).

<strong>Zakładka Mainboard (Płyta główna):</strong>
Manufacturer (Producent): Producent płyty (np. ASUSTeK COMPUTER INC., MSI).

Model: Dokładne oznaczenie modelu płyty głównej.

Chipset & Southbridge: Model mostka północnego/południowego lub układu logiki (np. Intel Skylake-S, AMD B450).
 
BIOS Brand & Version: Producent oraz wersja oprogramowania układowego BIOS (np. American Megatrends Inc., wersja 1802).

<strong>Zakładka Memory (Pamięć RAM – ogólne):</strong>

Type: Typ pamięci (np. DDR3, DDR4, DDR5).

Channel #: Tryb pracy pamięci (Single – jednokanałowy, Dual – dwukanałowy).

Size (Pojemność): Łączna ilość pamięci RAM zainstalowanej w systemie (np. 16 GBytes).

DRAM Frequency: Aktualne taktowanie rzeczywiste pamięci 

CAS# Latency (CL): Główne opóźnienie pamięci (np. 16.0 clocks).

<strong>Zakładka SPD (Pamięć RAM – szczegóły modułu):</strong>
Slot # (Wybór gniazda):

Module Size: Pojemność jednego modułu (np. 8192 MBytes).

Max Bandwidth: Maksymalna przepustowość standardowa (np. DDR4-2666 (1333 MHz)).

Module Manufacturer: Producent samej kości pamięci (np. Kingston, Crucial, Corsair).











### gpuz.exe

<img width="421" height="268" alt="image" src="https://github.com/user-attachments/assets/41b95902-2d0a-43c0-863d-f86438a78b22" />

<img width="394" height="604" alt="image" src="https://github.com/user-attachments/assets/ac736c79-4fb1-44a0-a50f-cccaf3c79a61" />

<img width="388" height="545" alt="image" src="https://github.com/user-attachments/assets/ad50ad11-66fb-4906-997b-a454eb8e325c" />

Program GPU-Z podobnie jak program CPU-Z często pojawia się na egzaminie a zadanie z nim związanie są dosyć prostę i także wymagają prostych screenów / czytania parametrów.

stary PDF, który zrobiłem, który wytłumacza funkcję GPU-Z.
<br>
[GPU-Z (1).pdf](https://github.com/user-attachments/files/27853055/GPU-Z.1.pdf)
















### hdtune_255.exe.

<img width="102" height="76" alt="image" src="https://github.com/user-attachments/assets/37fc31f1-61d7-4db0-9de9-7f782b29b02d" />

<img width="570" height="463" alt="image" src="https://github.com/user-attachments/assets/3f8af215-5e14-4b65-81ac-40083d75130f" />

<img width="573" height="468" alt="image" src="https://github.com/user-attachments/assets/127f19e7-4065-4857-ba9b-f258e6dd0a31" />

<img width="581" height="473" alt="image" src="https://github.com/user-attachments/assets/25ba9b20-e772-4195-9180-798b9acb9be3" />

<img width="574" height="478" alt="image" src="https://github.com/user-attachments/assets/b7aa7f8a-018c-4acc-bfbb-df517df8ebe3" />

darmowe narzędzie diagnostyczne służące do testowania wydajności dysków komputerowych poprzez pomiar ich szybkości odczytu oraz czasu dostępu do danych. Dodatkowo umożliwia ono monitorowanie kondycji nośnika za pomocą parametrów S.M.A.R.T.

### crystaldiskinfo.exe

<img width="674" height="997" alt="image" src="https://github.com/user-attachments/assets/9c2b4e80-41c2-4d9b-afad-3443ef5d4771" />

CrystalDiskInfo jak sama nazwa wskazuje jest programem, który służy do otrzymania informacji o dysku z systemu. Na egzaminach INF02 przykładem eksploatacji tego programu ( podobnie jak ostatnich ) byoby by zrobienie zdjeć danych parametrów oraz zapisanie ich w tabelce.

### hwmonitor.exe – do temperatur i napięć.

<img width="641" height="797" alt="image" src="https://github.com/user-attachments/assets/fc5191b2-12fd-4798-90ec-efd3dfa4947a" />

Program HWMonitor służy do sprawdzania temperatur, napięć różnych komponentów w naszym systemie w danym czasie.

### wireshark_setup.exe

Program wireshark służy do analizy ruchu sieciowego, który przechodzi przez nasz komputer. 

<img width="109" height="73" alt="image" src="https://github.com/user-attachments/assets/bed7748f-fddc-4da8-90f2-7bd9fd8e5e23" />

<img width="1561" height="749" alt="image" src="https://github.com/user-attachments/assets/8607dbbd-83a6-42db-a493-1ea3897426c4" />

pliki w wiresharku mają rozszerzenie .pcap - jeśli na egzaminie będzie zadanie aby otworzyć plik .pcap wchodzimy tutaj

<img width="321" height="46" alt="image" src="https://github.com/user-attachments/assets/27d8cfbc-21cf-4a34-9064-5217146ab6af" />

A następnie otworzy się okienko w ,którym będziemy mieli wybrać nasz plik.

<img width="532" height="191" alt="image" src="https://github.com/user-attachments/assets/f4c364b0-f9dd-4ba8-b1c3-ce52ac46546b" />

Po kliknięciu na interfejs karty sieciowej na, której jest obecnie przetwarzany jakiś ruch pokaże się nam taki interfejs:

<img width="830" height="569" alt="image" src="https://github.com/user-attachments/assets/dfffe462-a731-42ec-9d88-c0bf9829e074" />

Tutaj dzieje się cała magia i widać pakiety, które przychodzą i wychodzą z komputera, które można potem zfiltrować do dalszej analizy

<strong>Filmik na yt jak używac Wiresharka:</strong>

[Link](https://www.youtube.com/watch?v=lb1Dw0elw0Q&t=68s)

> Wszystkie filmiki są krótkie i na temat.

### nmap_setup.exe / zenmap.exe

Nmap pojawił się już na paru egzaminach INF02 a więc napewno warto się go nauczyć. Lepiej się nauczyć wersji w GUI bo uczenie się go przez CLI wychodzi za zakres egzaminu.

<img width="109" height="81" alt="image" src="https://github.com/user-attachments/assets/ad045772-84d4-44a6-b8c2-9976ee6deefa" />

<img width="1726" height="1180" alt="image" src="https://github.com/user-attachments/assets/325e9fc1-5c56-42f3-91f1-f2b749df91c1" />

Na egzaminie może pojawić się np. Pytanie aby przeskanować całą naszą sieć. Zrobilibyśmy to tak:

<img width="1735" height="1186" alt="image" src="https://github.com/user-attachments/assets/96b7fbd0-d15c-4b23-b19d-0b5f99029966" />

Jak z Wiresharkiem dam link do filimka na yt o Zenmapie ( GUI ).

[link](https://www.youtube.com/watch?v=wgNIva5nRjA)

> Wszystkie filmiki są krótkie i na temat.

### 7z_setup.exe
program 7-Zip jest stosunkowo łatwym w użytkowaniu programem, który na egzaminie może się pokazać jeśli mamy np. Zapakować lub Wypakować jakieś archiwum.

<img width="1075" height="1035" alt="image" src="https://github.com/user-attachments/assets/10999ae6-7b9a-42f3-867d-b27f7575bdbd" />

aby zapakować jakieś pliki do nowego archiwum należy wybrać nasze pliki i kliknąć guzik 'Dodaj'

<img width="52" height="49" alt="image" src="https://github.com/user-attachments/assets/e481cfe7-102d-43a2-8a6e-68ccfa147582" />

<img width="628" height="565" alt="image" src="https://github.com/user-attachments/assets/bcdb057c-5b62-460a-beeb-45dca3a646b0" />

<br>

<img width="85" height="22" alt="image" src="https://github.com/user-attachments/assets/dc8eeef4-3106-4854-98bd-602c456d06aa" />

<br>

Jeżeli chcemy zato Wypakować pliki z jakiegoś archiwum to po wybraniu tego archiwum klikamy guzik 'Wypakuj'

<img width="59" height="47" alt="image" src="https://github.com/user-attachments/assets/04e4d478-5cb8-4955-86a4-38f1e537d1e0" />
<img width="527" height="325" alt="image" src="https://github.com/user-attachments/assets/5cc118a1-48ae-4271-a8c7-dd696c65dc76" />

### VirtualBox_Setup.exe

<img width="1283" height="1033" alt="image" src="https://github.com/user-attachments/assets/fdb9fd86-2987-445e-9c5a-74437d486b4f" />

Virtual Box jest narzędziem słóżącym do virtualizacji systemów operacyjnych jeśli pokaże się na egzaminie oznacza to, że będzie najprawdobodobniej trzeba stworzyć na nim maszynę virtualną urzywając iso, które dostaniemy.

[Przykład Instalowania maszyny wirtualnej z ISO](https://www.youtube.com/watch?v=8ZS5AiKE0z8)

<strong>Znaczenia / dodatkowe rzeczy do różnych zadań:</strong>
```
putty.exe – jedyny sposób na połączenie się z ruterem przez kabel konsolowy. ( omówiony w folderze 'TP-link konfiguracja' )
Folder DRUKARKA – zawiera pliki .inf (np. dla HP LaserJet lub wirtualnej drukarki).
inf02.txt oraz inf03.txt – małe pliki tekstowe (często 0 KB), używane do zadań typu: "utwórz archiwum .tar w Linuxie" lub "nadaj uprawnienia NTFS".
index.html / test.html – prosta strona WWW do sprawdzenia działania roli serwera WWW (IIS lub Apache).
obraz.jpg, logo.png, baner.gif – pliki graficzne, które mają znaleźć się na Twojej stronie testowej.
skrypt.bat / skrypt.ps1 – gotowy szkielet skryptu, który musisz uzupełnić.
```
<strong>Jeśli na egzaminie nie będzie Worda / Excela na Kliencie należy szukać tych programów na pendrivie aby zainstalowac pakiet office.
- LibreOffice_Installer.msi 
- Apache_OpenOffice_Setup.exe.

> aida64_trial.exe – nie będzie omawiany.

## Programy, funkcje na Windowsie ( wbudowane )

<strong>Właściwości</strong>

<img width="398" height="627" alt="image" src="https://github.com/user-attachments/assets/eadee721-16a2-40f2-adc1-01e3baec8e13" />

<img width="346" height="63" alt="image" src="https://github.com/user-attachments/assets/af75bab4-9b33-4e9c-b088-1cd574572d22" />

To właśnie tutaj w właściwościach możemy zmienić wiele ustawień o, które pytają nas na INF02.

W pierwszej zakładcę możemy zmienić nazwę pliku , dodawać atrybuty.

<img width="450" height="480" alt="image" src="https://github.com/user-attachments/assets/fa921b89-b8d2-491c-82a0-c1685e7a1549" />


W Drugiej zakładce możemy udostępnić folder jako zasób sieciowy.

<img width="440" height="472" alt="image" src="https://github.com/user-attachments/assets/59d7048f-98b5-4b2e-8e50-9392613ea778" />

Przykład udostępniania folderu jako zasób sieciowy:



1. Wchodzimy do zakładki 'Udostepnianie' w właściwościach i kliamy guzik 'Udostępnj'
   
<img width="441" height="480" alt="image" src="https://github.com/user-attachments/assets/63ededc9-f446-459a-a021-be5b74293489" />

2. Klikamy 'Udostępnij' poraz kolejny 

<img width="619" height="456" alt="image" src="https://github.com/user-attachments/assets/284a216c-2b5c-4e14-9f17-17b65b71357b" />

3. kopiujemy link

<img width="612" height="442" alt="image" src="https://github.com/user-attachments/assets/25d22d60-0b12-41c9-b9ca-b330ddcbdb38" />

4. Klikamy 'Gotowe'

<img width="80" height="31" alt="image" src="https://github.com/user-attachments/assets/838ec78a-c80d-48d0-933a-871428501cce" />

5. Wchodzimy do eksploratora plików i wykonujemy prawoklik na 'Ten Komputer' -> 'Pokaż Więcej opcji' -> 'Mapuj Dysk Sieciowy'

<img width="396" height="375" alt="image" src="https://github.com/user-attachments/assets/4ee59d4c-ea72-46b2-95c8-9502c02559dd" />

<img width="616" height="448" alt="image" src="https://github.com/user-attachments/assets/129ee4ea-b034-4d1d-aed9-957683e3a4f5" />

6. Wklejamy naszą ścieżke a następnie dostosowujemy ją pod format o, który proszą nas na dole 

<img width="613" height="450" alt="image" src="https://github.com/user-attachments/assets/857b3bc6-5077-4f0b-88df-f30ca6424017" />

7. Po Zmienieniu ścieżki na poprawną klikamy Zakończ

<img width="616" height="447" alt="image" src="https://github.com/user-attachments/assets/2a108543-906c-4a0d-a1ac-af4fb5c48190" />

8. Jak widac nasz dysk się udostępnił w sieci.

<img width="1414" height="674" alt="image" src="https://github.com/user-attachments/assets/d0887e85-5c32-4b0e-b6b2-9ae425ea90b0" />

9. Dodatkowo w tym okienku można kliknąć w link 'Centrum Sieci i udostępniania' aby pozmieniać ustawienia tak aby było widać nasz folder na innych urządzeniach

<img width="437" height="472" alt="image" src="https://github.com/user-attachments/assets/d7113493-fbe1-4fc7-a058-0441dc567614" />

<img width="839" height="756" alt="image" src="https://github.com/user-attachments/assets/c3f29fa8-0e2b-4d90-b68d-72079afddee1" />



























































































































## Windows jako Klient




## Zadania praktyczne.

Windows-Klient
<img width="904" height="317" alt="image" src="https://github.com/user-attachments/assets/49ea49ad-eab6-461f-a11f-53ab5e7caae4" />
<img width="878" height="166" alt="image" src="https://github.com/user-attachments/assets/d5b3d1ea-2a4c-475b-8dcf-95d4aadd4cd3" />
<img width="894" height="988" alt="image" src="https://github.com/user-attachments/assets/6345da4d-31e7-412e-86ce-5172b3427052" />
<img width="897" height="815" alt="image" src="https://github.com/user-attachments/assets/34d6653f-3d51-42f5-b926-b089133134a4" />
<img width="881" height="280" alt="image" src="https://github.com/user-attachments/assets/5d125f9b-166e-4d54-88cf-c4f427a367be" />
<img width="896" height="413" alt="image" src="https://github.com/user-attachments/assets/13831b43-4e8c-4809-92e4-60b8caafa985" />
<img width="720" height="321" alt="image" src="https://github.com/user-attachments/assets/c114274d-f83a-448d-8a6b-8bee172907f0" />
<img width="703" height="492" alt="image" src="https://github.com/user-attachments/assets/a6ac2b05-49de-45bd-94e5-7567b9337558" />
<img width="718" height="472" alt="image" src="https://github.com/user-attachments/assets/1822b073-4947-43a2-9a3a-5f4ad3bb8af1" />
<img width="723" height="493" alt="image" src="https://github.com/user-attachments/assets/7b916a18-8084-4c89-8e5d-4ac9def4b5fe" />
<img width="713" height="424" alt="image" src="https://github.com/user-attachments/assets/9ca5f9e6-751a-46d6-9e54-f2057c83a095" />
<img width="722" height="420" alt="image" src="https://github.com/user-attachments/assets/a0fdc51e-6ee5-4b4e-89f5-e37abea0b54d" />
<img width="704" height="143" alt="image" src="https://github.com/user-attachments/assets/e9bcb17e-7e57-475b-8e9b-f464a38e048a" />
<img width="713" height="514" alt="image" src="https://github.com/user-attachments/assets/ed61e170-4f82-4b9a-a6d0-12969e070f14" />
<img width="724" height="688" alt="image" src="https://github.com/user-attachments/assets/2b823bdf-6547-4060-b2c1-2a7b2aa553c9" />
<img width="712" height="587" alt="image" src="https://github.com/user-attachments/assets/a09423ca-9127-416d-9134-67652319c49f" />
<img width="696" height="330" alt="image" src="https://github.com/user-attachments/assets/e02f5b20-9d85-40c4-a4ca-c5abccd3964c" />
<img width="741" height="247" alt="image" src="https://github.com/user-attachments/assets/8a18d8c8-a3e5-4398-9c82-0fdd5a1737d8" />
<img width="725" height="241" alt="image" src="https://github.com/user-attachments/assets/08d6680d-3b25-4235-adfe-8d989786bf0b" />
<img width="736" height="209" alt="image" src="https://github.com/user-attachments/assets/5295bf0f-60c8-4070-9348-22dfa696d985" />
<img width="745" height="248" alt="image" src="https://github.com/user-attachments/assets/36cdf1d4-31d3-4631-bf1a-1f22304b7e12" />
<img width="749" height="370" alt="image" src="https://github.com/user-attachments/assets/aa829c67-f575-4fdb-8098-4871ea984027" />
<img width="738" height="59" alt="image" src="https://github.com/user-attachments/assets/a479358a-2afb-470d-b334-9d0554b714b7" />
<img width="746" height="296" alt="image" src="https://github.com/user-attachments/assets/a0da5c36-318b-4843-9557-a7d67a8abc7d" />
<img width="751" height="258" alt="image" src="https://github.com/user-attachments/assets/eaf82dce-b381-4efe-8b5a-eb58634cdaf9" />
<img width="761" height="216" alt="image" src="https://github.com/user-attachments/assets/6c69881c-a39e-4418-b08b-f1a7a5e6a96f" />
<img width="738" height="245" alt="image" src="https://github.com/user-attachments/assets/3eba12c3-ae8b-497e-a59a-7845329a5e7a" />
<img width="616" height="442" alt="image" src="https://github.com/user-attachments/assets/aee420a3-ae0e-4724-993d-932d91a7f6ae" />
<img width="576" height="281" alt="image" src="https://github.com/user-attachments/assets/793c8a18-8ae7-400e-936b-8935dfcc90d3" />
<img width="1167" height="1145" alt="image" src="https://github.com/user-attachments/assets/45337493-68c2-4dc9-938f-1fa99361fe54" />
<img width="940" height="405" alt="image" src="https://github.com/user-attachments/assets/4daaf309-79b6-4abc-9490-f3b5a43c1d78" />


Windows-Server
<img width="893" height="652" alt="image" src="https://github.com/user-attachments/assets/225b42ff-bdcf-47b4-97d2-18f2190401dc" />
<img width="905" height="728" alt="image" src="https://github.com/user-attachments/assets/c9843ec9-c758-461a-b3d4-2c56f3f99204" />
<img width="874" height="745" alt="image" src="https://github.com/user-attachments/assets/1430fe32-aecf-4815-a7f0-26b3ff8670bc" />
<img width="715" height="406" alt="image" src="https://github.com/user-attachments/assets/44f27e45-a3be-4499-9d17-5160feeb7bf6" />
<img width="888" height="673" alt="image" src="https://github.com/user-attachments/assets/ca3cf13a-e4ac-491f-a544-6e10692bc470" />
<img width="888" height="1007" alt="image" src="https://github.com/user-attachments/assets/4dfc0b71-1e4d-4694-b00f-ae2bd61d37b6" />
<img width="903" height="941" alt="image" src="https://github.com/user-attachments/assets/ebd6cd5c-f264-477a-8b83-56127f5a5ffa" />
<img width="893" height="494" alt="image" src="https://github.com/user-attachments/assets/1677ac74-aadb-4f48-9427-34a0d727897f" />
<img width="917" height="1137" alt="image" src="https://github.com/user-attachments/assets/1f49bfce-7885-46aa-bee8-e6237d56ea85" />
<img width="919" height="687" alt="image" src="https://github.com/user-attachments/assets/2e583141-b070-498b-aa32-70a3e97469f6" />
<img width="905" height="1071" alt="image" src="https://github.com/user-attachments/assets/b74f4db7-50fb-4b9e-b4b7-b278449f0f79" />
<img width="888" height="737" alt="image" src="https://github.com/user-attachments/assets/49af2472-5ebb-455b-86b6-d4668d88802b" />
<img width="888" height="1085" alt="image" src="https://github.com/user-attachments/assets/8051e123-a8cd-4f32-8c60-9f11bb5f9bd0" />
<img width="728" height="860" alt="image" src="https://github.com/user-attachments/assets/15b4a737-4944-4672-9588-6c7e4a9eb8ff" />
<img width="717" height="336" alt="image" src="https://github.com/user-attachments/assets/a5db0ccd-7aa3-4990-9b8a-026f08f049fc" />
<img width="727" height="524" alt="image" src="https://github.com/user-attachments/assets/a0bd891c-0920-4b71-83fe-ec43be33e29c" />
<img width="715" height="649" alt="image" src="https://github.com/user-attachments/assets/f6d13fa1-1984-4d67-b375-511bcb69f4ed" />
<img width="713" height="819" alt="image" src="https://github.com/user-attachments/assets/6380c641-de19-43d6-853f-4a487bbb6515" />
<img width="717" height="937" alt="image" src="https://github.com/user-attachments/assets/9fafa350-cb6d-461f-b81d-ebf1584b88bb" />
<img width="725" height="896" alt="image" src="https://github.com/user-attachments/assets/bbd5b486-0a86-4f4d-9b76-fe46cf40f0a5" />
<img width="747" height="453" alt="image" src="https://github.com/user-attachments/assets/acb86654-df2b-481d-9627-6d8a11ce6737" />
<img width="735" height="454" alt="image" src="https://github.com/user-attachments/assets/fc90ad73-54fd-4c60-b95a-fd11a4400d00" />
<img width="724" height="377" alt="image" src="https://github.com/user-attachments/assets/0047f321-8750-4e97-9b60-4dec8c447314" />
<img width="747" height="621" alt="image" src="https://github.com/user-attachments/assets/68bc33d5-ebdb-4ae6-8ce4-1a88bdb8548a" />
<img width="735" height="358" alt="image" src="https://github.com/user-attachments/assets/ab92e22f-e2a9-4527-bd35-f3ff03d5a8d4" />
<img width="747" height="214" alt="image" src="https://github.com/user-attachments/assets/8883e5cb-648b-43fc-bea2-178ee0359982" />
<img width="737" height="368" alt="image" src="https://github.com/user-attachments/assets/3eec10bc-b35a-41e8-9ba8-ff960f55cfde" />
<img width="757" height="631" alt="image" src="https://github.com/user-attachments/assets/7c1dd24d-d47a-4ffc-9bac-cf6d8ea98d66" />
<img width="763" height="809" alt="image" src="https://github.com/user-attachments/assets/eb66cf69-da68-475e-8ff7-9539b1f338fa" />
<img width="759" height="813" alt="image" src="https://github.com/user-attachments/assets/5ddef8eb-4b53-4ce4-9a77-f7a13cdd7970" />
<img width="755" height="212" alt="image" src="https://github.com/user-attachments/assets/c2fae318-cba3-453f-831d-0d62c7f7f56f" />
<img width="814" height="413" alt="image" src="https://github.com/user-attachments/assets/c326423d-f707-4f72-8b2f-5d83c3e8eb35" />
<img width="1049" height="757" alt="image" src="https://github.com/user-attachments/assets/fb1ee090-7c00-4c3a-a852-df5bbf052337" />



Diagnostyka na Windowsie
<img width="895" height="373" alt="image" src="https://github.com/user-attachments/assets/642f5a7d-9f98-4893-9d9e-2544af01c9ed" />
<img width="921" height="734" alt="image" src="https://github.com/user-attachments/assets/8801b7c6-681b-42ac-860d-f5bce201a967" />
<img width="875" height="409" alt="image" src="https://github.com/user-attachments/assets/61f89201-587f-4088-b65e-c4cb701dfe52" />
<img width="893" height="376" alt="image" src="https://github.com/user-attachments/assets/c2e8d23b-4325-463a-b12f-76b310b1e676" />
<img width="852" height="152" alt="image" src="https://github.com/user-attachments/assets/8f35a64f-3700-4a18-8e8f-3472a4f54cc4" />
<img width="868" height="473" alt="image" src="https://github.com/user-attachments/assets/fae80dee-157c-4540-9a9f-7e00720ae312" />
<img width="732" height="328" alt="image" src="https://github.com/user-attachments/assets/a8797d08-59ce-4a64-b784-0500fac1529e" />
<img width="712" height="148" alt="image" src="https://github.com/user-attachments/assets/8658a5e2-eea3-4f9e-9fad-f620eca2e85c" />
<img width="709" height="192" alt="image" src="https://github.com/user-attachments/assets/8fd45a3e-1f8b-44e8-8beb-24514007afb9" />
<img width="695" height="331" alt="image" src="https://github.com/user-attachments/assets/0d45400a-b251-4af1-87cb-8393f2836a96" />
<img width="695" height="179" alt="image" src="https://github.com/user-attachments/assets/df9ebf15-bcc2-488e-bb35-f0a64b2a1502" />
<img width="708" height="297" alt="image" src="https://github.com/user-attachments/assets/104051bc-3359-491a-be5f-26308acfcf96" />
<img width="704" height="216" alt="image" src="https://github.com/user-attachments/assets/eb6d16ab-f919-4ae7-8202-be7a719f85b1" />
<img width="718" height="281" alt="image" src="https://github.com/user-attachments/assets/a0b6a0e1-faf7-4e02-8477-b1817ea18d48" />
<img width="738" height="122" alt="image" src="https://github.com/user-attachments/assets/0c5d6855-6cf4-4823-b1d5-e5dc9c89a7d9" />
<img width="728" height="197" alt="image" src="https://github.com/user-attachments/assets/8bde67ff-2f8e-4b99-8b1a-41e4f3db30df" />
<img width="735" height="115" alt="image" src="https://github.com/user-attachments/assets/f6258302-fbdc-4222-b232-2f731854bd3a" />
<img width="713" height="573" alt="image" src="https://github.com/user-attachments/assets/899469f5-34a1-4d20-83f8-8260d6d0c5ba" />
<img width="738" height="120" alt="image" src="https://github.com/user-attachments/assets/dcb3b339-1b14-4fc8-8ad7-fd11e5d08d9e" />
<img width="718" height="246" alt="image" src="https://github.com/user-attachments/assets/089905ed-5370-49ff-a403-c8049dfcac85" />
<img width="761" height="361" alt="image" src="https://github.com/user-attachments/assets/cefb6d4f-3804-4ca0-99a1-3f6025ddb358" />
<img width="776" height="601" alt="image" src="https://github.com/user-attachments/assets/5af37a57-1e90-43a2-b482-0c40083ede2a" />
<img width="859" height="631" alt="image" src="https://github.com/user-attachments/assets/619b7c8e-a2e4-4cf9-9751-08c1930542d1" />
<img width="1032" height="925" alt="image" src="https://github.com/user-attachments/assets/2b04eb7d-5544-4f99-ab52-8640e4185b1a" />
<img width="1024" height="207" alt="image" src="https://github.com/user-attachments/assets/e5bb417a-3651-4fbe-81db-c9ddc09eed30" />
<img width="1071" height="654" alt="image" src="https://github.com/user-attachments/assets/57511f37-736e-466c-ae74-ac0d7d573f9f" />
<img width="1054" height="295" alt="image" src="https://github.com/user-attachments/assets/62002560-30b4-4c3a-ab88-7402e94c9f87" />
<img width="1036" height="793" alt="image" src="https://github.com/user-attachments/assets/35b0714f-7e28-4156-ac05-52fb7ad8ecf2" />

























> dodać normy EN 50174

