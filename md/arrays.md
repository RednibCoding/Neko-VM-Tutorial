
[🠔 INDEX](../readme)
#

# Arrays

## Neko Arrays

Arrays are zero-indexed lists of values, which may be heterogenous. They do not resize automatically.

## Creating Arrays

There are a couple ways to create arrays in Neko. The first is to use `$array` and pass in all the values you wish to have in the array. This will create an array of exactly the needed length with the values in the order they are given.

```js
var a = $array(1, "2", function() { "3" });

$print(a);
```

The second method is to create an empty array of a particular size. The array will be populated with `null` values.

```js
var a = $amake(3);

$print(a);
```

An array can also be created via a shallow copy.

```js
var a = $array(1, "2", function() { "3" });
var b = $acopy(a);

$print(b);
```

## Accessing Array Elements

Array elements may be accessed using the usual bracket notation (`[]`) and positive integers. For any non-existent indexes, `null` will be returned.

```js
var a = $array(1, "2", function() { "3" });

$print(a[1]);

a[1] = "3";

$print(a[1]);
```

Multiple elements may be retrieved using `$asub`, which takes a starting position and length. However, indexes or lengths that are out of range will cause an error.

```js
var a = $array(1, "2", function() { "3" });

$print(a[1,2]);
```

## Combining Arrays

Arrays can be copied into each other using the `$ablit` function. This function allows one to copy any portion of one array into another array, starting at a certain index. If the copy will not fit, the function throws an error.

```js
var a = $array(1, 2, 3);
var b = $array(4, 5, 6);

$ablit(a, 1, b, 1, 2);

$print(a); // prints [1, 5, 6]
```

Arrays may also be concatenated. This will create a new array which is a shallow copy of both arrays added together. Note that the `$aconcat` function takes a single argument, which should be an array of arrays.

```js
var a = $array(1, 2, 3);
var b = $array(4, 5, 6);

var c = $aconcat($array(a, b));

$print(c); // prints [1, 2, 3, 4, 5, 6]
```

## Function Documentation

See [here](http:// nekovm.org/doc/view/builtins#array) for details of the array functions.

#
[🠔 INDEX](../readme)