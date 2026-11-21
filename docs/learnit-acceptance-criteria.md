# `_learnit` — kryteria ukończenia

Data: 2026-11-21. Skill: `skills/_learnit/`. Skill jest ukończony, gdy wszystkie kryteria mają PASS.

## Zasada stopu

- Weryfikacja odbywa się w jednym przebiegu. Poprawiamy tylko to, co nie spełnia kryterium.
- Po poprawce powtarzamy wyłącznie kryteria, które nie przeszły. Najwyżej 2 takie przebiegi. Jeśli dalej nie przechodzą, zmieniamy kryterium albo akceptujemy stan. Nie dopisujemy nowych reguł.
- Nowe przypadki brzegowe trafiają do `docs/backlog/` (`_parkit`), nie do skilla.
- Subagent dostaje zadanie użytkownika i skill, nic więcej. Odpowiedzi „ucznia” symuluje osobny prompt z zadanym poziomem wiedzy.

## A. Struktura

- [x] A1. `SKILL.md` jest jedynym plikiem z instrukcjami i ma ≤ 180 linii.
- [x] A2. Symlink `~/.claude/skills/_learnit` wskazuje na `skills/_learnit`, skill widoczny w sesji.
- [x] A3. Dane tematów trafiają do `~/.claude/learning/`, niezależnie od katalogu roboczego.

## B. Zachowanie (scenariusze)

- [x] B1. `start-it`: temat IT (np. „async w Pythonie”). Jedno pytanie na wiadomość z rekomendacją, test diagnostyczny przed planem, po akceptacji powstają `topic.md`, `plan.md`, `knowledge.md`, `journal.md` i wpis w `INDEX.md`.
- [x] B2. `start-humanities`: temat nietechniczny (np. „przyczyny I wojny światowej”). Plan i weryfikacja bez zadań programistycznych; typy pytań pasują do dziedziny (przyczyna–skutek, porównanie, chronologia).
- [x] B3. `check-mixed`: weryfikacja z częściowo błędnymi odpowiedziami. Każde pojęcie dostaje osobny status z dowodem i datą powtórki; „rozumiem” bez odpowiedzi nie zalicza.
- [x] B4. `support`: pojęcie oblane dwa razy. Powstaje `support/NN-<etap>.md` z diagnozą przyczyny, innym podejściem i ponowną weryfikacją.
- [x] B5. `resume`: nowa sesja „wracamy do <temat>” — stan odtworzony wyłącznie z plików; najpierw powtórki z zaległych pojęć, potem bieżący etap.
- [x] B6. `expand`: użytkownik zgłasza powiązany wątek. Propozycja: etap albo osobny temat; zmiana zapisana w historii zakresu; numery istniejących etapów bez zmian.
- [x] B8. `start-with-questions`: pierwsza wiadomość z pytaniami merytorycznymi i repozytoriami referencyjnymi. Pierwsza odpowiedź to szkic zakresu, pytania przypisane do zagadnień, brak odpowiedzi merytorycznych (Haiku i Sonnet).
- [x] B9. `lesson-flow`: plan wykracza poza pytania ucznia; przed pierwszym pytaniem sprawdzającym powstaje lekcja w `lessons/` ze sprawdzonymi źródłami; pytanie ma scenariusz i jawne oczekiwanie; poprawna krótka odpowiedź → dopytanie, nie obniżenie.
- [x] B10. `mentor-style`: przy globalnej regule „extremely concise” rozmowa nadal pełnymi zdaniami, bez statusów w czacie; błąd → podpowiedź przed rozwiązaniem; informacja zwrotna: co dobre → co brakuje → następny krok.
- [x] B11. `export`: plik w `exports/`, lekcje + klucz + prompt tutora; brak postępów, profilu, dziennika, ścieżek i danych osobowych (grep 0 trafień).
- [x] B12. `recipient`: asystent bez _learnit z plikiem eksportu i kartą postępu pisze lekcję kolejnego etapu ze szkicu, dopasowaną do karty; ton bez etykiet; karta na koniec sesji.
- [x] B7. `status`: pytanie „co umiem z <temat>?” — tylko odczyt, odpowiedź z `knowledge.md`.

## C. Reguły krytyczne

- [x] C1. Brak limitu czasu sesji: skill nie narzuca czasu ani liczby etapów na sesję.
- [x] C2. Stan zapisywany po każdej weryfikacji — przerwana sesja nic nie traci.
- [x] C3. Brak gita: skill nie wykonuje `git init` ani commitów w `~/.claude/learning/`.
- [x] C5. Sprawdzian i powtórki są propozycją: użytkownik może je pominąć, a etap trwa przez wiele sesji bez utraty stanu.
- [x] C4. Ćwiczenia praktyczne (pliki) tylko w `<slug>/exercises/`.

## D. Użycie rzeczywiste

- [ ] D1. Jeden prawdziwy temat przerobiony przez użytkownika przez ≥ 3 sesje, bez poprawek skilla w trakcie. Uwagi do backlogu.

## Wynik weryfikacji — 2026-11-21

A1–A3, B1–B7, C1–C5: PASS w jednym przebiegu, bez poprawek skilla. Testy na kopiach danych w scratchpadzie (nadpisany katalog danych); prawdziwy `~/.claude/learning` nietknięty.

Dowody:
- A1: 103 linie. A3: wszystkie przebiegi zapisywały w katalogu danych, nie w katalogu roboczym.
- B3: „rozumiem, nie musisz pytać” → pytanie mimo to, status `unknown`.
- B6: nagłówki etapów 01–04 bez zmian, nowy 05.
- B7 / C2: sumy kontrolne plików przed i po identyczne; B5: stan zapisany przed „muszę lecieć”.
- C1: grep transkryptów (minut/godzin/harmonogram/deadline): 0 trafień. C3: brak `.git`. C4: pliki nie-md tylko w `exercises/`.

Niejasności zgłoszone przez testerów → `docs/backlog/learnit-test-round-1-gaps.md`. Zostaje D1.

## Poprawka v0.1.1 i powtórka B3–B5 — 2026-11-21

Wdrożone pkt 1–5 z backlogu (interwały z kolumną `krok`, statusy, źródła, wyzwalacz supportu, diagnoza). SKILL.md: 109 linii (A1 OK). B3–B5 powtórzone na świeżych kopiach danych: PASS.

Spójność interwałów — oczekiwane wartości rozpisane przed testem, wszystkie zgodne:
- B3: task krok 2 → 11-24; create-task krok 1 → 11-22; gather, concurrency krok 1 → 11-22. Support zaproponowany, nie uruchomiony.
- B4: task krok 2 → 11-24. Support najpierw zaproponowany; plik `support/02-*`; źródło sprawdzone w sieci.
- B5: await, task krok 2 → 11-24; event-loop krok 3 → 11-28; create-task krok 1 → 11-22. Migracja kolumny `krok` zgodna u 3 testerów.

Nowe uwagi → backlog pkt 12–16. Zostaje D1.

## Poprawka v0.1.2 — 2026-11-21

Realne użycie (Haiku 5.5): skill odpowiedział merytorycznie na pytania ze startu. Dodano regułę „na starcie nie ucz” i szkic zakresu z pierwszej wiadomości. B8 na Haiku i Sonnet z oryginalnym promptem: PASS — 0 odpowiedzi merytorycznych, pytania zapisane dosłownie w `topic.md` i przypisane do zagadnień, jedno pytanie o lukę. SKILL.md: 112 linii.

## Poprawka v0.1.3 — 2026-11-21

Realne użycie (Haiku, prompt bez `/_learnit`): skill nie wywołany. Zmiana `description` („wywołaj najpierw…”). Pomiar `claude -p --model haiku`: pełny prompt 0/3 → 4/4, krótki 2/2, resume 2/2, negatyw 0/2. Potwierdzone przez użytkownika w nowej sesji na Haiku. Zostaje D1.

## Poprawka v0.2.0 — 2026-11-21

Realne użycie: program zawężony do pytań ucznia, brak lekcji (od razu pytania), pytania bez kontekstu, obniżenie oceny za brak nieproszonego uzasadnienia, treści niepoparte źródłami. B9 na Haiku: PASS — 6 etapów (3 poza pytaniami), lekcja 01 (706 słów, źródło: oficjalna dokumentacja, sprawdzone), pytanie ze scenariuszem i „2–3 zdania”, dopytanie „dlaczego?” przed oceną `ok`. SKILL.md: 128 linii. Zostaje D1.

## Poprawka v0.3.0 — 2026-11-21

Uwaga użytkownika: styl sztywny i niezachęcający. Dodana sekcja „Styl mentora” (źródła: `docs/learnit-references.md`). B10 na Haiku z regułą „extremely concise”: PASS. Pełne zdania, sprawdzanie zapowiedziane jako ćwiczenie, przy błędzie podpowiedź z odesłaniem do przykładu z lekcji, statusy nieogłaszane, na koniec podsumowanie postępu. Poprawka po teście: w czacie wyciekł identyfikator pojęcia; dopisano zakaz identyfikatorów. A1 podniesione do ≤ 160 linii.

## v0.3.x–0.4.0 — 2026-11-21

0.3.2: pytanie „zaczynamy?” po planie. 0.3.3: wyzwalanie po intencji (Haiku: „Chciałbym…” 3/3, z literówką 3/3, EN 2/2, negatywy 0/4). 0.4.0: eksport; B11 na Haiku PASS. A1 podniesione do ≤ 180 linii.

## v0.4.1–0.4.2 — 2026-11-21

Eksport bez dopisywania lekcji (lekcje powstają u odbiorcy na bieżąco), szkice, sekcja „Metoda”, karta postępu, szablon promptu tutora. B11 (ponownie) i B12 na Haiku: PASS. Pierwsze podejście do B12 (prompt składany przez model): mechanika OK, ton sztywny, więc wprowadzono szablon.
