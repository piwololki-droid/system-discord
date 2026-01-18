# system-discord
Pomysł na queue:
1. Action PAY (gracz zlecił o 1:00:13) -> wykonanie o 1:00:18
2. MESSAGE (gracz napisal saldo o 1:00:14) -> wykonanie o 1:00:20
3. MESSAGE (gracz napisal cf o 1:00:15) -> wykonanie o 1:00:22
4. Action PAY (gracz zlecił o 1:00:17) -> wykonanie o 1:00:27
komenda orzeł/reszka 1000 pierwszenstwo nad wszystkim
Komendy bota: 
- saldo -> sprawdza saldo gracza w bazie danych
- cf -> wysyła graczowi informacje o możliwości gry "Coinflip: /msg kasynodiscord [orzel/reszka] [kwota] -> Grasz z botem w CF -> dostajesz info na /msg o tym czy wygrałeś czy przegrałeś ZINTEGROWANE Z DISCORD [wyniki gier] [brak cooldownu na komendę orzel/reszka kwota] [cooldown 2 sec na wiadomosci czy gracz wygrał czy nie]
- wyplac [saldo] -> [cooldown 1 min, obsługuje jedną wiadomość od konkretnego gracza na minutę] Sprawdza czy gracz ma w bazie danych odpowiednią ilość salda zeby wyplacić ->
- jezeli nie ma "Twoje saldo:" wysyła na /msg jezeli ma to dodaje do kolejki i realizuje [antibot system 5,5 sec] [plus błędy czyli error 0,1,2,3 odpowiednio jak wyskoczy na czacie:
0 -> Nie posiadasz tylu pieniędzy!
1 -> Nie odnaleziono takiego gracza na serwerze!
2 -> Nastepna komende możesz wpisać na [liczba]ms!
  jak gracz nie ma salda:
3 -> Gracz nie ma salda
  wszystkie błędy kieruje na kanał #admin -> 1462240962234286201

  
Funkcje:
Pełne Logowanie [nie ruszać!] -> auth.js 
Komendy admina [DC] -> admin.js
Czytanie balance z scoreboard, konwersja kasy-> balancemc.js
Parowanie konta MC i DC -> code.js
Coinflip Discord -> granie w CF na discord odpowiedni embed ->coinflip.js
Coinflip Minecraft -> granie w CF przez grę Minecraft, odrazu informacja o wygranej/przegranej -> coinflipmc.js
Obsługa klienta (dostępne komendy, wypłata, parowanie konta, sprawdzanie salda, nieznana komenda i ich delaye) -> commands.js
Tworzenie niezbędnych tabel w bazie danych -> database.js
Budowanie embed na Discord -> embed.js
Centralny system zarządzania kolejką wiadomości -> queue.js
System Statusu (Stock): Na bieżąco aktualizuje informację o tym, czy bot jest Online/Offline na specjalnym kanale Discord (STATUS_CHANNEL_ID) -> stock.js
Przepływ gotówki między serwerem Minecraft a bazą danych kasyna. ->transactions.js
Ręczne nadzorowania przepływów pieniężnych, których bot nie jest pewien. -> verifycash.js







 == MINECRAFT.JS ==
Pełni rolę pośrednika komunikacyjnego między serwerem Minecraft a resztą systemu.
Zarządzanie połączeniem (Mineflayer): Inicjuje bota, obsługuje automatyczne restarty (co 15 sekund w przypadku rozłączenia) oraz bezpieczne zamykanie procesu z aktualizacją statusu na Discordzie.
Automatyzacja Logowania (Auth): Obsługuje proces wejścia na serwer (akceptacja resource packa, przechodzenie przez lobby, weryfikacja pozycji/ruchu) aż do momentu pełnego zalogowania do trybu gry.
System Statusu (Stock): Na bieżąco aktualizuje informację o tym, czy bot jest Online/Offline na specjalnym kanale Discord (STATUS_CHANNEL_ID).
Przechwytywanie Wiadomości Prywatnych (/msg): Wykrywa szepty od graczy w różnych formatach (-> ja, szepcze:, -> kasynodiscord), wyodrębnia nick nadawcy oraz treść i przekazuje je do centralnego procesora komend (commands.js).
Obsługa Transakcji Finansowych:
Wpłaty: Wykrywa przychodzące przelewy od graczy i przekazuje je do księgowania w bazie.
Weryfikacja Wypłat: Monitoruje czat pod kątem potwierdzeń wykonania komendy /pay przez bota (sprawdza sukcesy lub błędy typu "ms!").
Nawigacja po zalogowaniu: Automatycznie wykonuje komendę /home po 5 sekundach od poprawnego zalogowania do trybu, aby bot znalazł się w bezpiecznym miejscu.
Zgodnie z Twoim nowym plikiem queue.js, to właśnie tutaj w punkcie 2 wywoływana jest funkcja commands.handleCommand, która ustawia zadania w kolejce 2s/5.5s.

