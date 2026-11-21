# Changelog

## 0.1.1 — 2026-11-17

- Szablon README: sekcja „Założenia”. „Koniec planowania”: usuń sekcję „Otwarte pytania” zamiast ją czyścić.

## 0.1.0 — 2026-11-17

- Pierwsza wersja. Oparta na `_make-plan` (se-harness): etapy w plikach, stan `draft`/`complete` w README, jedno pytanie z rekomendacją, bramka między etapami, weryfikacja świeżym agentem, tryb zapytania, archiwizacja.
- Względem `_make-plan`: dowolna dziedzina (wykonawca etapu `agent`/`user`/`mixed`, kryteria jako checkboxy, „Plan szczegółowy”), tryb `autonomous` i numery decyzji `Q<n>` (z `planit`), start od pomysłu `_parkit`, lokalizacja z reguł projektu, stałe numery etapów, zgoda przed czynnością, sanityzacja.
- Uproszczona po 4 rundach testów: jeden plik zamiast `SKILL.md` + `references/`; odrzucone m.in. tryb `critical`, statusy `waiting`/`skipped`/`abandoned`, rozbudowane oznaczenia decyzji i reguły przypadków brzegowych (kopia rozbudowanej wersji poza repo).
