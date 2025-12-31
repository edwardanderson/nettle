# Named graph

[testmark]:# (0-arrange)
```nettle
base http://example.org/

g1 {
  mick
    knows
      keith
}
```

[testmark]:# (0-assert)
```trig
@prefix ex: <http://example.org/> .

<http://example.org/g1> {
    <http://example.org/mick> ex:knows <http://example.org/keith> .
}
```
