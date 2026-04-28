# Annotation

[testmark]:# (0-arrange)
```nettle
base http://example.org/

<<
  Mick
    knows
      Keith
>>
  accordingTo
    Ronnie
```

[testmark]:# (0-assert)
```turtle
@prefix : <http://www.example.org/>

<< ex:Mick ex:knows ex:Keith >> ex:accordingTo ex:Ronnie .
```

[testmark]:# (1-arrange)
```nettle
base http://example.org/

[a1] <<
  Mick
    knows
      Keith
>>
  accordingTo
    Ronnie
```

[testmark]:# (1-assert)
```turtle
@prefix : <http://www.example.org/>

<< ex:Mick ex:knows ex:Keith ~_:a1 >> ex:accordingTo ex:Ronnie .
```
