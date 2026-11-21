---
title: "_learnit: niejasności z 1. rundy testów"
type: fix
date: 2026-11-21
source: weryfikacja B1–B7 skilla _learnit (wszystkie PASS, uwagi testerów)
tags: [learnit]
---

## Kontekst
Wszystkie kryteria A–C przeszły. Testerzy zgłosili niejasności — rozstrzygali je rozsądnie, ale różnie.

## Problem / cel
Ujednolicić zachowanie w miejscach, gdzie testerzy zgadywali. Priorytet wg liczby zgłoszeń.

## Proponowane rozwiązanie
1. **Interwały powtórek** (B3, B4, B5): jawna reguła kroku — pierwsze `ok` → +1 dzień; każde kolejne `ok` → następny krok 3/7/21; błąd → reset do 1 dnia, status `shaky`.
2. **Źródła** (B2): tytuły, linki, wydania sprawdzaj w sieci albo oznacz „niezweryfikowane”.
3. **Support — wyzwalacz** (B3, B4): zaproponuj support (nie uruchamiaj bez pytania); próg: 2. nieudana próba pojęcia albo etap `review`. Nazwa pliku: numer etapu z trudnością.
4. **`unknown` vs `shaky`** (B3): `unknown` = brak poprawnych elementów; `shaky` = częściowo poprawnie.
5. **Wynik diagnozy** (B1, B2): zapisuj w `knowledge.md` z dopiskiem „diagnoza”, bez terminu powtórki. Pytania diagnostyczne otwarte, bez opcji.
6. **Pole „Po”** (B2, B6): dodać do szablonu etapu; przy równym „Po” kolejność wg numeru.
7. **Zakres** (B1): akceptacja zakresu jednym pytaniem przed planem.
8. **`profile.md`** (B1, B2): tworzyć przy pierwszym temacie z preferencjami z rozmowy startowej.
9. **Katalogi** (B2): `support/` i `exercises/` tworzyć dopiero przy pierwszym użyciu.
10. **Powtórki w check** (B3, B4): zaproponować też na starcie check; pominięcie nie zmienia terminu.
11. **Status** (B7): może kończyć się jednym pytaniem o następny krok; niespójność danych zgłoś, nie poprawiaj.

Z powtórki B3–B5 (2026-11-21):
12. **Awans po supporcie** (B4r): `ok` tuż po błędzie tego samego dnia daje krok 2 (3 dni) — rozważyć, by `ok` w tej samej sesji co błąd dawało tylko krok 1.
13. **Wybór powtórek** (B5r): przy > 3 zaległych — które wybrać (sugestia: `shaky` + najstarsze); pojęcie z bieżącego sprawdzianu nie jest liczone jako powtórka.
14. **„Nie musisz pytać”** (B3r): pytać mimo to czy traktować jak pominięcie.
15. **Etap `review` w INDEX** (B3r): czy pokazywać status etapu w kolumnie „etap”.
16. **Spójność danych** (B5r, B7): etap `done` przy kluczowym pojęciu, które spadło do `shaky` — zgłosić czy zmienić status.

## Alternatywy odrzucone
- Pełny algorytm SM-2 — za ciężki na start.

## Kryteria akceptacji
- SKILL.md ≤ 140 linii po zmianach.
- Powtórzone B3–B5 dają te same interwały u różnych testerów.

## Powiązane pliki
- `skills/_learnit/SKILL.md`
- `docs/learnit-acceptance-criteria.md`

## Historia
- 2026-11-21 — utworzenie
- 2026-11-21 — pkt 1–5 wdrożone w v0.1.1; B3–B5 powtórzone: interwały zgodne z oczekiwanymi u 3 testerów; dopisane pkt 12–16
