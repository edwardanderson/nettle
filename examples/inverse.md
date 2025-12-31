# inverse

[testmark]:# (0-arrange)
```nettle
base http://example.org/

guitar
  plays @inverse
    keith
```

[testmark]:# (0-assert)
```turtle
@prefix ex: <http://example.org/> .

<http://example.org/keith> ex:plays <http://example.org/guitar> .
```
