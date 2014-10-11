<a name="module_array-tools"></a>
##array-tools
Useful functions for working with arrays

**Example**  
var a = require("array-tools");

* [array-tools](#module_array-tools)
  * [.without(input, toRemove)](#module_array-tools.without) ⇒ <code>Array</code>
  * [.pluck(arrayOfObjects, ...property)](#module_array-tools.pluck) ⇒ <code>Array</code>
  * [.arrayify(input)](#module_array-tools.arrayify) ⇒ <code>Array</code>
  * [.exists(array, value)](#module_array-tools.exists) ⇒ <code>boolean</code>
  * [.where(arrayOfObjects, query)](#module_array-tools.where) ⇒ <code>Array</code>
  * [.findWhere(arrayOfObjects, query)](#module_array-tools.findWhere) ⇒ <code>object</code>
  * [.pick(arrayOfObjects, ...property)](#module_array-tools.pick) ⇒ <code>Array.&lt;object&gt;</code>
  * [.union(array1, array2, idKey)](#module_array-tools.union) ⇒ <code>Array</code>
  * [.commonSequence(a, b)](#module_array-tools.commonSequence) ⇒ <code>Array</code>
  * [.unique(array)](#module_array-tools.unique) ⇒ <code>Array</code>
  * [.spliceWhile(array, index, test, ...elementN)](#module_array-tools.spliceWhile) ⇒ <code>Array</code>
  * [.extract(array, query)](#module_array-tools.extract) ⇒ <code>Array</code>
  * [.flatten()](#module_array-tools.flatten)

<a name="module_array-tools.without"></a>
###a.without(input, toRemove) ⇒ <code>Array</code>
Returns the input minus the specified values.

| Param | Type | Description |
| ----- | ---- | ----------- |
| input | <code>Array</code> | the input array |
| toRemove | <code>\*</code> | a single, or array of values to omit |

**Example**  
> a.without([ 1, 2, 3 ], 2)
[ 1, 3 ]
> a.without([ 1, 2, 3 ], [ 2, 3 ])
[ 1 ]
<a name="module_array-tools.pluck"></a>
###a.pluck(arrayOfObjects, ...property) ⇒ <code>Array</code>
Plucks the value of the specified property from each object in the input array

| Param | Type | Description |
| ----- | ---- | ----------- |
| arrayOfObjects | <code>Array.&lt;object&gt;</code> | the input array of objects |
| ...property | <code>string</code> | the property(s) to pluck |

**Example**  
> var data = [
...     {one: 1, two: 2},
...     {two: "two"},
...     {one: "one", two: "zwei"},
... ];
undefined
> a.pluck(data, "one");
[ 1, 'one' ]
> a.pluck(data, "two");
[ 2, 'two', 'zwei' ]
> a.pluck(data, "one", "two");
[ 1, 'two', 'one' ]
<a name="module_array-tools.arrayify"></a>
###a.arrayify(input) ⇒ <code>Array</code>
Takes input and guarantees an array back. Result can be one of three things:

- puts a single scalar in an array
- converts array-like object (e.g. `arguments`) to a real array
- converts `null` or `undefined` to an empty array

| Param | Type | Description |
| ----- | ---- | ----------- |
| input | <code>\*</code> | the input value to convert to an array |

**Example**  
> a.arrayify(null)
[]
> a.arrayify(0)
[ 0 ]
> a.arrayify([ 1, 2 ])
[ 1, 2 ]
> function f(){ return a.arrayify(arguments); }
undefined
> f(1,2,3)
[ 1, 2, 3 ]
<a name="module_array-tools.exists"></a>
###a.exists(array, value) ⇒ <code>boolean</code>
returns true if a value, or nested object value exists in an array

| Param | Type | Description |
| ----- | ---- | ----------- |
| array | <code>Array</code> | the array to search |
| value | <code>\*</code> | the value to search for |

**Example**  
> a.exists([ 1, 2, 3 ], 2)
true
> a.exists([ { result: false }, { result: false } ], { result: true })
false
> a.exists([ { result: true }, { result: false } ], { result: true })
true
> a.exists([ { result: true }, { result: true } ], { result: true })
true
<a name="module_array-tools.where"></a>
###a.where(arrayOfObjects, query) ⇒ <code>Array</code>
returns an array containing items from `arrayOfObjects` where key/value pairs 
from `query` are matched identically

| Param | Type | Description |
| ----- | ---- | ----------- |
| arrayOfObjects | <code>Array</code> | the array to search |
| query | <code>query</code> | an object containing the key/value pairs you want to match |

**Example**  
> dudes = [{ name: "Jim", age: 8}, { name: "Clive", age: 8}, { name: "Hater", age: 9}]
[ { name: 'Jim', age: 8 },
  { name: 'Clive', age: 8 },
  { name: 'Hater', age: 9 } ]
> a.where(dudes, { age: 8})
[ { name: 'Jim', age: 8 },
  { name: 'Clive', age: 8 } ]
<a name="module_array-tools.findWhere"></a>
###a.findWhere(arrayOfObjects, query) ⇒ <code>object</code>
returns the first item from `arrayOfObjects` where key/value pairs 
from `query` are matched identically

| Param | Type | Description |
| ----- | ---- | ----------- |
| arrayOfObjects | <code>Array</code> | the array to search |
| query | <code>query</code> | an object containing the key/value pairs you want to match |

**Example**  
> dudes = [{ name: "Jim", age: 8}, { name: "Clive", age: 8}, { name: "Hater", age: 9}]
[ { name: 'Jim', age: 8 },
  { name: 'Clive', age: 8 },
  { name: 'Hater', age: 9 } ]
> a.findWhere(dudes, { age: 8})
{ name: 'Jim', age: 8 }
<a name="module_array-tools.pick"></a>
###a.pick(arrayOfObjects, ...property) ⇒ <code>Array.&lt;object&gt;</code>
return a copy of the input `arrayOfObjects` containing objects having only the cherry-picked properties

| Param | Type | Description |
| ----- | ---- | ----------- |
| arrayOfObjects | <code>Array.&lt;object&gt;</code> | the input |
| ...property | <code>string</code> | the properties to include in the result |

**Example**  
> data = [
    { one: "un", two: "deux", three: "trois" },
    { two: "two", one: "one" },
    { four: "quattro" },
    { two: "zwei" }
]
> a.pick(data, "two")
[ { two: 'deux' },
  { two: 'two' },
  { two: 'zwei' } ]
<a name="module_array-tools.union"></a>
###a.union(array1, array2, idKey) ⇒ <code>Array</code>
merge two arrays into a single array of unique values

| Param | Type | Description |
| ----- | ---- | ----------- |
| array1 | <code>Array</code> | First array |
| array2 | <code>Array</code> | Second array |
| idKey | <code>string</code> | the unique ID property name |

**Example**  
> var array1 = [ 1, 2 ], array2 = [ 2, 3 ];
undefined
> a.union(array1, array2)
[ 1, 2, 3 ]
> var array1 = [ { id: 1 }, { id: 2 } ], array2 = [ { id: 2 }, { id: 3 } ];
undefined
> a.union(array1, array2)
[ { id: 1 }, { id: 2 }, { id: 3 } ]
> var array2 = [ { id: 2, blah: true }, { id: 3 } ]
undefined
> a.union(array1, array2)
[ { id: 1 },
  { id: 2 },
  { id: 2, blah: true },
  { id: 3 } ]
> a.union(array1, array2, "id")
[ { id: 1 }, { id: 2 }, { id: 3 } ]
<a name="module_array-tools.commonSequence"></a>
###a.commonSequence(a, b) ⇒ <code>Array</code>
Returns the initial elements which both input arrays have in common

| Param | Type | Description |
| ----- | ---- | ----------- |
| a | <code>Array</code> | first array to compare |
| b | <code>Array</code> | second array to compare |

**Example**  
> a.commonSequence([1,2,3], [1,2,4])
[ 1, 2 ]
<a name="module_array-tools.unique"></a>
###a.unique(array) ⇒ <code>Array</code>
reduces an array to unique values

| Param | Type | Description |
| ----- | ---- | ----------- |
| array | <code>Array</code> | input array |

**Example**  
> n = [1,6,6,7,1]
[ 1, 6, 6, 7, 1 ]
> a.unique(n)
[ 1, 6, 7 ]
<a name="module_array-tools.spliceWhile"></a>
###a.spliceWhile(array, index, test, ...elementN) ⇒ <code>Array</code>
splice from `index` until `test` fails

| Param | Type | Description |
| ----- | ---- | ----------- |
| array | <code>Array</code> | the input array |
| index | <code>number</code> | the position to begin splicing from |
| test | <code>RegExp</code> | the test to continue splicing while true |
| ...elementN | <code>\*</code> | the elements to add to the array |

**Example**  
> letters = ["a", "a", "b"]
[ 'a', 'a', 'b' ]
> a.spliceWhile(letters, 0, /a/, "x")
[ 'a', 'a' ]
> letters
[ 'x', 'b' ]
<a name="module_array-tools.extract"></a>
###a.extract(array, query) ⇒ <code>Array</code>
Removes items from `array` which satisfy the query. Modifies the input array, returns the extracted.

| Param | Type | Description |
| ----- | ---- | ----------- |
| array | <code>Array</code> | the input array, modified directly |
| query | <code>function</code> \| <code>object</code> | Per item in the array, if either the function returns truthy or the exists query is satisfied, the item is extracted |

**Returns**: <code>Array</code> - the extracted items.  
<a name="module_array-tools.flatten"></a>
###a.flatten()
flatten

**Since**: 1.4.0  
**Todo**

- document
