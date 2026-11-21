---
name: mapit
description: Rozpisuje plan dowolnego przedsięwzięcia (kod, migracja, przeprowadzka, trening, wydarzenie) na etapy w plikach docs/plans/<slug>/, pytając po jednym pytaniu z rekomendacją; potem wykonuje etapy z bramką i weryfikacją oraz odpowiada na pytania o stan planu. Może startować od pomysłu odłożonego przez _parkit (docs/backlog/). Map it out, zaplanuj, rozpisz na etapy, co dalej w planie. NIE używaj do ticketów w Jira/ADO ani do zwykłej listy TODO w rozmowie.
---

# _mapit

Plan w etapach, w plikach, z możliwością przerwania i wznowienia. Trzy fazy: **plan**, **wykonanie**, **zapytanie**. Rozpoznawaj je z intencji. Rozmowa w języku użytkownika, zwięźle. Treść plików w języku rozmowy, chyba że reguły projektu każą inaczej. Nazwy plików: angielski, kebab-case.

**Tryb:** domyślnie `interactive`. Gdy użytkownik prosi o pracę samodzielną (`samodzielnie`, `bez pytań`) — `autonomous`: nie pytaj, wybieraj rekomendację i zapisuj decyzję z dopiskiem `autonomicznie`. Wyjątek: rzeczy wymagające zgody użytkownika (patrz Zasady) i fakty, które zna tylko on.

## Lokalizacja

- Reguły projektu (`CLAUDE.md`/`AGENTS.md`) wskazują katalog planów → użyj go.
- Inaczej w repo: `<korzeń repo>/docs/plans/<slug>/`, archiwum `docs/plans/archive/<slug>/`. Repo = to, którego plan dotyczy (wskazane albo repo pliku backlogu), nie zawsze katalog roboczy.
- Poza repo → zapytaj; rekomendacja `./plans/<slug>/`.

## Faza 1 — Plan

### Start

- Katalog planu istnieje → czytaj `README.md` i kontynuuj. `Planning: draft` → zadaj pierwsze otwarte pytanie; nie pytaj ponownie o rozstrzygnięte. Zmianę zapisanej treści pokaż jako diff przed zapisem.
- Start od pomysłu z `docs/backlog/` (plik `_parkit`) → użyj go jako wejścia: cel, proponowane rozwiązanie, kryteria, otwarte pytania (do kolejki pytań), powiązane pliki (sprawdź aktualność). W README wpisz `Źródło: <ścieżka>`.
- W repo z kodem przeczytaj reguły projektu i istotny kod (Grep/Glob najpierw). Reguły projektu wygrywają z domysłami.
- `README.md` utwórz z `Planning: draft` po pierwszej odpowiedzi i aktualizuj po każdej — przerwana sesja nic nie traci.

### Pytania

- **Jedno pytanie na wiadomość**, `AskUserQuestion`, 2–4 opcje, rekomendowana **pierwsza** z `(Recommended)` i powodem w opisie.
- Każda decyzja dostaje stały numer `Q<n>` i trafia do „Decyzje” w README.
- Pytaj tylko o to, co zmienia plan. Pomijaj to, co rozstrzyga kontekst. Nie wymyślaj faktów o użytkowniku (budżet, terminy, ograniczenia) — zapytaj albo zapisz jako założenie.
- Koniec pytań, gdy jasne są cel, zakres, kryteria i podział na etapy. Podsumuj decyzje jedną krótką listą.

### Etapy

- Domyślnie jeden etap. Dziel tylko przy realnej zależności albo sprawdzalnym stanie pośrednim (w planach rozłożonych w czasie: naturalne fazy). Podział potwierdź jednym pytaniem.
- Numeracja `01`, `02`… w kolejności wykonania. **Numerów nie zmieniaj**; etap dodany później dostaje kolejny wolny numer.
- Każdy etap ma wykonawcę: `agent` (Claude), `user` (człowiek) albo `mixed`.

### Pliki

`README.md` — indeks i stan:

```markdown
# <Tytuł>
Cel: <1–3 zdania>
Planning: draft | complete
Źródło: <zdanie z rozmowy | docs/backlog/<plik>.md>

## Otwarte pytania
## Etapy
| NN | Etap | Wykonawca | Status | Weryfikacja |
## Decyzje
- Q1: <decyzja> (<powód>)
## Założenia
- <założenie> (pomiń sekcję, gdy brak)
```

Status etapu: `planned` / `in progress` / `gaps` / `done`.

`NN-<etap>.md` — spec:
- Cel (1–3 zdania); Zakres w / poza (jawnie); Decyzje (`Q<n>`)
- Plan szczegółowy — treść merytoryczna, o którą prosił użytkownik (rozpiska, harmonogram, lista), jeśli etap jej wymaga
- Kryteria akceptacji — obserwowalne, jako checkboxy `- [ ]` (w kodzie: testy, kontrakty, pliki; poza kodem: sprawdzalny fakt)
- Weryfikacja — w kodzie testy do uruchomienia (najwęższe najpierw); poza kodem: jak użytkownik potwierdzi
- Pliki / materiały (ścieżki); nota o wersji/CHANGELOG, jeśli wymagają tego reguły projektu
- Zależy od: poprzedni etap (`done`)

`NN-<etap>.brief.md` — tylko dla `agent`/`mixed`: samodzielny prompt dla wykonawcy: cel, potrzebny kontekst, ścieżki, pełna treść specu (skopiowana), czego nie zmieniać, ograniczenia (bez commitów, bez `.env`, bez nowych zależności i akcji na zewnątrz bez zgody), definicja ukończenia.

Pisz tylko te pliki.

### Koniec planowania

Pokaż listę plików i tabelę etapów. Zapytaj o akceptację (`autonomous`: pomiń). Potem `Planning: complete`, usuń sekcję „Otwarte pytania” i zaproponuj start `01`. Nie zaczynaj bez zgody, chyba że użytkownik prosił o wykonanie.

## Faza 2 — Wykonanie etapu

0. Bramka: `Planning: complete` i poprzedni etap `done`. Inaczej `BLOCKED: <powód> — <co zrobić>`.
1. Status `in progress`.
2. Realizacja:
   - `agent` — wykonaj z briefu i specu, wg reguł projektu.
   - `user` — pokaż plan szczegółowy i kryteria jako checklistę; czekaj na zgłoszenia (także w kolejnych sesjach). Każde potwierdzone kryterium od razu odhacz w specu.
   - `mixed` — obie części, w kolejności wynikającej z zależności.
   - Pytania w trakcie: jak w fazie 1; decyzję zapisz w specu i README.
3. Weryfikacja:
   - Część `agent` — automatycznie po realizacji: jeden `Agent` (`general-purpose`, świeży kontekst) dostaje ścieżki specu i briefu i sprawdza każde kryterium: `PASS` / `GAP` z dowodem (`path:line`, wynik polecenia); nie edytuje plików. Testy ze specu uruchom sam i zacytuj prawdziwy wynik.
   - Część `user` — kryterium jest `PASS` tylko po wyraźnym potwierdzeniu użytkownika.
4. Wynik:
   - wszystko `PASS` → `done`;
   - `GAP` albo czerwony test → `gaps` i lista luk. Jedno pytanie: naprawić teraz (Recommended) czy dodać nowy etap. Nie rozszerzaj zakresu po cichu.
   - Kryterium czekające na zgodę użytkownika nie jest luką: etap zostaje `in progress`, dopóki zgody nie ma.

## Zapytanie (w dowolnym momencie)

Tylko odczyt: który etap trwa, co dalej, czy można zacząć, luki, otwarte pytania.
- Jeden plan → użyj go. Kilka → pytanie o wszystkie = tabela przeglądowa; o jeden = zapytaj który (rekomendacja: ten z etapem `in progress`). Pomijaj `archive/`.
- Odpowiadaj z `README.md`; spec czytaj tylko dla etapu, o który pytano. Statusy cytuj dosłownie.
- „Czy można zacząć następny?” = tak tylko, gdy `Planning: complete`, poprzedni `done`, a następny nie jest `in progress`.
- Sprzeczność w plikach zgłoś, nie naprawiaj. Bez edycji, testów i agentów.

## Zasady

- Jedno pytanie na wiadomość. Rekomendacja pierwsza i oznaczona.
- Nie wymyślaj wymagań. Założenie oznacz jako założenie.
- **Zgoda przed czynnością:** gdy reguły projektu wymagają zgody (np. podbicie wersji), a także przed zakupem, wysłaniem wiadomości, rezerwacją — zapytaj (`autonomous`: przygotuj, wpisz jako kryterium „zgoda użytkownika” i wykonaj dopiero po zgodzie).
- Nie zapisuj sekretów ani danych osobowych (nazwiska, telefony, e-maile, numery kont) — zastąp opisem lub placeholderem.
- Pliki tylko w katalogu planu. Wyjątek za zgodą: jedna linia w „Historia” źródłowego pliku backlogu (`YYYY-MM-DD — przeniesione do planu <slug>`).
- Gdy wszystkie etapy są `done`, zaproponuj (jedno pytanie) archiwizację: przeniesienie do `archive/<slug>/`, usunięcie `*.brief.md`, poprawę linków; dla planu ze `Źródło` w backlogu — także usunięcie pliku backlogu.
- Bez commitów, pushy i PR, chyba że użytkownik poprosi. Nie dotykaj `.env`.
