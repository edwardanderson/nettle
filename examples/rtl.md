# Right-to-Left (RTL) Text

Nettle does not have explicit RTL features, but using the [alias](../docs/specification.md#alias) and [include](../docs/specification.md#include) directives may help minimise the mixing of LTR and RTL text.

```nettle
# prologue.ntl
prefix foaf http://xmlns.com/foaf/0.1/
alias ميك http://example.org/mick
alias كيث http://example.org/keith
alias يعرف foaf:knows
```

<pre dir="rtl">
include prologue.ntl

ميك
  يعرف
    كيث
</pre>

```turtle
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

<http://example.org/mick> foaf:knows <http://example.org/keith> .
```

> [!NOTE]
> Editors that support Unicode bidirectional rendering will naturally display Latin‑script directives (e.g., prefix, alias) in left‑to‑right order and Arabic script triples in right‑to‑left order, without affecting the logical byte order parsed by Nettle. Authors may use Unicode direction marks (e.g., U+200E, U+200F) for optional fine‑tuned display. Control characters such as U+202A–U+202E should generally be avoided, as they can alter the logical text order and break parsing or editor behaviour.
