[🠔 INDEX](index.md)
#

# Objects

## Neko Objects

Neko objects are basically just optimized hashtables, except they can also have an inheritance chain. Each field name is hashed into an integer for fast lookup.

## Creating Objects

Empty objects are easily created with a call to `$new`:

```js
var myobj = $new(null)
```

`$new` takes a single argument. If `null` is given, it constructs an empty object. If an object is given, it will create a copy of that object. That is, the new object will have the same set of fields as the old object, but they will reference the same values.

There is also this alternative syntax for creating a new object and populating some fields:

```js
var a = {
    test => "test",
    hello => function() {
        $print("Hello\n")
    }
}

a.hello();
```


## Fields

Setting and accessing fields on an object is simple with the dot syntax:

```js
var myobj = $new(null)

myobj.hello = function() { $print("Hello\n") }

myobj.test = "test"

myobj.hello()
```

However, if you are using Neko to implement a language, it will likely be more convenient to use the built-in setter and getters. You can also use a function to call a method on a specified object.

```js
var myobj = $new(null)

$objset(myobj, $hash("hello"), function() { $print("Hello\n") })

$objset(myobj, $hash("test"), "test")

var test = $objget(myobj, $hash("test"))

$objcall(myobj, $hash("hello"), $amake(0))
```

Note that field names need to be hashed before being passed into these functions. The `$hash` function returns a unique integer value for each string, but will always be the same for the same string.

You can also check for the existence of fields and remove them. However, this does not check an object's parent objects or affect them in any way.

```js
var myobj = $new(null)

$objset(myobj, $hash("test"), "test")

$objfield(myobj, $hash("test"))  // true

$objremove(myobj, $hash("test"))
```

It is also possible to get a list of an object's fields. The `$objfields` method will return a list of the object's fields, but be aware that it returns the hash values of the fields. The `$field` method will return the string value associated with the hash value.

```js
var myobj = $new(null)

$objset(myobj, $hash("test"), "test")

var fields = $objfields(myobj)

$print($field(fields[0]));
```

## Inheritance

Inheritance in Neko is handled by simply setting a parent object for a given object. When a field is accessed which does not exist in the current object, the object's parent will be checked.

```js
var myobj = $new(null)

myobj.hello = function() { $print("Hello\n") }

var obj2 = $new(null)

$objsetproto(obj2, myobj)

obj2.hello()
```

## This Value

Within any function called, the special variable `this` is set to the function's associated object (if there is one.) It is also possible to manually set `this` to any value desired.

```js
var myobj = $new(null)

myobj.test = "test"

myobj.hello = function() { 
    $print(this.test)
    this = "hello"
    $print(this)
}

myobj.hello();
```

## Operator Overloading

Some operations may be overridden using special field names. These are documented [here](https://nekovm.org/specs/objects/#operators-overloading).

## More Functions

All functions related to manipulating objects can be found [here](http://nekovm.org/doc/view/builtins#object).

#
[🠔 INDEX](index.md)