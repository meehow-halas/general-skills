# `_mapit` — kryteria ukończenia

Data: 2026-11-17. Skill: `skills/_mapit/`. Skill jest ukończony, gdy wszystkie kryteria mają PASS.

## Zasada stopu

- Weryfikacja odbywa się w jednym przebiegu. Poprawiamy tylko to, co nie spełnia kryterium.
- Po poprawce powtarzamy wyłącznie kryteria, które nie przeszły. Najwyżej 2 takie przebiegi. Jeśli dalej nie przechodzą, zmieniamy kryterium albo akceptujemy stan. Nie dopisujemy nowych reguł.
- Nowe przypadki brzegowe znalezione przy okazji trafiają do `docs/backlog/` (`_parkit`), nie do skilla.
- Testy w trybie normalnym, bez szukania niejasności i bez wykonywania „dosłownie”. Subagent dostaje zadanie użytkownika i skill, nic więcej.

## A. Struktura (sprawdzane poleceniami)

- [x] A1. `SKILL.md` jest jedynym plikiem z instrukcjami skilla i ma ≤ 120 linii.
- [x] A2. Brak odwołań do usuniętych plików i koncepcji (`references/`, `waiting`, `skipped`, `critical`).
- [x] A3. Symlink `~/.claude/skills/_mapit` wskazuje na `skills/_mapit`, a skill jest widoczny w sesji.

## B. Zachowanie (scenariusze z `evals/evals.json`, uruchomione raz)

- [x] B1. `new-code-plan`: spełnione wszystkie oczekiwania.
- [x] B2. `non-code-plan`: spełnione wszystkie oczekiwania.
- [x] B3. `seed-from-backlog`: spełnione wszystkie oczekiwania.
- [x] B4. `resume-draft`: spełnione wszystkie oczekiwania.
- [x] B5. `autonomous`: spełnione wszystkie oczekiwania.
- [x] B6. `query-status`: spełnione wszystkie oczekiwania.

## C. Regresje z rund 1–4 (wartościowy rdzeń)

- [x] C1. Zgoda przed czynnością: w `autonomous`, gdy reguła projektu wymaga zgody na podbicie wersji, `VERSION` nie zmienia się przed zgodą, a etap nie dostaje `done`.
- [x] C2. Stałe numery: dodanie etapu do zamkniętego planu daje kolejny wolny numer i nie zmienia nazw istniejących plików.
- [x] C3. Wznowienie: plan przerwany w stanie `draft` jest kontynuowany w nowej sesji wyłącznie z plików, bez powtarzania rozstrzygniętych pytań.
- [x] C4. Sanityzacja: plan z backlogu zawierającego nazwisko, telefon, e-mail i numer konta. Grep tych danych po plikach planu daje 0 trafień.
- [x] C5. Etap `agent` w repo: testy są naprawdę uruchomione i zacytowane, a weryfikację wykonuje świeży `Agent`.

## D. Użycie rzeczywiste (po A–C)

- [ ] D1. Jeden prawdziwy plan wykonany przez użytkownika do końca, bez poprawek skilla w trakcie. Uwagi trafiają do backlogu.

## Wynik weryfikacji — 2026-11-17

A1–A3, B1–B6 i C1–C5: PASS, w jednym przebiegu, bez poprawek skilla.

Dowody z plików na dysku:
- C1: `VERSION` = 0.1.0, etap `in progress` z adnotacją „czeka na zgodę”.
- C4: grep danych osobowych w plikach planu dał 0 trafień.
- C5: `Ran 4 tests … OK`, weryfikacja przez świeży `Agent`.
- C2: nowy etap `03-*`, nazwy istniejących plików bez zmian.

Zostaje D1.

## Poprawka po weryfikacji — 2026-11-17

Wdrożono pozycję backlogu `mapit-readme-template-gaps` (v0.1.1): sekcja „Założenia” w szablonie README, „Koniec planowania” usuwa sekcję „Otwarte pytania”. SKILL.md: 110 linii (A1 nadal OK). Kryteria B/C nie były powtarzane — zmiana nie dotyka ich zachowania. Zostaje D1.
