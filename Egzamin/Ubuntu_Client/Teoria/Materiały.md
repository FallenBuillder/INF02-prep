# Teoria

Linux jest bardziej skomplikowany niż Windows ponieważ w windowsie możemy sobie coś tam przeklikać i nawet jak nic nie wiemy to można dojść do celu. Na linuxie jest inaczej ponieważ jeśli chcemy cośz robić musimy znać do tego komendę.

Zagadnienia:

- Podstawowe Komendy w linuxie
- Sprawdzanie parametrów systemowych w Linuxie 
- Linux jako client, któremu są świadczone usługi

## Komendy w linuxie

Jeśli nie mamy skonfigurowanego pod nas środowiska to aby coś zrobić w linuxie trzeba znać w nim komendy. Niektóre komendy są proste i będziemy ich używać niemal ciągle podczas konfiguracji systemu z linuxem a niektóre rzadziej jeśli mamy zrobić jakąś konkretną rzecz.

- cd
- pwd
- ls
- mkdir
- rm
- touch
- chage
- passwd
- less
- chmod
- chown
- cat
- man
- date
- uptime
- alias
- history


pwd - wyświetla bieżący katalog (print working directory)

cd - zmiana katalogu
cd /home - przejście do katalogu /home
cd .. - przejście o jeden katalog w górę
cd ~ - przejście do katalogu domowego użytkownika

ls - wyświetlanie zawartości katalogu
ls -l - szczegółowy widok (długi format)
ls -la - widok wszystkich plików (także ukrytych)
ls -la | grep nazwa - filtrowanie wyników

mkdir nazwa - tworzenie nowego katalogu

touch nazwa_pliku - tworzenie pustego pliku

cp plik1 plik2 - kopiowanie pliku
cp -r katalog1 katalog2 - kopiowanie katalogu rekursywnie

mv plik1 plik2 - przenoszenie/zmiana nazwy pliku

rm plik - usuwanie pliku
rm -rf katalog - usuwanie katalogu rekursywnie

rmdir katalog - usuwanie pustego katalogu

  


