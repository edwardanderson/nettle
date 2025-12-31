# language

[testmark]:# (0-arrange)
```nettle
language en
base http://example.org/

Mick
  schema:name
    "Michael"
    "ミック・ジャガー"@jp
    "მიკ ჯაგერი"@ka
```

[testmark]:# (0-assert)
```turtle
@prefix schema: <https://schema.org/> .

<http://example.org/Mick> schema:name "Michael"@en , "ミック・ジャガー"@jp , "მიკ ჯაგერი"@ka .
```
