# `_parkit` — kryteria ukończenia

Data: 2026-11-17. Skill: `skills/_parkit/`. Skill jest ukończony, gdy wszystkie kryteria mają PASS.

Cel: prosty, przewidywalny brudnopis pomysłów. Priorytet: niezawodność i prostota, nie pokrycie przypadków brzegowych.

## Zasada stopu

- Weryfikacja w jednym przebiegu. Poprawiamy tylko to, co nie spełnia kryterium.
- Po poprawce powtarzamy wyłącznie kryteria, które nie przeszły. Najwyżej 2 takie przebiegi. Jeśli dalej nie przechodzą, zmieniamy kryterium albo akceptujemy stan. Nie dopisujemy nowych reguł.
- Poprawka nie może wydłużyć `SKILL.md` ponad limit z A1. Lepiej usunąć regułę niż dodać.
- Nowe przypadki brzegowe trafiają do `docs/backlog/`, nie do skilla.
- Testy w trybie normalnym, bez szukania niejasności. Subagent dostaje zadanie użytkownika i skill, nic więcej.

## A. Struktura (sprawdzane poleceniami)

- [x] A1. `SKILL.md` jest jedynym plikiem z instrukcjami skilla i ma ≤ 120 linii.
- [x] A2. Brak sprzeczności z `_mapit`: format pliku zawiera sekcje, które `_mapit` czyta (Problem / cel, Proponowane rozwiązanie, Kryteria akceptacji, Otwarte pytania, Powiązane pliki, Historia); brak zakazu kolidującego z polem `Źródło`.
- [x] A3. Skill `_parkit` jest widoczny w sesji (`~/.claude/skills/_parkit/SKILL.md` wskazuje na plik z repo).

## B. Zachowanie (scenariusze z `skills/_parkit/evals/evals.json`, uruchomione raz)

- [x] B1. `park-from-conversation`: spełnione wszystkie oczekiwania.
- [x] B2. `nothing-to-park`: spełnione wszystkie oczekiwania.
- [x] B3. `dedup`: spełnione wszystkie oczekiwania.
- [x] B4. `sanitization`: spełnione wszystkie oczekiwania.
- [x] B5. `review-and-return`: spełnione wszystkie oczekiwania.
- [x] B6. `review-empty`: spełnione wszystkie oczekiwania.

## C. Niezawodność (twarde granice, sprawdzane po B)

- [x] C1. W żadnym scenariuszu nie powstał ani nie zmienił się plik bez wcześniejszego zatwierdzenia podglądu.
- [x] C2. W żadnym scenariuszu nie zmieniono plików poza `docs/backlog/` ani nie wykonano operacji git.

## D. Użycie rzeczywiste (po A–C)

- [ ] D1. Jeden prawdziwy pomysł odłożony przez użytkownika i później użyty jako wejście `_mapit`, bez poprawek skilla w trakcie. Uwagi trafiają do backlogu.

## Wynik weryfikacji — 2026-11-17

A1–A3, B1–B6 i C1–C2: PASS, w jednym przebiegu, bez poprawek skilla. 6 świeżych agentów `general-purpose`, każdy w osobnym repo testowym, odpowiedzi użytkownika symulowane.

Dowody z plików na dysku (sumy kontrolne przed/po):
- B1: powstał tylko `docs/backlog/cache-for-report-queries.md` w korzeniu repo (cwd był `src/`); przed `docs/` pytanie o lokalizację.
- B2, B6: brak `docs/`, żadnych zmian.
- B3: zmieniony tylko istniejący plik; nowy wpis w „Historia”; brak nowego pliku.
- B4: grep nazwiska, firmy, e-maila, telefonu, tokenu i hosta po `docs/` dał 0 trafień.
- B5: sumy kontrolne obu plików bez zmian; tabela z `→ plan report-cache`.
- C1: w każdym zapisie podgląd przed zapisem. C2: zmiany tylko w `docs/backlog/`, 0 commitów we wszystkich repo.

Zostaje D1.
