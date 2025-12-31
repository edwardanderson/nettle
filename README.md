# Nettle

Nettle (Nested Triple Trees Language) is a concrete RDF syntax that organises triples with hierarchical indentation.

Refer to the [Specification](docs/specification.md).

## Example

```nettle
language en
base http://example.org/
prefix ex http://example.org/
prefix schema https://schema.org/
prefix wd http://www.wikidata.org/entity/
prefix xsd http://www.w3.org/2001/XMLSchema#
alias knows <http://xmlns.com/foaf/0.1/knows>
alias Keith wd:Q189599

Mick
  a
    schema:Person
  schema:name
    "Sir Michael Philip Jagger"
    "ミック・ジャガー"@jp
  schema:birthDate
    "1943-07-26" xsd:date
  knows
    Keith
      schema:name
        "Keith"
  schema:description
    "Sir Michael Philip Jagger (born 26 July 1943) is an English musician, songwriter, and film producer.
    He is the lead singer and one of the founder members of the Rolling Stones."
  ex:educatedAt (
    [Wentworth]
      schema:name
        "Wentworth Primary School"
    [Dartford]
      schema:name
        "Dartford Grammar School"
  )

g1 {
  Dartford
    schema:containsPlace
      [Wentworth]
      [Dartford]
}

<<
  Mick
    schema:birthPlace
      Dartford
>>
  ex:accordingTo
    https://en.wikipedia.org/w/index.php?title=Mick_Jagger&oldid=1325054665
```

```trig
@version "1.2" .
@prefix ex: <http://example.org/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix schema: <https://schema.org/> .
@prefix wd: <http://www.wikidata.org/entity/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<http://example.org/Mick> a schema:Person ;
    schema:name "Sir Michael Philip Jagger"@en , "ミック・ジャガー"@jp ;
    schema:birthDate "1943-07-26"^^xsd:date ;
    foaf:knows wd:Q189599 ;
    schema:description "Sir Michael Philip Jagger (born 26 July 1943) is an English musician, songwriter, and film producer.\nHe is the lead singer and one of the founder members of the Rolling Stones."@en ;
    ex:educatedAt ( _:b0 , _:b1 ) .

_:b0 schema:name "Wentworth Primary School"@en .

_:b1 schema:name "Dartford Grammar School"@en .

wd:Q189599 schema:name "Keith"@en .

<http://example.org/g1> {
  <http://example.org/Dartford> schema:containsPlace _:b0 , _:b1 .
}

<< <http://example.org/Mick> schema:birthPlace <http://example.org/Dartford> >> ex:accordingTo <https://en.wikipedia.org/w/index.php?title=Mick_Jagger&oldid=1325054665> .
```
