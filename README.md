# Nettle

Nettle (Nested Triple Trees Language) is a compact, human-friendly syntax for authoring RDF graphs. It expresses triples as whitespace-indented trees so that related resources may be visually grouped.

Refer to the [Nettle 0.2.0](docs/specification.md) specification.

## Features

- Significant whitespace for readability
- Simplified syntax to reduce the number of special characters
- `include` directive for modular composition
- `shapes` directive for validation hinting
- `alias` directive for identity management
- `@inverse` predicate annotation for materialising a triple in reverse
- Named graphs
- Ordered lists (collections)
- Annotations (reification)

## Example

```nettle
base http://example.org/

prefixes
  owl http://www.w3.org/2002/07/owl#
  schema https://schema.org/
  wd http://www.wikidata.org/entity/

aliases
  Brian wd:Q204943
  date http://www.w3.org/2001/XMLSchema#date

Mick
  a
    schema:Person
  schema:name
    "Sir Michael Philip Jagger"@en
  schema:description
    > **Sir Michael Philip Jagger** is an English musician, songwriter, and film producer.
  knows
    Keith
      schema:birthDate
        "1943-12-18" date
    Brian
      schema:birthDate
        "1942-02-28" date
    [Bill]
      schema:birthDate
        "1936-10-24" date
    https://viaf.org/viaf/102199951
      schema:birthDate
        "1941-06-02" date
  owl:sameAs
    wd:Q128121
```

```turtle
@prefix ex: <http://example.org/> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix schema: <https://schema.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<http://example.org/Mick> a schema:Person ;
    schema:name "Sir Michael Philip Jagger"@en ;
    schema:description "<p><strong>Sir Michael Philip Jagger</strong> is an English musician, songwriter, and film producer.</p>"^^rdf:HTML ;
    ex:knows <http://example.org/Keith> , <http://www.wikidata.org/entity/Q204943> , [
      schema:birthDate "1936-10-24"^^xsd:date
    ] , <https://viaf.org/viaf/102199951> ;
    owl:sameAs <http://www.wikidata.org/entity/Q128121> .

<http://www.wikidata.org/entity/Q204943> schema:birthDate "1942-02-28"^^xsd:date .

<http://example.org/Keith> schema:birthDate "1943-12-18"^^xsd:date .

<https://viaf.org/viaf/102199951> schema:birthDate "1941-06-02"^^xsd:date .
```

## Licence

`CC-BY-4.0`
