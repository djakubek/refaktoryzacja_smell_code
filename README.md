# Refaktoryzacja

Autor: Daniel Jakubek

#

Ruby Gem konwertujący Dokument MS [Word do Markdown'a](https://github.com/benbalter/word-to-markdown)

Instalacja:

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
