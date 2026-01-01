# Right-to-Left Text (RTL)

Nettle does not have explicit RTL features, but using the [alias](../docs/specification.md#alias) and [include](../docs/specification.md#include) directives can help minimise mixing LTR and RTL text.

`prologue.ntl`

```nettle
prefix foaf http://xmlns.com/foaf/0.1/
alias ميك http://example.org/mick
alias كيث http://example.org/keith
alias يعرف foaf:knows
```

<pre dir="rtl">
include /path/to/prologue.ntl

ميك
  يعرف
    كيث
</pre>


```turtle
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

<http://example.org/mick> foaf:knows <http://example.org/keith> .
```
