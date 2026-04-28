# Prologue

## Individual

[testmark]:# (0-arrange)
```nettle
prefix wd http://www.wikidata.org/entity/
alias knows http://xmlns.com/foaf/0.1/knows
alias Mick wd:Q128121
alias Keith wd:Q189599

Mick
  knows
    Keith
```

[testmark]:# (0-assert)
```turtle
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix wd: <http://www.wikidata.org/entity/> .

wd:Q128121 foaf:knows wd:Q189599 .
```

## Grouped

[testmark]:# (1-arrange)
```nettle
prefixes
  ex http://example.org/
  wd http://www.wikidata.org/entity/

aliases
  knows ex:knows
  Mick wd:Q128121
  Keith wd:Q189599

Mick
  knows
    Keith
```

[testmark]:# (1-assert)
```turtle
@prefix ex: <http://example.org/> .
@prefix wd: <http://www.wikidata.org/entity/> .

wd:Q128121 ex:knows wd:Q128121 .
```
