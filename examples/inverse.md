# inverse

## 0

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

## 1

[testmark]:# (1-arrange)
```nettle
base http://example.org/

Person
  a @inverse
    Mick
    Keith
```

[testmark]:# (1-assert)
```turtle
@prefix ex: <http://example.org/> .

<http://example.org/Mick> a ex:Person .

<http://example.org/Keith> a ex:Person .
```
