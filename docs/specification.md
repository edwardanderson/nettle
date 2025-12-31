---
author: Edward Anderson
date: 2025-12-31
---

# Nettle 0.1.0

**Status:** Draft

---

- [Nettle 0.1.0](#nettle-010)
  - [Simple Triples](#simple-triples)
  - [IRIs](#iris)
  - [Blank Nodes](#blank-nodes)
  - [Predicate Lists](#predicate-lists)
  - [Object Lists](#object-lists)
  - [Collections](#collections)
  - [Named Graphs](#named-graphs)
  - [Quoted Triples](#quoted-triples)
  - [Comments](#comments)
  - [Directives](#directives)
    - [Prologue](#prologue)
      - [alias](#alias)
      - [base](#base)
      - [include](#include)
      - [language](#language)
      - [prefix](#prefix)
      - [shapes](#shapes)
    - [Tree](#tree)
      - [`@inverse`](#inverse)

## Simple Triples

The simplest triple statement is a tree of (subject, predicate, object) terms separated by significant whitespace. Terms may be [IRIs](#iris), CURIEs, [aliases](#alias), or [blank nodes](#blank-nodes).

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/knows
    http://example.org/keith
```

## IRIs

IRIs may be written as relative or absolute IRIs, or as prefixed names.

```nettle
base http://example.org/
prefix foaf http://xmlns.com/foaf/0.1/

mick
  foaf:knows
    http://example.org/keith
```

## Blank Nodes

Blank nodes are indicated by `[]`. A label may be given inside the brackets so that the same node can be referred to in the current document. Blank node labels are not preserved across serialisation.

```nettle
base http://example.org/

mick
  sibling
    [Chris]
      schema:birthDate
        "1947-12-19"
```

## Predicate Lists

These two examples are equivalent ways of writing the triples about Mick.

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/knows
    http://example.org/keith
  http://xmlns.com/foaf/0.1/name
    "Mick"
```

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/knows
    http://example.org/keith
http://example.org/mick
  http://xmlns.com/foaf/0.1/name
    "Mick"
```

## Object Lists

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/name
    "Mick"
    "ミック・ジャガー"@jp
```

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/name
    "mick"
http://example.org/mick
  http://xmlns.com/foaf/0.1/name
    "ミック・ジャガー"@jp
```

## Collections

Sequences of resources may be declared using lists of terms inside `()` in the subject or object position of a triple. Preceding or following predicates my be written on the same line as the opening or closing bracket.

```nettle
base http://example.org/

mick
  educatedAt (
    Wentworth_Primary_School
    Dartford_Grammar_School
    London_School_of_Economics
  )
```

```nettle
base http://example.org/

(
  Wentworth_Primary_School
  Dartford_Grammar_School
  London_School_of_Economics
)
  educated
    mick
```

## Named Graphs

```nettle
base http://example.org/

g1 {
  mick
    knows
      keith
}
```

## Quoted Triples

```nettle
base http://example.org/

<<
  mick
    birthPlace
      dartford
>>
  accordingTo
    https://en.wikipedia.org/w/index.php?title=Mick_Jagger&oldid=1325054665
```

## Comments

Comments must be prefixed with `#`.

```
# This is a comment.
```

## Directives

Directives are processed in document order.

### Prologue

#### alias

The `alias` directive declares a local name for an IRI. Aliases propagate transitively when the [`include`](#include) directive is used. If the same alias is declared multiple times, the later declaration overrides earlier ones.

```nettle
prefix wd http://www.wikidata.org/entity/
alias mick wd:Q128121
alias knows <http://xmlns.com/foaf/0.1/knows>
alias keith wd:Q189599

mick
  knows
    keith
```

#### base

The `base` directive sets a base IRI against which relative IRIs are resolved.

#### include

The `include` directive imports triples, prefixes, base IRIs, and aliases from another Nettle or RDF document, merging them into the current dataset. `include` directives are processed before subsequent triples in the current document.

```nettle
include http://exmaple.org/data/example.ttl
```

Behaviour when `include` directives form cycles is implementation-defined.

#### language

The `language` directive sets a default language for all literals which do not have a specific language tag or datatype.

#### prefix

The `prefix` directive defines a label for a namespace.

```nettle
prefix ex http://example.org

ex:mick
  a
    ex:person
```

#### shapes

The `shapes` directive identifies a SHACL shape that may be used to validate the current graph. The directive is advisory and does not affect RDF graph construction.

```nettle
shapes http://example.org/shapes/example.ttl
```

### Tree

#### `@inverse`

The `@inverse` directive is an in-line predicate keyword for reversing the direction of the annotated predicate in the current triple. The directive does not affect the behaviour of other predicates nor unannotated instances of the same predicate.

```nettle
base http://example.org/

mick
  knows @inverse
    keith
```
