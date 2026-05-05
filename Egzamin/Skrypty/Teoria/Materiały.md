# Skrypty
w ostatnich latach na egzaminach INF02 coraz częściej pojawiają się skrypty powłoki ( bash ) i skrypty wsadowe ( bat ) w tej sekcji omówimy wszystkie przykłady z egzaminów w ,których występowało zadanie z napisaniem tego typu skryptów oraz nauczymy cię jak je pisać.
> Powoli na egzaminach INF02 odchodzi się już od arkuszy kalkulacyjnych i zastępuje się je skrypytami !






Skrypty z 2021-2026 roku 
<br>
<img width="677" height="237" alt="image" src="https://github.com/user-attachments/assets/86818d59-7f47-4036-b29c-c898512017e0" />
Rozwiązanie:

<br>

nano konfiguracja.sh

#!/bin/bash

groupadd informatycy

usermod -aG informatycy administrator

groupmod -g 1111 informatycy

chmod +x konfiguracja.sh
sudo ./konfiguracja.sh
> tar -cvf konfiguracja.tar konfiguracja.sh - dodatkowo jeszcze jest tutaj utworzenie archiwum. ( Komendy tego typu będą znajdować się w pliku 'Windows-Client','Windows-Server'





<img width="674" height="180" alt="image" src="https://github.com/user-attachments/assets/00699952-3a05-4725-a9ab-6df479a2ee68" />
<img width="677" height="135" alt="image" src="https://github.com/user-attachments/assets/0c5ae09f-ace7-4cef-bf42-aa7047aea66a" />


Skryprt z 2026 roku
<img width="896" height="330" alt="image" src="https://github.com/user-attachments/assets/518f74e5-a41a-4860-a8cf-3741d242d72c" />
<img width="777" height="455" alt="image" src="https://github.com/user-attachments/assets/370a6132-a0cb-4237-9b8d-f0c4682ed9dd" />
<img width="1191" height="441" alt="image" src="https://github.com/user-attachments/assets/59ca4c35-8ed2-4aa7-bc16-d3496447aab5" />

