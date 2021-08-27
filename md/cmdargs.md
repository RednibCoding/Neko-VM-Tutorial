[🠔 INDEX](index.md) | [OVERVIEW](overview.md)
#

# Commandline Args

### Accessing Commandline Arguments

Arguments passed into a Neko application via the commandline are stored as strings in an array on the `$loader` object.

For example, running this

```js
$print($loader.args)
```

like this

    neko cmdargs.n hello world!

results in

    [hello,world!]

#

[🠔 INDEX](index.md) | [OVERVIEW](overview.md)