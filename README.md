# Sieci Projekt komunikator IRC



## Opis zadania

Komunikator tekstowy oparty na pokojach. Użytkownicy mogą tworzyć pokoje (z opcjonalnym hasłem). Użytkownicy mogą dołączyć do pokojów i wysyłać wiadomości, które widzą wszyscy uczestnicy pokoju. Twórca pokoju może zablokować poszczególnych użytkowników od dostępu do pokoju.

## Protokół komunikacyjny


Po nawiązaniu połączenia serwer prosi klienta o dane logowania.
Po zalogowaniu klient może uzyskać dane z serwera wysyłając komendy:
 - `/rooms` wysyła klientowi listę wszystkich pokojów.
 - `/create <name> <pwd>` tworzy pokój o danej nazwie z opcjonalnym hasłem.
 - `/join <name> <pwd>` dołącza klienta do danego pokoju, i przesyła mu historię wiadomości z pokoju.
 - `/leave` rozłącza klienta z aktualnego pokoju.
 - `/remove <name>` usuwa dany pokój. Tylko twórca pokoju ma do tego uprawnienia.
 - `/ban <room> <user>` blokuje dostęp użytkownika do pokoju. Tylko twórca pokoju ma do tego uprawnienia.
 - Jeżeli klient jest w pokoju to wiadomość jest wysłana do pokoju i wszystkich jego członków.


## Opis implementacji i plików źródłowych


Projekt wykorzystuje model klient-serwer i korzysta z protokołu TCP, i epoll do współbierznej obsługi klientów. 

Źródła:

W katalogu `server/`:
 - `IRCsv.c` zawiera kod źródłowy serwera, obsługuje klientów, zarządza pokojami i wiadomościami.

W katalogu `client/`:
 - `IRCCLient.py` zawiera klienta w wesji z wiersza poleceń używanego do testowania, nie jest potrzebny do interfejsu graficznego.

 - `gui_style.py` zwiera definicje klas interfejsu graficznego dla poszczególnych ekranów aplikacji.
 - `irc_core.py` obsługuje gniazdo sieciowe i wymianę danych z serwerem.
 - `style_sheet.py` przechowuje arkusz danych dotyczących wyglądu interfejsu.
 - `main.py` główny plik aplikacji klienta, uruchamia GUI i wysyła odpowiednie komendy do serwera poprzez fukncje z irc_core.py.

 

## Kompilacja

By skompilować serwer na maszynie Linux: `gcc -Wall IRCsv.c -o IRCsv.o`
By uruchomić serwer: `./IRCsv.o`

By uruchomić klient na maszynie Windows/Linux:
Potrzeba mieć zainstalowane bilbioteki zawarte w requirements.txt:

`pyside6==6.10.1`

`pyside6_addons==6.10.1`

`pyside6_essentials==6.10.1`

W 39 linijce `main.py` trzeba ustawić adres ip na ten na którym uruchomiony jest serwer. Port jest domyślnie 1234.

A następnie uruchomić poprzez `python3 main.py`

