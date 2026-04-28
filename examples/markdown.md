# Markdown

Lowering Markdown to HTML is implementation-defined.

[testmark]:# (0-arrange)
```nettle
base http://example.org/
prefix dc http://purl.org/dc/terms/

Mick
  dc:description
    > **Sir Michael Philip Jagger** is an English musician, songwriter, and film producer.
```

[testmark]:# (0-assert)
```turtle
@prefix dc: <http://purl.org/dc/terms/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<http://example.org/Mick> dc:description "<p><strong>Sir Michael Philip Jagger</strong> is an English musician, songwriter, and film producer.</p>"^^rdf:HTML .
```

## Language

> [!NOTE]
> Nettle does not specify how to describe the language of Markdown content.

> [!NOTE]
> A default `language` in the prologue does not annotate the language of the Markdown content.
