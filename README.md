# Refaktoryzacja

Autor: Daniel Jakubek

#

Ruby Gem konwertujący Dokument MS [Word do Markdown'a](https://github.com/benbalter/word-to-markdown)

# Instalacja api:

```ruby

 sudo apt-get install zlib1g-dev

 gem install word-to-markdown

```

Przykładowe użycie:

```ruby

 w2m test.doc

```

W wyniku otrzymamy gotowy kod Markdown'a na STDOUT terminala

```ruby

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

# Problemy zgłaszane przez reek

```ruby

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

```ruby

 307.1: flog total

 7.0: flog/method average

```

# Problemy zgłaszane przez flay

```ruby

$ flay lib

Total score (lower is better) = 0

```


# Przejdźmy do działania - REFAKTORYZACJA

Po pierwsze zająłem się problemami:
https://github.com/troessner/reek/blob/master/docs/Irresponsible-Module.md
https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Method-Name.md
https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Parameter-Name.md
https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Variable-Name.md

Czyli odpowiednio dodałem komentarze do klas, ponazywałem metody, parametry i nazwy zmiennych.

Przykładowo

```ruby
def h(n)
      font_sizes.percentile(((HEADING_DEPTH - 1) - n) * HEADING_STEP)
    end
```
kod po refaktoryzacji

```ruby
def naglowek(wielkosc)
  font_sizes.percentile(((HEADING_DEPTH - 1) - wielkosc) * HEADING_STEP)
end

```

```ruby
class WordToMarkdown
  class Document
    class NotFoundError < StandardError; end
    class ConversionError < StandardError; end
```
Po refaktoryzacji

```ruby
class WordToMarkdown
  #Class Dokument wzorzec do convertowania
  class Document
    #Class NotFoundError obsluga wyjatku braku pliku
    class NotFoundError < StandardError; end
    #Class ConversionError obsluga bledow convertowania
    class ConversionError < StandardError; end

```

Następnie zająłem się problemem

https://github.com/troessner/reek/blob/master/docs/Utility-Function.md

okazało się że funkcja idelanie pasuje w innym miejscu 

W pliku document.rb znalazłem funckcję,

```ruby
    def filter
      if WordToMarkdown.soffice.major_version == '5'
        'html:XHTML Writer File:UTF8'
      else
        'html'
      end
    end
```

 która idealnie pasuje do innej klasy w pliku word-to-markdown.rb


