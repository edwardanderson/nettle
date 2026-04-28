# Pre-formatted text

[testmark]:# (0-arrange)
```nettle
language en

http://example.org/app
  https://schema.org/text
    """
    for i in range(3):
      print(i)
    """
```

[testmark]:# (0-assert)
```turtle
@prefix schema: <https://schema.org/> .

<http://example.org/app> schema:text """for i in range(3):
     print(i)""" .
```
