# base

[testmark]:# (0-arrange)
```nettle
base http://example.org/

Mick
  knows
    Keith
```

[testmark]:# (0-assert)
```turtle
@prefix ex: <http://example.org/> .

ex:Mick ex:knows ex:Keith .
```
