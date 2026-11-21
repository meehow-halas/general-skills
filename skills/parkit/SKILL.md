---
name: parkit
description: Odkłada do brudnopisu pomysłów w repozytorium (docs/backlog/, pliki .md) ustalenia z rozmowy do późniejszego opracowania (funkcjonalność, poprawka, optymalizacja, pomysł) - park this, save for later, odłóż na później. Użyj też, by przejrzeć odłożone pomysły, wrócić do jednego, zmienić go lub usunąć. NIE używaj do backlogu w Jira/Trello/innym trackerze (tickety, sprinty, grooming). Rozpoznawaj intencję, nie słowa.
---

# _parkit

Zapisuje wypracowane w rozmowie pomysły do plików `.md` w `docs/backlog/`. To brudnopis do późniejszego opracowania: pozycje nie mają statusu.

## Kiedy działa

Tylko po wywołaniu przez użytkownika; nie sugeruje zapisu sam. Samo wywołanie bez wskazówki = odłóż ustalenia z rozmowy. Nic do odłożenia → powiedz to, nie wymyślaj treści. Intencję wywnioskuj z wypowiedzi (bez komend); niejasna → zapytaj jednym zdaniem.

## Intencje

- **Odłożenie** — wyłuskaj ustalenia z rozmowy, pokaż podgląd, zapisz po zatwierdzeniu.
- **Przegląd** — tabela (data, type, tytuł, plik), najnowsze na górze; użytkownik może zawęzić po rodzaju lub temacie. Wpis „przeniesione do planu <slug>” w „Historia” → dopisz przy tytule `→ plan <slug>`. Brak katalogu → „nic nie odłożono”, niczego nie twórz.
- **Powrót** — znajdź plik po opisie (kilka pasuje → zapytaj), wczytaj, krótko streść; sprawdź aktualność `path:line` przed użyciem. Nie zmieniaj pliku. Rozpisanie na etapy to zadanie `_mapit`.
- **Zmiana lub usunięcie** — edycja lub usunięcie pliku w `docs/backlog/` wymaga podglądu i wyraźnego potwierdzenia. Edycja dodaje wpis w „Historia”.

## Lokalizacja

`docs/backlog/` w korzeniu repo, nie w bieżącym podkatalogu.

1. Idź w górę od katalogu roboczego, szukaj `docs/backlog/`, potem `docs/`; zatrzymaj się na katalogu z `.git` (katalog lub plik) lub korzeniu systemu.
2. Jedno miejsce → użyj (utwórz `backlog/`, jeśli brak). Kilka → zapytaj.
3. Brak → zapytaj, gdzie utworzyć; zaproponuj korzeń repo. Nic nie twórz bez potwierdzenia.
4. Tylko `docs/`, nie `doc/`.

## Co zapisać

- Tylko to, co ustalono lub wyraźnie omówiono. Jeden temat = jeden plik.
- `type`: `feature` | `fix` | `optimization` | `idea`.
- Braki wypisz w „Otwarte pytania”, nie dopytuj o każdy szczegół.

## Sanityzacja

Nie zapisuj: sekretów (hasła, tokeny, klucze, connection stringi), danych osobowych (osoby, e-maile, telefony, klienci), wewnętrznych URL-i i hostów. Zastąp opisem lub placeholderem (`<token>`, „klient X”); gdy pomysł traci sens, pomiń i dopisz w „Otwarte pytania”. Dotyczy też nazwy pliku, `source` i `tags`. W podglądzie zaznacz, co zanonimizowano.

## Podgląd przed zapisem

Przed utworzeniem lub zmianą pliku pokaż i poczekaj na zatwierdzenie (także dla jednej pozycji):

| # | Tytuł | type | Plik | Treść (1 linia) |
|---|-------|------|------|-----------------|

Podaj docelowy katalog, deduplikację i sanityzację. Użytkownik może połączyć, rozdzielić, usunąć pozycje lub zmienić tytuły, typy, nazwy.

## Nazwa pliku

Angielski, małe litery, `-`, 3–6 słów, max 50 znaków, np. `cache-for-report-queries.md`. Zajęta nazwa innego tematu → sufiks `-2`.

## Deduplikacja

Przed podglądem poszukaj podobnego pomysłu (tytuł, tagi, treść, sens). Jest → pokaż i zapytaj: dopisać czy nowy plik. Dopisanie: wpinaj w pasujące sekcje, bez powtórzeń, dodaj wpis w „Historia”.

## Format pliku

```markdown
---
title: <krótki tytuł>
type: feature | fix | optimization | idea
date: YYYY-MM-DD
source: <skrót kontekstu rozmowy, jedna linia>
tags: [<opcjonalne>]
---

## Kontekst
## Problem / cel
## Proponowane rozwiązanie
## Alternatywy odrzucone
## Kryteria akceptacji
## Otwarte pytania
## Ryzyka
## Powiązane pliki
- `path/to/file.ext:42` — czemu istotne
## Historia
- YYYY-MM-DD — utworzenie
```

Sekcje bez pokrycia w rozmowie pomijaj (poza „Historia”). „Kontekst”: jedno zdanie, dlaczego odłożono (np. czeka na decyzję, za duże na teraz), jeśli wynika z rozmowy. „Historia”: zawsze ostatnia; przy utworzeniu wpis „utworzenie”, przy każdej zmianie lub dopisaniu jedna linia z datą i tym, co zmieniono. Każda do ok. 4 linii, plik zwykle poniżej ok. 40 linii; długa rozmowa → kilka plików. Treść w języku rozmowy, nazwa pliku po angielsku. `date` z kontekstu środowiska lub `date +%F`, nie szacuj. Cytuj wartości YAML ze znakami specjalnymi (np. `:`, `#`). „Powiązane pliki”: ścieżki od korzenia projektu, nie zgaduj.

Przykład (`cache-for-report-queries.md`):

```markdown
---
title: "Cache: zapytania raportowe do zewnętrznego API"
type: optimization
date: 2026-11-16
source: rozmowa o wolnym ładowaniu dashboardu raportów
tags: [api, wydajność]
---

## Kontekst
Odłożone: najpierw trzeba zdecydować o miejscu cache.

## Problem / cel
Dashboard odpytuje API ok. 12 razy przy odświeżeniu. Skrócić ładowanie.

## Proponowane rozwiązanie
- Cache wyników, TTL 5 min, klucz = endpoint + parametry.

## Otwarte pytania
- Pamięć procesu czy Redis?

## Historia
- 2026-11-16 — utworzenie
```

## Zasady

- Brak operacji git i commitów.
- Nie modyfikuj plików poza `docs/backlog/`; nie twórz `docs/` bez potwierdzenia.
- Nie zapisuj ani nie usuwaj bez potwierdzenia podglądu.
- Po zapisie podaj pełne ścieżki zmienionych plików.
