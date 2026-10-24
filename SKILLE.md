# Skille w Codexie i Claude Code — krótki przewodnik

## Co to jest skill i do czego służy?

Skill to zestaw instrukcji dla AI do wielokrotnego użytku — przepis na wykonanie konkretnego zadania. Dzięki niemu nie trzeba za każdym razem tłumaczyć tych samych zasad.

Przykładowe zastosowania:

- podsumowywanie spotkań według ustalonego wzoru;
- sprawdzanie kodu zgodnie z zasadami projektu;
- tworzenie raportów i dokumentacji;
- wykonywanie powtarzalnych operacji za pomocą skryptów.

Skill jest folderem. Jego wymagany plik to `SKILL.md`, a pozostałe pliki są opcjonalne.

## Gdzie umieścić skill na Windowsie?

Dla narzędzi uruchomionych bezpośrednio w Windowsie:

| Narzędzie | Zastosowanie | Przykładowa ścieżka |
| --- | --- | --- |
| Codex | Skill użytkownika, dostępny w różnych projektach | `C:\Users\micha\.agents\skills\raport-spotkania\SKILL.md` |
| Claude Code | Skill użytkownika, dostępny w różnych projektach | `C:\Users\micha\.claude\skills\raport-spotkania\SKILL.md` |
| Codex | Skill konkretnego repozytorium | `X:\ścieżka\do\projektu\moja-aplikacja\.agents\skills\raport-spotkania\SKILL.md` |
| Claude Code | Skill konkretnego repozytorium | `X:\ścieżka\do\projektu\moja-aplikacja\.claude\skills\raport-spotkania\SKILL.md` |

Brakujące foldery utwórz samodzielnie. Każdy skill powinien mieć osobny folder, np. `raport-spotkania`.

W WSL użyj katalogu domowego użytkownika wewnątrz WSL:

- Codex: `~/.agents/skills/raport-spotkania/SKILL.md`;
- Claude Code: `~/.claude/skills/raport-spotkania/SKILL.md`.

## Jak utworzyć plik SKILL.md?

Poniższy format działa w Codexie i Claude Code.

1. Utwórz folder skilla w wybranej lokalizacji.
2. Otwórz VS Code lub Notatnik.
3. Utwórz zwykły plik tekstowy o nazwie dokładnie `SKILL.md`.
4. W Notatniku wybierz przy zapisie typ „Wszystkie pliki” i kodowanie UTF-8. Sprawdź, czy plik nie nazywa się `SKILL.md.txt`.
5. Wpisz metadane i instrukcje, korzystając z poniższego przykładu.

```markdown
---
name: raport-spotkania
description: Twórz raport, gdy użytkownik poda notatki ze spotkania.
---

Przygotuj raport po polsku na podstawie otrzymanych notatek.

1. Wypisz najważniejsze ustalenia.
2. Zbierz zadania w tabeli: zadanie, osoba, termin.
3. Jeśli brakuje osoby lub terminu, wpisz „nie ustalono”.
4. Nie dopisuj faktów, których nie ma w notatkach.
```

Początkowy blok między liniami `---` to metadane w formacie YAML:

- `name` — nazwa skilla; używaj małych liter, cyfr i myślników, np. `raport-spotkania`;
- `description` — krótki opis tego, co skill robi i kiedy należy go użyć.

Tekst pod drugim `---` to instrukcje w Markdown. Możesz pisać je po polsku.

## Jakie dodatkowe pliki może zawierać skill?

```text
raport-spotkania/
├── SKILL.md
├── references/
│   └── zasady-firmy.md
├── scripts/
│   └── generuj_raport.py
├── assets/
│   ├── szablon.md
│   └── logo.png
└── agents/
    └── openai.yaml
```

| Element | Przeznaczenie |
| --- | --- |
| `SKILL.md` | Główne instrukcje i metadane. Jedyny wymagany plik. |
| `references/` | Dodatkowa wiedza: zasady firmowe, dokumentacja, opisy danych. |
| `scripts/` | Programy pomocnicze, np. Python, JavaScript lub PowerShell. Ich uruchomienie wymaga odpowiednich narzędzi w środowisku. |
| `assets/` | Szablony, obrazki, logo i inne materiały używane w wyniku. |
| `agents/openai.yaml` | Opcjonalne ustawienia prezentacji skilla, sposobu wywoływania i zależności w Codexie. Claude Code nie potrzebuje tego pliku. |

Nie musisz tworzyć wszystkich tych folderów. Na początek wystarczy sam `SKILL.md`.

Jeśli dodasz pliki pomocnicze, wskaż w instrukcji, kiedy i jak z nich korzystać, np.:

```markdown
Przed przygotowaniem raportu przeczytaj references/zasady-firmy.md.
Zastosuj układ z assets/szablon.md.
```

Ścieżki te odnoszą się do folderu skilla. Codex i Claude Code najpierw widzą nazwę i opis skilla, następnie wczytują jego instrukcje, a po materiały pomocnicze sięgają w miarę potrzeb.

## Jak używać skilla?

Oba narzędzia mogą dobrać skill automatycznie na podstawie pola `description`. Możesz też wskazać go wprost:

| Narzędzie | Przykład wywołania w rozmowie |
| --- | --- |
| Codex | `$raport-spotkania Podsumuj poniższe notatki: …` |
| Claude Code | `/raport-spotkania Podsumuj poniższe notatki: …` |

W Codex CLI lub rozszerzeniu IDE możesz użyć `/skills` albo wpisać `$`, aby wybrać skill. Jeśli nowy skill lub jego zmiany się nie pojawią, uruchom Codexa ponownie.

W Codexie możesz również poprosić wbudowany kreator o przygotowanie skilla:

```text
$skill-creator Stwórz skill do podsumowywania spotkań po polsku.
Wynik ma zawierać ustalenia oraz tabelę zadań, osób i terminów.
```

W Claude Code, jeśli skill ma być uruchamiany wyłącznie na Twoje żądanie, dodaj do początkowego bloku YAML w `SKILL.md`:

```yaml
disable-model-invocation: true
```

`CLAUDE.md` służy do ogólnych zasad projektu w Claude Code, a skill do konkretnej procedury wykonywanej w razie potrzeby.

## Jak pisać dobre skille?

- Skup każdy skill na jednym konkretnym zadaniu.
- Jasno opisz, kiedy powinien się uruchamiać.
- Określ dane wejściowe, sposób pracy i oczekiwany wynik.
- Dodawaj konkretne zasady, które pomagają wykonać zadanie.
- Przenieś obszerną wiedzę do plików pomocniczych i odwołaj się do nich w instrukcji.
- Sprawdź skill na kilku prawdziwych przykładach i poprawiaj go na podstawie wyników.

## Źródła

- [Tworzenie skilli i lokalizacje w Codexie — dokumentacja OpenAI](https://learn.chatgpt.com/docs/build-skills)
- [Czym są skille — dokumentacja OpenAI](https://developers.openai.com/plugins/concepts/skills)
- [Skille w Claude Code — dokumentacja Anthropic](https://code.claude.com/docs/en/skills)
