# Right-to-Left Text (RTL)

Nettle does not have explicit RTL features, but using the [alias](../docs/specification.md#alias) and [include](../docs/specification.md#include) directives may help minimise mixing LTR and RTL text.

[testmark]:# (0-arrange)
```nettle
# prologue.ntl
prefix foaf http://xmlns.com/foaf/0.1/
alias ميك http://example.org/mick
alias كيث http://example.org/keith
alias يعرف foaf:knows

ميك
  يعرف
    كيث
```

<pre dir="rtl">
prefix foaf http://xmlns.com/foaf/0.1/
alias ميك http://example.org/mick
alias كيث http://example.org/keith
alias يعرف foaf:knows

ميك
  يعرف
    كيث
</pre>


<pre dir="rtl">
include prologue.ntl

ميك
  يعرف
    كيث
</pre>

[testmark]:# (0-assert)
```turtle
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

<http://example.org/mick> foaf:knows <http://example.org/keith> .
```
