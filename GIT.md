# Git — komendy i flagi

Podstawowe komendy Git i najczęściej używane flagi. Polecenia wykonuj w terminalu, w katalogu repozytorium. Wartości w nawiasach `<...>` zastąp własnymi danymi (bez nawiasów).

## Konfiguracja i rozpoczęcie pracy

| Komenda | Co robi |
| --- | --- |
| `git config --global user.name "Jan Kowalski"` | Ustawia nazwę autora commitów dla bieżącego użytkownika systemu. |
| `git config --global user.email "jan@example.com"` | Ustawia adres e-mail autora commitów. |
| `git config --list` | Wyświetla ustawienia Git. |
| `git init` | Tworzy repozytorium w bieżącym katalogu. |
| `git clone <adres-repozytorium>` | Kopiuje istniejące repozytorium do nowego katalogu i ustawia zdalne repozytorium `origin`. |

Flaga `--global` zapisuje konfigurację dla użytkownika systemu. Bez niej `git config user.name ...` i `git config user.email ...` ustawiają dane tylko dla bieżącego repozytorium.

## Sprawdzanie i zapisywanie zmian

Git rozróżnia pliki robocze, indeks (staging area — zmiany przygotowane do commita) i historię commitów. Commit zapisuje lokalnie zmiany z indeksu.

| Komenda | Co robi |
| --- | --- |
| `git status` | Pokazuje bieżącą gałąź oraz nowe, zmienione i przygotowane pliki. |
| `git status -sb` | Pokazuje skrócony status (`-s`) z informacją o gałęzi (`-b`). |
| `git diff` | Pokazuje zmiany w śledzonych plikach, które nie trafiły jeszcze do indeksu. |
| `git diff --staged` | Pokazuje zmiany przygotowane do następnego commita. |
| `git add <plik>` | Dodaje aktualne zmiany wskazanego pliku do indeksu. |
| `git add .` | Dodaje nowe pliki, zmiany i usunięcia z bieżącego katalogu oraz jego podkatalogów, z uwzględnieniem reguł ignorowania. |
| `git add -A` | Dodaje nowe pliki, zmiany i usunięcia z całego repozytorium, z uwzględnieniem reguł ignorowania. |
| `git add -p` | Pozwala wybierać fragmenty zmian do dodania do indeksu. |
| `git commit -m "Opis zmian"` | Tworzy commit z przygotowanych zmian; `-m` podaje jego opis. |
| `git commit -am "Opis zmian"` | Przygotowuje zmiany i usunięcia śledzonych plików (`-a`) i tworzy commit z opisem (`-m`). Nie dodaje nowych plików. |

## Historia

| Komenda | Co robi |
| --- | --- |
| `git log` | Wyświetla historię commitów; klawisz `q` zamyka przeglądarkę, jeśli została otwarta. |
| `git log --oneline` | Pokazuje każdy commit w jednym wierszu: skrócony identyfikator i opis. |
| `git log --oneline --graph --all` | Pokazuje zwięzłą historię z rysunkiem rozgałęzień (`--graph`) dla wszystkich referencji, m.in. gałęzi i tagów (`--all`). |
| `git log -n 5` | Pokazuje maksymalnie pięć ostatnich commitów. |
| `git show <commit>` | Pokazuje szczegóły i zmiany wskazanego commita. |

## Gałęzie i łączenie zmian

| Komenda | Co robi |
| --- | --- |
| `git branch` | Wyświetla lokalne gałęzie; gwiazdka oznacza bieżącą. |
| `git branch -a` | Wyświetla gałęzie lokalne i lokalnie zapisane referencje gałęzi zdalnych. |
| `git switch -c <nazwa>` | Tworzy gałąź (`-c`) i przełącza się na nią. |
| `git switch <nazwa>` | Przełącza się na istniejącą gałąź. |
| `git merge <gałąź>` | Łączy wskazaną gałąź z bieżącą. W razie konfliktów trzeba je rozwiązać. |
| `git merge --abort` | Próbuje anulować trwające scalanie i odtworzyć stan sprzed jego rozpoczęcia. |
| `git branch -d <nazwa>` | Usuwa lokalną gałąź, jeśli Git uzna ją za scaloną. |

Przed przełączeniem gałęzi lub scalaniem najlepiej zapisać zmiany w commicie albo schowku (`git stash`).

## Repozytorium zdalne

`origin` to zwyczajowa nazwa repozytorium zdalnego, a `main` to przykładowa nazwa głównej gałęzi — w projekcie mogą być inne.

| Komenda | Co robi |
| --- | --- |
| `git remote -v` | Wyświetla repozytoria zdalne i ich adresy; `-v` oznacza szczegółowy widok. |
| `git remote add origin <adres-repozytorium>` | Dodaje zdalne repozytorium o nazwie `origin`. |
| `git fetch origin` | Pobiera historię i aktualizuje lokalne referencje zdalnych gałęzi, bez scalania z bieżącą gałęzią. |
| `git pull --ff-only` | Pobiera zmiany i aktualizuje bieżącą gałąź tylko wtedy, gdy wystarczy przesunąć jej wskaźnik do przodu. Przy rozbieżnej historii przerywa pracę. |
| `git push -u origin <gałąź>` | Wysyła gałąź i ustawia jej powiązanie ze zdalną gałęzią (`-u`, czyli `--set-upstream`). |
| `git push` | W typowej konfiguracji wysyła commity bieżącej gałęzi do powiązanej gałęzi zdalnej. |

## Cofanie zmian i schowek

| Komenda | Co robi |
| --- | --- |
| `git restore --staged <plik>` | Wycofuje plik z indeksu, pozostawiając jego zawartość w katalogu roboczym. |
| `git restore <plik>` | Przywraca plik roboczy do wersji z indeksu. **Usuwa niezapisane w indeksie zmiany tego pliku.** |
| `git revert <commit>` | Tworzy nowy commit odwracający zmiany wskazanego commita, zachowując historię. |
| `git stash push -u -m "Opis schowka"` | Tymczasowo odkłada zmiany; `-u` uwzględnia też nowe, nieśledzone pliki, ale pomija pliki ignorowane. |
| `git stash list` | Wyświetla zapisane schowki. |
| `git stash pop` | Przywraca ostatni schowek i usuwa go z listy po udanym zastosowaniu. Może spowodować konflikty. |

Zachowaj ostrożność z `git reset --hard` (odrzuca zmiany śledzonych plików i może nadpisać nieśledzone pliki stojące na przeszkodzie), `git clean -fd` (usuwa nieśledzone pliki i katalogi) oraz `git push --force` (może nadpisać zdalną historię).

## Jak czytać flagi

- Flagi krótkie zaczynają się od jednego myślnika, np. `-m`, a długie od dwóch, np. `--staged`.
- Niektóre flagi przyjmują wartość: `-m "Opis"` lub `-n 5`.
- Część krótkich flag można łączyć: `git commit -am "Opis"` odpowiada `git commit -a -m "Opis"`.
- Znaczenie flagi zależy od polecenia: `-u` w `git push` ustawia upstream, a w `git stash push` uwzględnia nieśledzone pliki.
- `git <komenda> -h` wyświetla krótką pomoc, np. `git commit -h`.
- `--` oddziela opcje i referencje od ścieżek, np. `git diff -- README.md` pokazuje różnice dla tego pliku.

## Przykładowy cykl pracy

Przykład zakłada istniejące repozytorium z gałęzią `main` powiązaną ze zdalną gałęzią i czysty katalog roboczy:

```bash
git switch main
git pull --ff-only
git switch -c dodaj-dokumentacje

# Teraz edytuj README.md, a potem sprawdź i zapisz zmiany:
git diff -- README.md
git add README.md
git diff --staged
git commit -m "Dodaj dokumentację Git"
git push -u origin dodaj-dokumentacje
```
