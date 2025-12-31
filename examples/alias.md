# alias

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
