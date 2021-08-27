[🠔 INDEX](index.md) | [OVERVIEW](overview.md)
#

# NXML

## What is NXML

[NXML](http://nekovm.org/doc/nxml) is based on XML and is representing a Neko Abstract Syntax Tree (AST).
So when generating an AST from your language, you can generate an AST in NXML-format.
After you have generated the NXML file from your language, you can directly compile it
to neko bytecode. This comes in pretty handy as from a language designer point of view,
your job is pretty much done after the AST generation part.

## Why NXML
Neko sources syntax is easy to read, though can sometimes be difficult to generate. Also, NXML does allow embedding file and line number information. For example, if you generate from a file in your language MyFile.mylang to myfile.neko you would like to get error traces in terms of position in the original MyFile.mylang file.

## How to use NXML
A NXML file must follow a few rules in order to be valid. Basically it is like XML.

- Each file must
start with an opening `<nxml>`-tag and end with a closing `</nxml>`-tag.
- There must be at least one tag that contains file/line information (the `p`-attribute).
- A NXML file is just a file that contains nxml syntax and also has the `.neko` file extension.

## Example
Lets say we want to represent the following code in NXML...

*hello.neko*
```js
$print("Hello, NXML\n")
```

we would write it as follows:

*hello.neko*
```xml
<nxml>
    <c p="hello.my:2">  // at least one tag with a p attribute
        <v v="$print"/>
        <s v="Hello, nxml!\n"/>
    </c>
</nxml>
```

Now we can compile it like a regular `.neko` file:
```
>> necoc hello.neko
```
This will produce a `.n` file as usual. And you can run it as always with:
```
>> neko hello.n

  Hello nxml!

```

## NXML Nodes
In order to use the NXML syntax, you need to start with `<nxml>` and finish with `</nxml>`. All NXML nodes inside the `nxml` pair are Neko expressions. An NXML block is like a Neko block. For example, `<nxml></nxml>` is the equivalent of the empty Neko block { }.

Existing nodes are the following:
- `<i v="3"/>` the literal integer 3
- `<f v="1.5"/>` the literal float 1.5
- `<s v="a string"/>` the literal string a string
- `<v v="id"/>` the identifier id (includes special identifiers such as null, true, false and this)
- `<b>e1 e2 e3...</b>` a block having several subexpressions
- `<p>e</p>` parentheses around a subexpression
- `<g v="field">e</g>` field access of a subexpression (e).field
- `<c>e0 e1 e2 e3...</c>` call of e0(e1,e2,e3...)
- `<a>e1 e2</a>` array access e1[e2]
- `<var><v v="x">e</v><v v="y"/></var>` local variable declaration, equivalent to var x = e, y
- `<while>e1 e2</while>` while loop : while e1 e2
- `<do>e1 e2</do>` do...while loop : do e1 while e2
- `<if>e0 e1</if>` equivalent to if e0 e1
- `<if>e0 e1 e2</if>` equivalent to if e0 e1 else e2
- `<o v="*">e1 e2</o>` a binary operation such as e1 * e2
- `<try v="exc">e1 e2</try>` a try..catch block try e1 catch exc e2
- `<function v="x:y:z">e</function>` a function declaration such as function(x,y,z) e
- `<return/>` the return statement without an expression
- `<return>e</return>` return with an expression value
- `<break/>` the break statement without an expression
- `<break>e</break>` break with an expression value
- `<continue/>` the continue statement
- `<next>e1 e2</next>` a way to tie two expressions together (such as e1;e2)
- `<label v="here"/>` the goto label here:
- `<switch>e0 <case>e1 e2</case> <case>e1 e2</case> <default>edef</default></switch>` a switch with several cases and an optional default
- `<object><v v="f0"><i v="42"/></v><v v="f1"><s v="foo"/></v></object>` an object literal, equivalent to the neko code { f0 => 42, f1 => "foo" }
- `<neko>....</neko> neko source can be embedded into a %%<!CDATA[[...]]%%>` section


## File Position
The additional attribute p can be placed on every NXML node in order to specify the original file and line the expression is generated from. For example `<i v="33" p="myfile.l:478"/>` is the integer 33 referenced in myfile.l at line 478.

**But there must be at least one node with a `p` attribute in the file. Otherwise, it will produce an error.**

When encountered, such position is stored and remains valid for all NXML nodes. For example, `<nxml><i v="33" p="myfile.l:478"/><i v="34"/></nxml>` is listing two integers from myfile.l, both at line 478.

If you don't specify the filename in the p attribute, it's considered to be a number of lines skipped since the last p information. For example, `<nxml><i v="33" p="myfile.l:478"/><i v="34" p="2"/></nxml>` is listing two integers from myfile.l, the first 33 at line 478 and the second 34 at line 480 (478 + 2).

#
[🠔 INDEX](index.md) | [OVERVIEW](overview.md)