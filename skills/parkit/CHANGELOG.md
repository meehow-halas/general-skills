# Changelog

## 0.1.1 — 2026-11-17

- Spójność z `_mapit`: przegląd oznacza pozycje przeniesione do planu (`→ plan <slug>`), powrót wskazuje `_mapit` do rozpisania na etapy.
- Usunięta reguła „nie dodawaj odnośników do backlogu w innych dokumentach” — pokrywa ją zakaz zmian poza `docs/backlog/`; kolidowała z polem `Źródło` w `_mapit`.
- Dodane `evals/evals.json` i `docs/parkit-acceptance-criteria.md`.

## 0.1.0 — 2026-11-16

- Pierwsza wersja: odłożenie, przegląd, powrót, zmiana/usunięcie; podgląd przed zapisem, deduplikacja, sanityzacja, plik `.md` na temat w `docs/backlog/`.
