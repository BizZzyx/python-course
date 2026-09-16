# Python Practice — 50 Lessons / Python Practice — 50 lekcji

**English:** A single-page, browser-based Python learning app. It presents 50 guided lessons, lets learners write and run Python in the page, checks their submissions, and remembers progress in the browser.

**Polski:** Jednostronicowa aplikacja do nauki Pythona działająca w przeglądarce. Zawiera 50 prowadzonych lekcji, umożliwia pisanie i uruchamianie kodu, sprawdza rozwiązania oraz zapamiętuje postępy w przeglądarce.

## What it includes / Co zawiera

- **English:** 50 lessons, from `print()` and variables through functions, collections, exceptions, JSON, classes, and a final expense-summary project.
- **Polski:** 50 lekcji — od `print()` i zmiennych, przez funkcje, kolekcje, wyjątki, JSON i klasy, po końcowy projekt podsumowania wydatków.
- **English:** Every lesson includes a tutorial, example, assignment, reference answer, and explanation.
- **Polski:** Każda lekcja zawiera omówienie, przykład, zadanie, rozwiązanie referencyjne i wyjaśnienie.
- **English:** Python runs in the browser using [Pyodide](https://pyodide.org/), with automated assignment checks and captured output.
- **Polski:** Python działa bezpośrednio w przeglądarce dzięki [Pyodide](https://pyodide.org/); aplikacja automatycznie sprawdza zadania i pokazuje wynik programu.
- **English:** The app includes progress tracking, saved code for each lesson, reference-answer visibility, and responsive dark-mode styling.
- **Polski:** Aplikacja zawiera śledzenie postępów, zapisywanie kodu dla każdej lekcji, podgląd rozwiązania referencyjnego oraz responsywny ciemny interfejs.

## Run the app / Uruchomienie aplikacji

1. **English:** Save `index.html` on your computer or publish it as a static website.
2. **Polski:** Zapisz plik `index.html` na komputerze albo opublikuj go jako statyczną stronę internetową.
3. **English:** Open it in a current version of Chrome, Firefox, Edge, or Safari.
4. **Polski:** Otwórz go w aktualnej wersji Chrome, Firefox, Edge lub Safari.
5. **English:** Choose a lesson, write your solution, and select **Run & Check**.
6. **Polski:** Wybierz lekcję, napisz rozwiązanie i kliknij **Run & Check**.

**English:** The first run downloads Pyodide from jsDelivr, so internet access is required. GitHub Pages is suitable for publishing; do not use GitHub's file-preview page to run the app.

**Polski:** Przy pierwszym uruchomieniu aplikacja pobiera Pyodide z jsDelivr, dlatego wymaga połączenia z internetem. Do publikacji sprawdzi się GitHub Pages; nie uruchamiaj aplikacji z podglądu pliku na GitHubie.

## Keyboard shortcuts / Skróty klawiaturowe

| Action / Czynność | Shortcut / Skrót |
| --- | --- |
| Indent in the editor / Wstaw wcięcie w edytorze | `Tab` |
| Run and check code / Uruchom i sprawdź kod | `Ctrl` + `Enter` or / lub `Cmd` + `Enter` |

## How it works / Jak to działa

**English:** The entire application is contained in `index.html`.

**Polski:** Cała aplikacja mieści się w pliku `index.html`.

- `lessons` stores the assignments, starter code, reference solutions, and automated checks. / `lessons` przechowuje zadania, kod startowy, rozwiązania referencyjne i testy automatyczne.
- `extendedLessonContent` replaces concise material with expanded teaching content. / `extendedLessonContent` zastępuje krótkie materiały bardziej rozbudowaną treścią edukacyjną.
- A Web Worker starts a separate Pyodide session for every run, so the learner can stop an infinite loop or long-running submission. / Web Worker uruchamia osobną sesję Pyodide dla każdego uruchomienia, dzięki czemu można zatrzymać pętlę nieskończoną lub zbyt długo działający kod.
- User code runs before the lesson checks. / Kod użytkownika jest uruchamiany przed testami zadania.
- Output is limited to 16,000 characters; Python loading has a 90-second limit and execution has a 5-second limit. / Wynik jest ograniczony do 16 000 znaków; ładowanie Pythona ma limit 90 sekund, a wykonanie kodu — 5 sekund.

## Guide for contributors and AI assistants / Przewodnik dla osób rozwijających projekt i asystentów AI

**English:** This app has no build system, package manager, backend, or separate source files. Make changes directly in `index.html`. The file is organized into four main areas:

**Polski:** Ta aplikacja nie ma systemu budowania, menedżera pakietów, backendu ani osobnych plików źródłowych. Zmiany wprowadzaj bezpośrednio w `index.html`. Plik ma cztery główne obszary:

| Area / Obszar | Purpose / Cel |
| --- | --- |
| HTML near the start / HTML na początku pliku | Page structure, buttons, editor, results, and accessibility attributes. / Struktura strony, przyciski, edytor, wyniki i atrybuty dostępności. |
| `<style>` near the start / `<style>` na początku pliku | Responsive dark-theme styling. / Responsywne stylowanie ciemnego motywu. |
| `lessons` / `lessons` | The canonical sequence of 50 assignments: titles, starter code, solutions, and automated checks. / Podstawowa sekwencja 50 zadań: tytuły, kod startowy, rozwiązania i testy automatyczne. |
| `extendedLessonContent` / `extendedLessonContent` | Expanded Polish tutorials, examples, and solution explanations, matched by lesson index. / Rozszerzone polskie omówienia, przykłady i wyjaśnienia rozwiązań, dopasowane indeksem do lekcji. |
| Code after `SAVED STATE` / Kod po `SAVED STATE` | Local persistence, rendering, Python execution, timeouts, and UI events. / Lokalny zapis, renderowanie, wykonywanie Pythona, limity czasu i zdarzenia interfejsu. |

### Rules that must remain true / Zasady, które muszą pozostać spełnione

- **English:** `lessons.length` must equal `extendedLessonContent.length`. Entries are matched by position, not by title.
- **Polski:** `lessons.length` musi być równe `extendedLessonContent.length`. Wpisy są parowane według pozycji, a nie tytułu.
- **English:** Do not change a lesson's position unless its saved progress and saved code may intentionally move to another lesson. Browser storage uses numeric lesson indexes.
- **Polski:** Nie zmieniaj pozycji lekcji, chyba że świadomie chcesz przenieść zapisany postęp i kod do innej lekcji. Dane w przeglądarce używają numerycznych indeksów lekcji.
- **English:** Keep tests self-contained. They run after learner code in the same execution namespace and should use `assert` with helpful messages.
- **Polski:** Testy powinny być samowystarczalne. Uruchamiają się po kodzie ucznia w tej samej przestrzeni nazw i powinny używać `assert` z pomocnymi komunikatami.
- **English:** Preserve the Web Worker execution model and termination logic when changing code execution; it is what makes Stop and the time limits work.
- **Polski:** Zachowaj model wykonywania kodu w Web Workerze oraz logikę zatrzymywania przy zmianach w wykonywaniu Pythona — to umożliwia działanie przycisku Stop i limitów czasu.
- **English:** Keep user-generated text in `textContent`, not `innerHTML`, unless there is a deliberate and reviewed reason to render HTML.
- **Polski:** Umieszczaj tekst od użytkownika przez `textContent`, a nie `innerHTML`, chyba że istnieje świadomy i sprawdzony powód renderowania HTML.

### Suggested change workflow / Zalecany sposób wprowadzania zmian

1. **English:** Find the relevant section in `index.html` and make the smallest change that fulfills the request.
2. **Polski:** Znajdź odpowiednią sekcję w `index.html` i wprowadź najmniejszą zmianę realizującą wymaganie.
3. **English:** For a lesson change, update both the lesson entry and the same-index `extendedLessonContent` entry.
4. **Polski:** Przy zmianie lekcji zaktualizuj wpis lekcji oraz wpis `extendedLessonContent` o tym samym indeksie.
5. **English:** Open the page in a browser; confirm that it loads, the target lesson renders, code runs, feedback appears, and progress can be saved.
6. **Polski:** Otwórz stronę w przeglądarce; sprawdź, czy się ładuje, docelowa lekcja się wyświetla, kod działa, pojawia się informacja zwrotna i postęp można zapisać.
7. **English:** For execution changes, also check Stop and a deliberately failing submission.
8. **Polski:** Przy zmianach w wykonywaniu kodu sprawdź też przycisk Stop i celowo niepoprawne rozwiązanie.

### Common tasks / Typowe zadania

| Task / Zadanie | Where to change / Gdzie zmienić |
| --- | --- |
| Add or edit a lesson / Dodaj lub zmień lekcję | Matching entries in `lessons` and `extendedLessonContent`. / Odpowiadające sobie wpisy w `lessons` i `extendedLessonContent`. |
| Change starter code or answer / Zmień kod startowy lub odpowiedź | `solution` in the relevant `lessons` entry; the app generates starter code from it. / `solution` w odpowiednim wpisie `lessons`; aplikacja tworzy na jego podstawie kod startowy. |
| Change assignment validation / Zmień walidację zadania | `tests` in the relevant `lessons` entry. / `tests` w odpowiednim wpisie `lessons`. |
| Change layout or colors / Zmień układ lub kolory | The `<style>` block. / Blok `<style>`. |
| Change saved-progress behavior / Zmień zachowanie zapisu postępów | The `state`, `STORAGE_KEY`, and `saveState` area. / Sekcja `state`, `STORAGE_KEY` i `saveState`. |
| Change Python version or CDN / Zmień wersję Pythona lub CDN | `base` inside `pythonWorkerMain`. / Zmienna `base` wewnątrz `pythonWorkerMain`. |

## Saving and privacy / Zapisywanie i prywatność

**English:** The app saves the current lesson, editor contents, and completed lessons in browser `localStorage`, under `python-practice-v1`. The data stays in that browser and does not sync to GitHub or other devices. Clearing the site's browser data removes saved progress.

**Polski:** Aplikacja zapisuje bieżącą lekcję, zawartość edytora i ukończone lekcje w `localStorage` przeglądarki pod kluczem `python-practice-v1`. Dane pozostają w tej przeglądarce i nie synchronizują się z GitHubem ani innymi urządzeniami. Wyczyszczenie danych witryny usuwa zapisane postępy.

**English:** Code runs in the browser, but the Python runtime is downloaded from a CDN. Do not enter passwords, API keys, or other secrets, and do not run code you do not trust.

**Polski:** Kod działa w przeglądarce, ale środowisko Pythona jest pobierane z CDN. Nie wpisuj haseł, kluczy API ani innych sekretów i nie uruchamiaj kodu, któremu nie ufasz.

## Project structure / Struktura projektu

```text
index.html   # App interface, styling, lessons, checks, and browser runtime
             # Interfejs, stylowanie, lekcje, testy i środowisko uruchomieniowe
README.md    # Project overview and usage notes / opis projektu i instrukcje
```

## Customizing lessons / Dostosowywanie lekcji

**English:** To add or revise a lesson, update the corresponding entry in both `lessons` and `extendedLessonContent`. The arrays must remain the same length; the app validates this at startup. Every lesson needs a title, teaching content, an assignment, a reference solution, and checks that raise an assertion when a submission is incorrect.

**Polski:** Aby dodać lub zmienić lekcję, zaktualizuj odpowiadający jej wpis zarówno w `lessons`, jak i `extendedLessonContent`. Obie tablice muszą mieć taką samą długość — aplikacja sprawdza to przy uruchomieniu. Każda lekcja wymaga tytułu, treści edukacyjnej, zadania, rozwiązania referencyjnego oraz testów zgłaszających błąd asercji dla niepoprawnego rozwiązania.

## Known limitations / Znane ograniczenia

- **English:** An internet connection is required to load Pyodide. Progress belongs to one browser profile and device.
- **Polski:** Połączenie z internetem jest wymagane do załadowania Pyodide. Postępy są przypisane do jednego profilu przeglądarki i urządzenia.
- **English:** Checks validate behavior, not a particular programming technique.
- **Polski:** Testy sprawdzają działanie kodu, a nie konkretną technikę programowania.
- **English:** This is an in-browser practice environment, not a replacement for a local Python development setup.
- **Polski:** To środowisko ćwiczeniowe w przeglądarce, a nie zamiennik lokalnego środowiska programistycznego Pythona.
