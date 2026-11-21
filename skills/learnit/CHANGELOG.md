# Changelog

## 0.4.3 — 2026-11-21

- Eksport zaczyna się od instrukcji dla odbiorcy ze stałego szablonu `export-readme.md` (co to jest, jak korzystać z AI i bez, karta postępu, dobrze wiedzieć, zawartość pliku). Jeden plik zamiast osobnego README, żeby nic się nie zgubiło przy wysyłce i wklejaniu. Test na Haiku: szablon skopiowany w całości, placeholdery uzupełnione, 0 danych prywatnych.

## 0.4.2 — 2026-11-21

- Prompt tutora to stały szablon `export-tutor-prompt.md`, kopiowany w całości (zasady rozmowy, lekcji, sprawdzania, przykład „zamiast → lepiej”, wzór karty postępu). Powód: składany od nowa prompt gubił zasady stylu i asystent odbiorcy wracał do sztywnego tonu („Karta odebrana”, etykiety „Dobrze: / Czego brakuje:”). Test odbiorcy na Haiku (bez _learnit, plik + karta): ton naturalny, wybór z rekomendacją, lekcja 02 napisana ze szkicu z haczykiem i dopasowana do trudności z karty, pytania po „przeczytałem”, dopytanie „dlaczego?” zamiast wytykania braku, karta na koniec.

## 0.4.1 — 2026-11-21

- Export: brakujących lekcji nie dopisuje się przed eksportem (lekcje powstają na bieżąco i dopasowują się do postępów, także u odbiorcy); usunięte pytanie o dopisanie. Nowe w pliku: szkice etapów bez lekcji, sekcja „Metoda” (zasady z README i „Stylu mentora” + podstawy z linkami), karta postępu (prompt tutora prosi o nią na starcie i wypisuje ją na koniec sesji) jako pamięć między rozmowami; tutor pisze lekcję ze szkicu dopasowaną do karty.

## 0.4.0 — 2026-11-21

- Tryb `export`: jeden samodzielny plik Markdown `<slug>/exports/<slug>-YYYY-MM-DD.md` dla osoby bez _learnit. Zawiera plan, gotowe lekcje, ćwiczenia, „Sprawdź się” z kluczem w `<details>` i na końcu prompt tutora dla dowolnego asystenta AI (dla etapów bez lekcji asystent sam je pisze z planu). Przy brakujących lekcjach skill pyta, co zrobić. Bez postępów, profilu, dziennika i supportu; przykłady z prywatnych materiałów przepisane na ogólne. Opis w README (sekcja 9). Test na Haiku: eksport 1569 słów, grep danych osobowych i ścieżek repozytoriów dał 0 trafień.

## 0.3.3 — 2026-11-21

- `description`: wyzwalanie po intencji nauki w dowolnej formie, języku i z literówkami (chciałbym, I'd like to learn…), także gdy temat wygląda na krótką definicję. Powód: sesje „Front-loading i RAG w AI 1/2” (Haiku) — „Chciałbym/Chiałbym się nauczyć…” nie wywołało skilla. Pomiar Haiku: „Chciałbym…” 3/3, literówka 3/3, angielski 2/2, pełny prompt skille 2/2; negatywy „Co to jest RAG?” i „Wyjaśnij closure” 0/4 (poprawnie). Opis: 1255 znaków (limit listingu 1536).

## 0.3.2 — 2026-11-21

- Po akceptacji planu skill pyta „zaczynamy teraz / później” zamiast od razu pisać lekcję 01 (sesja „Użycie skills w AI 4”).

## 0.3.1 — 2026-11-21

- `README.md`: zasady nauczania przystępnym językiem (start, program, lekcje, sprawdzanie, pomoc, powtórki, tempo, zmiany zakresu, komendy, dane, podstawy naukowe). Tryb `about` w SKILL.md: pytanie o metodę → odpowiedź z README w języku rozmowy. Wyzwalacz w `description`. Odpowiedź językiem ucznia (bez statusów i plików stanu); gdy README niedostępny — z SKILL.md. Test Haiku (`claude -p`): skill wywołany 3/3, odpowiedź z README przystępna.

## 0.3.0 — 2026-11-21

- Sekcja „Styl mentora” oparta na badaniach (szczegóły w `docs/learnit-references.md`): model INSPIRE (Lepper), zasada personalizacji (Mayer), informacja zwrotna feed up/back/forward (Hattie & Timperley), przypominanie bez stawki, SDT (Ryan & Deci). Ton rozmowy zamiast protokołu, bez języka procesu i identyfikatorów w czacie, wybór dla ucznia, haczyk na start lekcji, pytania prowadzące i stopniowe podpowiedzi, sprawdzanie jako ćwiczenie, informacja zwrotna w trzech ruchach, refleksja, widoczny postęp na koniec. W trybie nauki styl ma pierwszeństwo przed globalnymi regułami lakoniczności. Status pojęcia zapisywany w pliku, nieogłaszany w czacie.

## 0.2.1 — 2026-11-21

- Języki (reguła agnostyczna językowo): nazwy plików i folderów zawsze po angielsku niezależnie od języka rozmowy (kebab-case, z przykładem), treść zawsze w języku rozmowy, w której założono temat (`Język:` w `topic.md`). Powód: test v0.2.0 utworzył `lessons/01-anatomia-skilla.md`.

## 0.2.0 — 2026-11-21

- Po realnym użyciu (temat „skille w AI”): zakres = mapa całej dziedziny, pytania ucznia to akcenty, nie granica. Etap = lekcja + ćwiczenia + sprawdzian; lekcja w `lessons/NN-<etap>.md` (po co, wyjaśnienie z kontekstem, przykłady, typowe błędy, odpowiedzi na pytania ucznia, podsumowanie, sprawdzone źródła, ćwiczenia) i w całości w czacie; pytania dopiero po „przeczytałem”. Treść oparta na źródłach, niesprawdzone oznaczane. Pytania sprawdzające: scenariusz z kontekstem + jawne oczekiwanie; ocena wg tego, o co zapytano, dopytanie przed obniżeniem. Test na Haiku: plan 6 etapów (poza pytaniami ucznia), lekcja 706 słów ze źródłem z dokumentacji, dopytanie przed oceną.

## 0.1.3 — 2026-11-21

- `description`: instrukcja „wywołaj najpierw” na początku, z jawnym przypadkiem wiadomości z pytaniami i repozytoriami referencyjnymi. Pomiar na Haiku (`claude -p`): pełny prompt z sesji 0/3 → 4/4; krótki 2/2 → 2/2; „wracamy do nauki” 2/2; negatyw „wyjaśnij closure” 0/2 (poprawnie).

## 0.1.2 — 2026-11-21

- Po pierwszym realnym użyciu: na starcie skill nie uczy — pytania merytoryczne z pierwszej wiadomości trafiają do `topic.md` („Pytania ucznia”) i do etapów planu (pole „Pytania ucznia”). Pierwsza odpowiedź to szkic zakresu z wiadomości, potem pytania tylko o luki. Test diagnostyczny do pominięcia, gdy poziom wynika z materiałów referencyjnych. Mocniejszy `description` (chcę zrozumieć, wiadomość z pytaniami merytorycznymi).

## 0.1.1 — 2026-11-21

- Po 1. rundzie testów (backlog `learnit-test-round-1-gaps`, pkt 1–5): kolumna `krok` i jawna reguła interwałów (ok → krok +1, błąd → krok 1, pominięcie bez zmian, `mastered` po kroku 4); definicje `unknown`/`shaky`/`ok`; źródła weryfikowane albo `(niezweryfikowane)`; support najpierw proponowany, wyzwalacz i nazwa pliku; wyniki diagnozy w `knowledge.md` (krok 0, bez terminu); odpowiedzi w learn to dowód; powtórki proponowane też w check.

## 0.1.0 — 2026-11-21

- Pierwsza wersja: tryby start / plan / learn / check / support / expand / status / resume; globalne dane lokalnie w `~/.claude/learning/` (bez gita); materiał per etap, nie per sesja; sprawdziany i powtórki na życzenie; mapa pojęć z powtórkami 1/3/7/21 dni; miękka bramka 80%; profil ucznia wspólny dla tematów; bez limitów czasu; agnostyczny dziedzinowo.
