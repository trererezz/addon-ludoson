LUDOS-on 0.4.1 – premiera WoW Forever (5.11.2026)
==================================================

W paczce dwa foldery add-onów:
  LUDOS-on          – dla KAŻDEGO gracza (zbiera dane, wysyła je oficerom)
  LUDOS-on_Odbior   – TYLKO dla oficerów i mastera (magazyn danych odebranych od graczy)

Działa na: WoW Forever (interface 16001), Classic Era / Anniversary (11509), TBC Anniversary (20506),
retail 12.1.5 (120105, do testów). Add-on sam rozpoznaje grę.


Instalacja
----------
1. Zamknij grę (albo instaluj przed uruchomieniem).
2. Rozpakuj zip. Foldery LUDOS-on i LUDOS-on_Odbior skopiuj do folderu add-onów TEJ gry, w którą grasz:
     World of Warcraft\_forever_\Interface\AddOns\        (WoW Forever – nazwę folderu sprawdź u siebie)
     World of Warcraft\_classic_era_\Interface\AddOns\    (Classic Era)
   Gracz kopiuje tylko LUDOS-on. Oficer i master – oba foldery.
   Folder Interface\AddOns może nie istnieć przy świeżej instalacji – utwórz go.
3. Stare foldery LUDOS-on i LUDOS-on_Odbior (0.3.x) zastąp nowymi. Dane w WTF zostają.
4. W grze, na ekranie wyboru postaci: przycisk „AddOns” (lewy dolny róg) – oba add-ony zaznaczone.
   Jeśli gra pokazuje „Nieaktualne” (out of date), zaznacz „Wczytuj nieaktualne add-ony”.
5. Po wejściu na czacie: „LUDOS-on v0.4.1 zaladowany. Sesja N, rola: …”.

Gdzie gra trzyma add-ony
------------------------
Każda wersja WoW ma własny folder z add-onami i własne pliki zapisu:
  _retail_\Interface\AddOns\       _retail_\WTF\...
  _classic_era_\Interface\AddOns\  _classic_era_\WTF\...
  _forever_\Interface\AddOns\      _forever_\WTF\...
Gra wczytuje add-ony WYŁĄCZNIE ze swojego folderu. Add-on w _classic_era_ nie działa w Forever i odwrotnie.
Ten sam folder add-onu można skopiować do kilku gier – plik .toc podaje kilka wersji interfejsu
(„## Interface: 11509, 20506, 16001, 120105”), więc każda gra uzna go za swój.
Dane LUDOS-on są osobne dla każdej gry (osobne WTF).

Plik z danymi: World of Warcraft\_forever_\WTF\Account\<KONTO>\SavedVariables\LUDOS-on.lua
(u oficera dodatkowo LUDOS-on_Odbior.lua; ścieżkę pokazuje /ludos → Informacje).


Kto jest odbiorcą
-----------------
Odbiorcy = członkowie gildii z rangą 0 (mistrz) i 1 (oficerowie), wg listy gildii z serwera.
Nic nie trzeba wpisywać. Edycja pliku u gracza nic nie da – każdy nadawca sprawdza rangę u siebie.
Oficer, który nie chce odbierać danych na swoim komputerze: /ludos → Ustawienia → odznacz
„Odbieram dane od graczy”.
Zanim powstanie gildia, dane zbierają się u każdego gracza i pójdą same po dołączeniu do gildii.


Co nowego w 0.4.1 (ilość danych na komputerach)
-----------------------------------------------
 1. Gracz: dane add-onu najwyżej ok. 10 MB. Ponad limit przy wejściu do gry znikają najstarsze sesje,
    które co najmniej jeden oficer odebrał w całości. Sesji niewysłanej do żadnego oficera add-on
    nie usuwa nigdy (wtedy komunikat na czacie). Wielkość: /ludos → Informacje („Dane add-onu”).
    10 MB to ok. 50 tys. wierszy, ok. 120 h gry. Wpis DIAG „sprzatanie” mówi, ile usunięto.
 2. Wymiana: każda sesja idzie do najwyżej 2 oficerów (pierwszych, którzy odpowiedzą). Gdy obaj mają ją
    w całości, nie idzie do kolejnych. Oficer, który nie odpowiada od 30 min, zwalnia miejsce dla następnego.
 3. Odbior (oficer): limit ok. 50 MB. Ponad limit przy wczytaniu znikają najstarsze paczki, które były
    w pliku przy co najmniej 2 kolejnych wczytaniach (uploader zdążył je wysłać) i mają ponad 24 h.
    Licznik „ile wierszy mam” zostaje, więc gracz nie wysyła ich od nowa. Gdy mimo to jest ponad
    limitem – ostrzeżenie „sprawdź, czy uploader działa”. Wielkość: /ludos → Informacje.
    WAŻNE: odbiór włączony tylko u oficerów z działającym uploaderem.
 4. Odbiorcy 0.4.0 i 0.4.1 dogadają się (ten sam protokół), ale reguła 2 oficerów działa tylko u graczy z 0.4.1.

Co nowego w 0.4.0 względem 0.3.1
--------------------------------
 1. Forever: combat log jest tam zablokowany dla add-onów. Zamiast niego:
    – WALKA: po walce add-on czyta wbudowany licznik obrażeń gry (zadane, otrzymane, leczenie,
      top 5 czarów jako ID:obrażenia); zrodlo = "licznik". W Classic bez zmian (zrodlo = "combatlog").
    – ZABOJSTWO w świecie: zdarzenie PARTY_KILL (gra podaje GUID moba); czas do zabicia od wejścia
      w walkę albo od wzięcia moba w cel (ttk_z = walka / cel).
    – ZABOJSTWO w lochu (GUID ukryte): komunikat „X dies, you gain N experience”; NPC ID z lootu.
    – SMIERC: z podsumowania śmierci gry (zabójca, czar, do 5 trafień); zrodlo = "recap".
    – Exp za moba (exp, rested) dopisywany do zabójstwa i do wiersza EXP.
 2. PvP: WROG_SPOTKANY (gracz wrogiej frakcji w celu / pod myszką / z tabliczką – raz na 15 min,
    z gildią, poziomem, klasą, rasą, miejscem), PVP_ZABOJSTWO (kogo zabiliśmy, z jakiej gildii, honor),
    PVP_SMIERC (kto nas zabił, czym, z jakiej gildii). Pomijane na BG i arenach.
 3. DIAG: raz na sesję (wersja gry, co jest dostępne), próbki odpowiedzi gry, liczniki błędów
    i ukrytych wartości przy reloadzie / wylogowaniu. Moduł, który 5 razy zgłosi błąd, wyłącza się sam.
 4. Zbieranie danych zawsze włączone (usunięta opcja). Odbiorcy wg rangi (patrz wyżej).
 5. Wymiana szybsza: paczki po 100 wierszy, jedno potwierdzenie zbiorcze, osobna etykieta dla
    wiadomości sterujących, pauza, gdy gra blokuje czat add-onów (boss, walka).
 6. Stan zapisu: widget z boku „w pamieci N zdarzen, od zapisu X min” (zielony / żółty / czerwony).
    Podpowiedź na czacie w locie / przy zmianie kontynentu (najwyżej co 10 min, ≥ 10 min od zapisu),
    okienko z przyciskiem „Zapisz teraz (/reload)” z boku ekranu (najwyżej co 30 min, nigdy w walce).
 7. Gildia: zrzut listy gildii u oficerów przy wejściu, wylogowaniu i reloadzie (≥ 1 h od poprzedniego)
    oraz /ludos zrzut. Dołączył / odszedł – u wszystkich; awans, degradacja, wyrzucony, online/offline –
    u oficerów.
 8. Killtracker: widget TESTOWY, domyślnie wyłączony (/ludos kt albo /ludos → Widgety).
 9. Poprawka sesji: wznowienie tylko po reloadzie i gdy ostatni wpis ma < 10 min.
10. /ludos sonda pokazuje też serwer, blokady add-onów, licznik obrażeń, ID gildii.

UWAGA: 0.4.x nie dogada się z 0.3.x (nowy protokół). Wszyscy w gildii muszą mieć 0.4.x (najlepiej 0.4.1).


Komendy
-------
  /ludos                okno (Informacje, Ustawienia, Widgety, Magazyn, Odbior, Pomoc)
  /ludos status         podsumowanie sesji
  /ludos zapisz         zapis danych (/reload)
  /ludos wymiana        stan wysyłania i odbierania
  /ludos wyslij         ogłoś stan danych oficerom teraz
  /ludos zrzut          ręczny zrzut listy gildii (tylko oficer z włączonym odbiorem, raz na minutę)
  /ludos zw             pokaż / ukryj widget stanu zapisu
  /ludos kt             pokaż / ukryj Killtracker (testowy)
  /ludos przypomnij     pokaż okienko przypomnienia (test)
  /ludos odbiorca lista lista dodatkowych odbiorców (zmiany: tylko master)
  /ludos sonda          co podaje gra (na prośbę mastera; nic nie zapisuje)
  /ludos debug          na czacie, co zapisuje add-on (dla dewelopera)
  /ludos pomoc          lista komend


Najważniejsza zasada
--------------------
Gra zapisuje plik tylko przy /reload, wylogowaniu i wyjściu z gry. Crash = utrata wszystkiego od
ostatniego zapisu. Dobry moment na /reload: lot taksówką, zeppelin, statek.
Uploader u oficera wysyła pliki na serwer sam po każdym zapisie.
