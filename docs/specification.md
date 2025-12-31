---
author: Edward Anderson
date: 2025-12-31
---

# Nettle 0.1.0

> [!CAUTION]
> Status: Draft

Nettle (Nested Triple Trees Language) is a compact, human-friendly concrete syntax for RDF. It expresses triples as indented trees so that related resources may be visually grouped.

- [Nettle 0.1.0](#nettle-010)
  - [Basics](#basics)
  - [Identifiers](#identifiers)
    - [Blank nodes](#blank-nodes)
  - [Predicate lists](#predicate-lists)
  - [Object lists](#object-lists)
  - [Literals](#literals)
    - [Language-tagged strings](#language-tagged-strings)
    - [Datatyped strings](#datatyped-strings)
  - [Collections](#collections)
  - [Named graphs](#named-graphs)
  - [Quoted triples](#quoted-triples)
  - [Comments](#comments)
  - [Directives](#directives)
    - [Prologue directives](#prologue-directives)
      - [alias](#alias)
      - [base](#base)
      - [include](#include)
      - [language](#language)
      - [prefix](#prefix)
      - [shapes](#shapes)
    - [Resource directives](#resource-directives)
      - [@inverse](#inverse)
  - [Notes](#notes)

## Basics

- Triples are written as trees: a subject on one line, one or more predicates indented under it, and one or more objects indented under each predicate
- Terms can be IRIs, prefixed names, aliases, or blank nodes
- Directives (prefix, base, alias, etc.) affect parsing

A simple triple:

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/knows
    http://example.org/keith
```

## Identifiers

Use absolute or relative IRIs, prefixed names (CURIEs), or aliases:

```nettle
base http://example.org/
prefix foaf http://xmlns.com/foaf/0.1/
prefix viaf http://viaf.org/viaf/
alias brian http://www.wikidata.org/entity/Q204943
alias bill viaf:54334218

http://example.org/mick # absolute IRI
  foaf:knows            # CURIE
    keith               # relative IRI
    brian               # alias
    bill                # alias
```

See also: [base](#base), [prefix](#prefix), [alias](#alias), [comments](#comments).

### Blank nodes

Square brackets denote a blank node. You may optionally give a local label to refer to the same blank node within the document. Unlabelled blank nodes are always unique.

```nettle
base http://example.org/
prefix schema https://schema.org/

mick
  knows
    [Keith]            # labelled blank node
      schema:birthDate
        "1943-12-18"
    []                 # unlabelled blank node
      schema:birthDate
        "1942-02-28"
```

See also: [base](#base), [prefix](#prefix), [literals](#literals), [comments](#comments).

## Predicate lists

Multiple predicates for the same subject may be grouped at the same level of indentation:

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/knows
    http://example.org/keith
  http://xmlns.com/foaf/0.1/name
    "Mick"
```

## Object lists

A predicate may have multiple objects. Each object is on its own indented line.

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/knows
    http://example.org/keith
    http://example.org/brian
```

## Literals

Literals must be wrapped in `"` quotation marks.

### Language-tagged strings

Provide a BCP-47 tag to specify the language of the string. Language tags override the [default language](#language).

```nettle
http://example.org/mick
  http://xmlns.com/foaf/0.1/name
    "Mick"@en
    "ミック・ジャガー"@jp
```

### Datatyped strings

Specify the datatype of a literal with an IRI, CURIE or [alias](#alias).

```nettle
http://example.org/mick
  https://schema.org/birthDate
    "1943-07-26" http://www.w3.org/2001/XMLSchema#date
```

## Collections

Ordered lists are written using parentheses. They may appear as subject or object. The preceding or following predicate may share the same line as the list's opening or closing bracket.

```nettle
base http://example.org/

mick
  educatedAt (
    Wentworth_Primary_School
    Dartford_Grammar_School
  )
```

See also: [identifiers](#identifiers), [base](#base).

## Named graphs

Triples collected as separate graphs are wrapped in curly braces. A graph name may be given as an identifier or a blank node. Triples outside of the curly braces or inside unlabelled graphs are part of the default graph.

```nettle
base http://example.org/

g1 {
  mick
    knows
      keith
}
```

See also: [identifiers](#identifiers), [blank nodes](#blank-nodes), [base](#base).

## Quoted triples

Quoted triples (reified/annotated triples) are written between `<<` and `>>`.

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

> [!NOTE]
> Reified triples are a feature of RDF 1.2 and may be ignored by parsers until that specification is finalised.

See also: [identifiers](#identifiers), [base](#base).

## Comments

Lines starting with `#` are comments and ignored.

## Directives

Directives are processed in document order.

### Prologue directives

#### alias

Give a short local name to an IRI or CURIE; aliases propagate when files are included.

`alias NAME IRI|CURIE`

See also: [include](#include); [example](../examples/alias.md).

#### base

Set the base namespace for resolving relative IRIs.

`base IRI`

See also: [example](../examples/base.md).

#### include

Import triples, prefixes, base and aliases from another document before continuing.

`include IRI`

See also: [example](../examples/include.md).

#### language

Default language tag for plain literals without explicit language or datatype.

`language TAG`

See also: [example](../examples/language.md).

#### prefix

Declare a namespace prefix.

`prefix NAME IRI`

#### shapes

Optional advisory pointer to a SHACL shapes file which a parser may use to validate the current document.

`shapes IRI`

### Resource directives

#### @inverse

Annotate a predicate to flip the subject/object direction for that occurrence only.

```nettle
guitar
  plays @inverse
    keith
```

`PREDICATE "@inverse"`

## Notes

- Blank node labels are local to the document and not preserved across serialisation
- The `include` directive merges content; behaviour on cycles is implementation-defined
- This specification focuses on readable syntax and intent. For edge cases and serialisation details consult implementation notes or tests
