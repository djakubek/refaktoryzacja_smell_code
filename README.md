# Refaktoryzacja

Autor: Daniel Jakubek

#

Ruby Gem konwertujący Dokument MS [Word do Markdown'a](https://github.com/benbalter/word-to-markdown)

# Instalacja api:

```sh

 sudo apt-get install zlib1g-dev

 gem install word-to-markdown

```

Przykładowe użycie:

```sh

 w2m test.doc

```

W wyniku otrzymamy gotowy kod Markdown'a na STDOUT terminala

```sh

|  Pogrubiony przykład w tabelce | Zwykły w tabelce |

| --- | --- |

|   | [Link do aplikacji](https://github.com/benbalter/word-to-markdown) |

- .To jest przykład wypunktowania

- .To jest przykład wypunktowania

- .To jest przykład wypunktowania

1. To jest lista numerowana

2. To jest lista numerowana – boldowany

3. To jest lista numerowana

# Test wielkoscimałe

```

Jak widać aplikacja działa prawidłowo bez żadnych problemów.

#

# Przejdźmy do działania – Problemy zgłaszane przez reek

```sh

$ reek -f json lib | jq .[].wiki\_link -r  | sort | uniq -c | sort -n

      1 https://github.com/troessner/reek/blob/master/docs/Control-Parameter.md

      1 https://github.com/troessner/reek/blob/master/docs/Instance-Variable-Assumption.md

      1 https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Method-Name.md

      1 https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Parameter-Name.md

      2 https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Variable-Name.md

      2 https://github.com/troessner/reek/blob/master/docs/Utility-Function.md

      4 https://github.com/troessner/reek/blob/master/docs/Too-Many-Statements.md

      5 https://github.com/troessner/reek/blob/master/docs/Feature-Envy.md

      5 https://github.com/troessner/reek/blob/master/docs/Nil-Check.md

      7 https://github.com/troessner/reek/blob/master/docs/Duplicate-Method-Call.md

      7 https://github.com/troessner/reek/blob/master/docs/Irresponsible-Module.md

      9 https://github.com/troessner/reek/blob/master/docs/Prima-Donna-Method.md

```

# Problemy zgłaszane przez flog

```sh

 307.1: flog total

 7.0: flog/method average

```

# Problemy zgłaszane przez flay

```sh

$ flay lib

Total score (lower is better) = 0

```
