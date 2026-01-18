# system-discord

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
