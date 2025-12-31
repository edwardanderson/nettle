# include

[testmark]:# (0-arrange)
```nettle
include data/mick-knows-keith.ntl
prefix schema https://schema.org/

Keith
  schema:birthDate
    "1943-12-18"
```

[testmark]:# (0-assert)
```turtle
@prefix ex: <http://example.org/> .
@prefix schema: <https://schema.org> .

<http://example.org/Mick> ex:knows <http://example.org/Keith> .

<http://example.org/Keith> schema:birthDate "1943-12-18" .
```
