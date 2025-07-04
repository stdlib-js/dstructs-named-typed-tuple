<!--

@license Apache-2.0

Copyright (c) 2018 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# Named Typed Tuple

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Create a factory for generating named typed tuples.

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

Named tuples assign a property name, and thus a meaning, to each position in a tuple and allow for more readable, self-documenting code.

Named typed tuples can be used wherever [typed arrays][@stdlib/array/typed] are used, with the added benefit that they allow accessing fields by both field name and position index.

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->

<section class="installation">

## Installation

```bash
npm install @stdlib/dstructs-named-typed-tuple
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

## Usage

```javascript
var namedtypedtuple = require( '@stdlib/dstructs-named-typed-tuple' );
```

<a name="main"></a>

#### namedtypedtuple( fields\[, options] )

Returns a named typed tuple factory.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var x = tuple.x;
// returns 1.0

x = tuple[ 0 ];
// returns 1.0

var y = tuple.y;
// returns -1.0

y = tuple[ 1 ];
// returns -1.0
```

The function accepts the following `options`:

-   **dtype**: default tuple data type. If a data type is not provided to a named typed tuple factory, this option specifies the underlying tuple data type. The following data types are supported:

    -   `float64`: double-precision floating-point numbers (IEEE 754).
    -   `float32`: single-precision floating-point numbers (IEEE 754).
    -   `int32`: 32-bit two's complement signed integers.
    -   `uint32`: 32-bit unsigned integers.
    -   `int16`: 16-bit two's complement signed integers.
    -   `uint16`: 16-bit unsigned integers.
    -   `int8`: 8-bit two's complement signed integers.
    -   `uint8`: 8-bit unsigned integers.
    -   `uint8c`: 8-bit unsigned integers clamped to 0-255.

    Default: `'float64'`.

-   **name**: tuple name. Default: `'tuple'`.

* * *

### Tuple Factory

<a name="factory"></a>

#### factory()

Returns a named typed tuple of the default data type.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory();

var x = tuple.x;
// returns 0.0

x = tuple[ 0 ];
// returns 0.0

var y = tuple.y;
// returns 0.0

y = tuple[ 1 ];
// returns 0.0
```

#### factory( dtype )

Returns a named typed tuple of the specified data type.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( 'int32' );

var x = tuple.x;
// returns 0

x = tuple[ 0 ];
// returns 0

var y = tuple.y;
// returns 0

y = tuple[ 1 ];
// returns 0
```

#### factory( typedarray\[, dtype] )

Returns a named typed tuple from a [typed array][@stdlib/array/typed].

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( new Float64Array( [ 1.0, -1.0 ] ) );

var x = tuple.x;
// returns 1.0

x = tuple[ 0 ];
// returns 1.0

var y = tuple.y;
// returns -1.0

y = tuple[ 1 ];
// returns -1.0
```

To override the default tuple data type (and potentially cast [typed array][@stdlib/array/typed] values to another data type), provide a `dtype`.

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var factory = namedtypedtuple( [ 'x', 'y' ] );

// Cast double-precision floating-point numbers to signed 32-bit integers:
var tuple = factory( new Float64Array( [ 1.0, -1.0 ] ), 'int32' );

var x = tuple.x;
// returns 1

x = tuple[ 0 ];
// returns 1

var y = tuple.y;
// returns -1

y = tuple[ 1 ];
// returns -1
```

#### factory( obj\[, dtype] )

Returns a named typed tuple from an array-like object or iterable.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var x = tuple.x;
// returns 1.0

x = tuple[ 0 ];
// returns 1.0

var y = tuple.y;
// returns -1.0

y = tuple[ 1 ];
// returns -1.0
```

To override the default tuple data type, provide a `dtype`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ], 'int32' );

var x = tuple.x;
// returns 1

x = tuple[ 0 ];
// returns 1

var y = tuple.y;
// returns -1

y = tuple[ 1 ];
// returns -1
```

#### factory( buffer\[, byteOffset]\[, dtype] )

Returns a named typed tuple view of an [`ArrayBuffer`][@stdlib/array/buffer] where the view length equals the number of tuple fields.

```javascript
var ArrayBuffer = require( '@stdlib/array-buffer' );

var factory = namedtypedtuple( [ 'x', 'y' ] );

var buf = new ArrayBuffer( 32 );

// Create a tuple view of the first 16 bytes (8 bytes per double):
var tuple = factory( buf );

var x = tuple.x;
// returns 0.0

x = tuple[ 0 ];
// returns 0.0

var y = tuple.y;
// returns 0.0

y = tuple[ 1 ];
// returns 0.0

// Create a tuple view of the last 16 bytes:
tuple = factory( buf, 16 );

x = tuple.x;
// returns 0.0

x = tuple[ 0 ];
// returns 0.0

y = tuple.y;
// returns 0.0

y = tuple[ 1 ];
// returns 0.0
```

To override the default tuple data type, provide a `dtype`.

```javascript
var ArrayBuffer = require( '@stdlib/array-buffer' );

var factory = namedtypedtuple( [ 'x', 'y' ] );

var buf = new ArrayBuffer( 16 );

// Create a tuple view of the first 8 bytes (4 bytes per float):
var tuple = factory( buf, 'float32' );

var x = tuple.x;
// returns 0.0

x = tuple[ 0 ];
// returns 0.0

var y = tuple.y;
// returns 0.0

y = tuple[ 1 ];
// returns 0.0

// Create a tuple view of the last 8 bytes:
tuple = factory( buf, 8, 'float32' );

x = tuple.x;
// returns 0.0

x = tuple[ 0 ];
// returns 0.0

y = tuple.y;
// returns 0.0

y = tuple[ 1 ];
// returns 0.0
```

<a name="static-method-from"></a>

#### factory.from( src\[, map\[, thisArg]] )

Creates a new named typed tuple from an array-like `object` or an iterable.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory.from( [ 1.0, -1.0 ] );

var x = tuple.x;
// returns 1.0

x = tuple[ 0 ];
// returns 1.0

var y = tuple.y;
// returns -1.0

y = tuple[ 1 ];
// returns -1.0
```

To invoke a function for each `src` value, provide a callback function.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

function mapFcn( v ) {
    return v * 2.0;
}

var tuple = factory.from( [ 1.0, -1.0 ], mapFcn );

var x = tuple.x;
// returns 2.0

x = tuple[ 0 ];
// returns 2.0

var y = tuple.y;
// returns -2.0

y = tuple[ 1 ];
// returns -2.0
```

A callback function is provided three arguments:

-   `value`: source value.
-   `index`: source index.
-   `field`: tuple field.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

function mapFcn( v ) {
    this.count += 1;
    return v * 2.0;
}

var ctx = {
    'count': 0
};

var tuple = factory.from( [ 1.0, -1.0 ], mapFcn, ctx );

var n = ctx.count;
// returns 2
```

<a name="static-method-from-object"></a>

#### factory.fromObject( obj\[, map\[, thisArg]] )

Creates a new named typed tuple from an `object` containing tuple fields.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var obj = {
    'x': 1.0,
    'y': -1.0
};

var tuple = factory.fromObject( obj );

var x = tuple.x;
// returns 1.0

x = tuple[ 0 ];
// returns 1.0

var y = tuple.y;
// returns -1.0

y = tuple[ 1 ];
// returns -1.0
```

To invoke a function for each `src` object tuple field, provide a callback function.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

function mapFcn( v ) {
    return v * 2.0;
}

var obj = {
    'x': 1.0,
    'y': -1.0
};

var tuple = factory.fromObject( obj, mapFcn );

var x = tuple.x;
// returns 2.0

x = tuple[ 0 ];
// returns 2.0

var y = tuple.y;
// returns -2.0

y = tuple[ 1 ];
// returns -2.0
```

A callback function is provided two arguments:

-   `value`: source object tuple field value.
-   `field`: source object tuple field name.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

function mapFcn( v ) {
    this.count += 1;
    return v * 2.0;
}

var obj = {
    'x': 1.0,
    'y': -1.0
};

var ctx = {
    'count': 0
};

var tuple = factory.fromObject( obj, mapFcn, ctx );

var n = ctx.count;
// returns 2
```

<a name="static-method-of"></a>

#### factory.of( element0\[, element1\[, ...elementN]] )

Creates a new named typed tuple from a variable number of arguments.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory.of( 1.0, -1.0 );

var x = tuple.x;
// returns 1.0

x = tuple[ 0 ];
// returns 1.0

var y = tuple.y;
// returns -1.0

y = tuple[ 1 ];
// returns -1.0
```

* * *

### Tuple

<a name="prop-bytes-per-element"></a>

#### tuple.BYTES_PER_ELEMENT

Size (in bytes) of each tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var nbytes = tuple.BYTES_PER_ELEMENT;
// returns 8
```

<a name="prop-buffer"></a>

#### tuple.buffer

Pointer to the underlying data buffer.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var buf = tuple.buffer;
// returns <ArrayBuffer>
```

<a name="prop-byte-length"></a>

#### tuple.byteLength

Length (in bytes) of the tuple.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var nbytes = tuple.byteLength;
// returns 16
```

<a name="prop-byte-offset"></a>

#### tuple.byteOffset

Offset (in bytes) of a tuple from the start of its underlying [`ArrayBuffer`][@stdlib/array/buffer].

```javascript
var ArrayBuffer = require( '@stdlib/array-buffer' );

var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var offset = tuple.byteOffset;
// returns 0

var buf = new ArrayBuffer( 64 );
tuple = factory( buf, 32 );

offset = tuple.byteOffset;
// returns 32
```

<a name="prop-length"></a>

#### tuple.length

Number of tuple elements.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var len = tuple.length;
// returns 2
```

<a name="prop-name"></a>

#### tuple.name

Tuple name.

```javascript
// Create a tuple factory which generates tuples having the default tuple name:
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var n = tuple.name;
// returns 'tuple'

// Create a tuple factory which generates tuples having a custom tuple name:
var opts = {
    'name': 'Point'
};
factory = namedtypedtuple( [ 'x', 'y' ], opts );

tuple = factory( [ 1.0, -1.0 ] );

n = tuple.name;
// returns 'Point'
```

<a name="prop-fields"></a>

#### tuple.fields

Returns the list of tuple fields.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

var fields = tuple.fields;
// returns [ 'x', 'y' ]
```

<a name="prop-ordered-fields"></a>

#### tuple.orderedFields

Returns the list of tuple fields in index order.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

// Sort tuple elements in ascending order:
tuple.sort();

// Get the list of tuple fields:
var fields = tuple.fields;
// returns [ 'x', 'y' ]

// Get the list of tuple fields in index order:
fields = tuple.orderedFields;
// returns [ 'y', 'x' ]
```

<a name="method-copy-within"></a>

#### tuple.copyWithin( target, start\[, end] )

Copies a sequence of elements within the tuple starting at `start` and ending at `end` (non-inclusive) to the position starting at `target`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 2.0, -2.0, 1.0, -1.0, 1.0 ] );

var x = tuple.x;
// returns 2.0

var y = tuple.y;
// returns -2.0

// Copy the last two elements to the first two elements:
tuple.copyWithin( 0, 3 );

x = tuple.x;
// returns -1.0

y = tuple.y;
// returns 1.0
```

By default, `end` equals the number of tuple elements (i.e., one more than the last tuple index). To limit the sequence length, provide an `end` argument.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 2.0, -2.0, 1.0, -1.0, 1.0 ] );

var w = tuple.w;
// returns -1.0

var v = tuple.v;
// returns 1.0

// Copy the first two elements to the last two elements:
tuple.copyWithin( 3, 0, 2 );

w = tuple.w;
// returns 2.0

v = tuple.v;
// returns -2.0
```

When a `target`, `start`, and/or `end` index is negative, the respective index is determined relative to the last tuple element. The following example achieves the same behavior as the previous example:

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 2.0, -2.0, 1.0, -1.0, 1.0 ] );

var w = tuple.w;
// returns -1.0

var v = tuple.v;
// returns 1.0

// Copy the first two elements to the last two elements:
tuple.copyWithin( -2, -5, -3 );

w = tuple.w;
// returns 2.0

v = tuple.v;
// returns -2.0
```

<a name="method-entries"></a>

#### tuple.entries()

Returns an iterator for iterating over tuple key-value pairs.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

// Create an iterator:
var it = tuple.entries();

// Iterate over key-value pairs...
var v = it.next().value;
// returns [ 0, 'x', 1.0 ]

v = it.next().value;
// returns [ 1, 'y', -1.0 ]

var bool = it.next().done;
// returns true
```

<a name="method-every"></a>

#### tuple.every( predicate\[, thisArg] )

Tests whether all tuple elements pass a test implemented by a `predicate` function.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

function predicate( v ) {
    return ( v >= 0.0 );
}

var bool = tuple.every( predicate );
// returns false
```

A `predicate` function is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, 1.0 ] );

function predicate( v ) {
    this.count += 1;
    return ( v >= 0.0 );
}

var ctx = {
    'count': 0
};

var bool = tuple.every( predicate, ctx );
// returns true

var n = ctx.count;
// returns 2
```

<a name="method-field-of"></a>

#### tuple.fieldOf( searchElement\[, fromIndex] )

Returns the field of the first tuple element strictly equal to a search element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var field = tuple.fieldOf( -1.0 );
// returns 'z'

field = tuple.fieldOf( 2.0 );
// returns undefined
```

By default, the method searches the entire tuple (`fromIndex = 0`). To begin searching from a specific tuple index, provide a `fromIndex`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var field = tuple.fieldOf( 1.0, 1 );
// returns undefined
```

When a `fromIndex` is negative, the starting index is resolved relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var field = tuple.fieldOf( 1.0, -2 );
// returns undefined
```

The method does **not** distinguish between signed and unsigned zero.

<a name="method-fill"></a>

#### tuple.fill( value\[, start\[, end]] )

Fills a tuple from a `start` index to an `end` index (non-inclusive) with a provided `value`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory();

// Set all tuple elements to the same value:
tuple.fill( 2.0 );

var x = tuple.x;
// returns 2.0

var y = tuple.y;
// returns 2.0

// Set all tuple elements starting from the first index to the same value:
tuple.fill( 3.0, 1 );

x = tuple.x;
// returns 2.0

y = tuple.y;
// returns 3.0

// Set all tuple elements, except the last element, to the same value:
tuple.fill( 4.0, 0, tuple.length-1 );

x = tuple.x;
// returns 4.0

y = tuple.y;
// returns 3.0
```

When a `start` and/or `end` index is negative, the respective index is determined relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory();

// Set all tuple elements, except the last element, to the same value:
tuple.fill( 2.0, -tuple.length, -1 );

var x = tuple.x;
// returns 2.0

var y = tuple.y;
// returns 0.0
```

<a name="method-filter"></a>

#### tuple.filter( predicate\[, thisArg] )

Creates a new tuple (of the same data type as the host tuple) which includes those elements for which a `predicate` function returns a truthy value.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v >= 0.0 );
}

var p2 = p1.filter( predicate );

var f = p2.fields;
// returns [ 'x', 'y' ]
```

If a `predicate` function does not return a truthy value for any tuple element, the method returns `null`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v >= 10.0 );
}

var p2 = p1.filter( predicate );
// returns null
```

A `predicate` function is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    this.count += 1;
    return ( v >= 0.0 );
}

var ctx = {
    'count': 0
};

var p2 = p1.filter( predicate, ctx );

var n = ctx.count;
// returns 3
```

<a name="method-find"></a>

#### tuple.find( predicate\[, thisArg] )

Returns the first tuple element for which a provided `predicate` function returns a truthy value.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v < 0.0 );
}

var v = tuple.find( predicate );
// returns -1.0
```

If a `predicate` function does not return a truthy value for any tuple element, the method returns `undefined`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v < -10.0 );
}

var v = tuple.find( predicate );
// returns undefined
```

A `predicate` function is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    this.count += 1;
    return ( v < 0.0 );
}

var ctx = {
    'count': 0
};

var v = tuple.find( predicate, ctx );
// returns -1.0

var n = ctx.count;
// returns 3
```

<a name="method-find-field"></a>

#### tuple.findField( predicate\[, thisArg] )

Returns the field of the first tuple element for which a provided `predicate` function returns a truthy value.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v < 0.0 );
}

var field = tuple.findField( predicate );
// returns 'z'
```

If a `predicate` function does not return a truthy value for any tuple element, the method returns `undefined`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v < -10.0 );
}

var field = tuple.findField( predicate );
// returns undefined
```

A `predicate` function is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    this.count += 1;
    return ( v < 0.0 );
}

var ctx = {
    'count': 0
};

var field = tuple.findField( predicate, ctx );
// returns 'z'

var n = ctx.count;
// returns 3
```

<a name="method-find-index"></a>

#### tuple.findIndex( predicate\[, thisArg] )

Returns the index of the first tuple element for which a provided `predicate` function returns a truthy value.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v < 0.0 );
}

var idx = tuple.findIndex( predicate );
// returns 2
```

If a `predicate` function does not return a truthy value for any tuple element, the method returns `-1`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    return ( v < -10.0 );
}

var idx = tuple.findIndex( predicate );
// returns -1
```

A `predicate` function is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

function predicate( v ) {
    this.count += 1;
    return ( v < 0.0 );
}

var ctx = {
    'count': 0
};

var idx = tuple.findIndex( predicate, ctx );
// returns 2

var n = ctx.count;
// returns 3
```

<a name="method-for-each"></a>

#### tuple.forEach( fcn\[, thisArg] )

Invokes a callback for each tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ], 'int32' );

var str = '';

function fcn( v, i, f ) {
    str += f + '=' + v;
    if ( i < tuple.length-1 ) {
        str += ' ';
    }
}

tuple.forEach( fcn );

console.log( str );
// => 'x=1 y=0 z=-1'
```

The callback is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ], 'int32' );

function fcn() {
    this.count += 1;
}

var ctx = {
    'count': 0
};

tuple.forEach( fcn, ctx );

var n = ctx.count;
// returns 3
```

<a name="method-includes"></a>

#### tuple.includes( searchElement\[, fromIndex] )

Returns a `boolean` indicating whether a tuple includes a search element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var bool = tuple.includes( -1.0 );
// returns true

bool = tuple.includes( 2.0 );
// returns false
```

By default, the method searches the entire tuple (`fromIndex = 0`). To begin searching from a specific tuple index, provide a `fromIndex`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var bool = tuple.includes( 1.0, 1 );
// returns false
```

When a `fromIndex` is negative, the starting index is resolved relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var bool = tuple.includes( 1.0, -2 );
// returns false
```

The method does **not** distinguish between signed and unsigned zero.

<a name="method-index-of"></a>

#### tuple.indexOf( searchElement\[, fromIndex] )

Returns the index of the first tuple element strictly equal to a search element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var idx = tuple.indexOf( -1.0 );
// returns 2

idx = tuple.indexOf( 2.0 );
// returns -1
```

By default, the method searches the entire tuple (`fromIndex = 0`). To begin searching from a specific tuple index, provide a `fromIndex`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var idx = tuple.indexOf( 1.0, 1 );
// returns -1
```

When a `fromIndex` is negative, the starting index is resolved relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var idx = tuple.indexOf( 1.0, -2 );
// returns -1
```

The method does **not** distinguish between signed and unsigned zero.

<a name="method-ind2key"></a>

#### tuple.ind2key( ind )

Converts a tuple index to a field name.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var field = tuple.ind2key( 1 );
// returns 'y'

field = tuple.ind2key( 100 );
// returns undefined
```

If provided a negative index, the method resolves the index relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var field = tuple.ind2key( -2 );
// returns 'y'
```

<a name="method-join"></a>

#### tuple.join( \[separator] )

Serializes a tuple by joining all tuple elements as a string.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ], 'int32' );

var str = tuple.join();
// returns '1,0,-1'
```

By default, the method delineates tuple elements using a comma `,`. To specify a custom separator, provide a `separator` string.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ], 'int32' );

var str = tuple.join( '|' );
// returns '1|0|-1'
```

<a name="method-keys"></a>

#### tuple.keys()

Returns an iterator for iterating over tuple keys.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

// Create an iterator:
var it = tuple.keys();

// Iterate over keys...
var v = it.next().value;
// returns [ 0, 'x' ]

v = it.next().value;
// returns [ 1, 'y' ]

var bool = it.next().done;
// returns true
```

<a name="method-key2ind"></a>

#### tuple.key2ind( field )

Converts a field name to a tuple index.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var idx = tuple.key2ind( 'y' );
// returns 1

idx = tuple.key2ind( 'foo' );
// returns -1
```

<a name="method-last-field-of"></a>

#### tuple.lastFieldOf( searchElement\[, fromIndex] )

Returns the field of the last tuple element strictly equal to a search element, iterating from right to left.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 1.0, 0.0, -1.0, 0.0, 1.0 ] );

var field = tuple.lastFieldOf( 0.0 );
// returns 'w'

field = tuple.lastFieldOf( 2.0 );
// returns undefined
```

By default, the method searches the entire tuple (`fromIndex = -1`). To begin searching from a specific tuple index, provide a `fromIndex`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 1.0, 0.0, -1.0, 0.0, 1.0 ] );

var field = tuple.lastFieldOf( 0.0, 2 );
// returns 'y'
```

When a `fromIndex` is negative, the starting index is resolved relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 1.0, 0.0, -1.0, 0.0, 1.0 ] );

var field = tuple.lastFieldOf( 0.0, -3 );
// returns 'y'
```

The method does **not** distinguish between signed and unsigned zero.

<a name="method-last-index-of"></a>

#### tuple.lastIndexOf( searchElement\[, fromIndex] )

Returns the index of the last tuple element strictly equal to a search element, iterating from right to left.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 1.0, 0.0, -1.0, 0.0, 1.0 ] );

var idx = tuple.lastIndexOf( 0.0 );
// returns 3

idx = tuple.lastIndexOf( 2.0 );
// returns -1
```

By default, the method searches the entire tuple (`fromIndex = -1`). To begin searching from a specific tuple index, provide a `fromIndex`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 1.0, 0.0, -1.0, 0.0, 1.0 ] );

var idx = tuple.lastIndexOf( 0.0, 2 );
// returns 1
```

When a `fromIndex` is negative, the starting index is resolved relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z', 'w', 'v' ] );

var tuple = factory( [ 1.0, 0.0, -1.0, 0.0, 1.0 ] );

var idx = tuple.lastIndexOf( 0.0, -3 );
// returns 1
```

The method does **not** distinguish between signed and unsigned zero.

<a name="method-map"></a>

#### tuple.map( fcn\[, thisArg] )

Maps each tuple element to an element in a new tuple having the same data type as the host tuple.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

function fcn( v ) {
    return v * 2.0;
}

var p2 = p1.map( fcn );

var x = p2.x;
// returns 2.0

var y = p2.y;
// returns 0.0

var z = p2.z;
// returns -2.0
```

A callback is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

function fcn( v ) {
    this.count += 1;
    return v * 2.0;
}

var ctx = {
    'count': 0
};

var p2 = p1.map( fcn, ctx );

var n = ctx.count;
// returns 3
```

<a name="method-reduce"></a>

#### tuple.reduce( fcn\[, initialValue] )

Applies a function against an accumulator and each element in a tuple and returns the accumulated result.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 2.0, 0.0, -3.0 ] );

function fcn( acc, v ) {
    return acc + ( v*v );
}

var v = tuple.reduce( fcn );
// returns 11.0
```

If not provided an initial value, the method invokes a provided function with the first tuple element as the first argument and the second tuple element as the second argument.

If provided an initial value, the method invokes a provided function with the initial value as the first argument and the first tuple element as the second argument.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 2.0, 0.0, -3.0 ] );

function fcn( acc, v ) {
    return acc + ( v*v );
}

var v = tuple.reduce( fcn, 0.0 );
// returns 13.0
```

A callback is provided five arguments:

-   `acc`: accumulated result.
-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

<a name="method-reduce-right"></a>

#### tuple.reduceRight( fcn\[, initialValue] )

Applies a function against an accumulator and each element in a tuple and returns the accumulated result, iterating from right to left.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 2.0, 0.0, -3.0 ] );

function fcn( acc, v ) {
    return acc + ( v*v );
}

var v = tuple.reduceRight( fcn );
// returns 1.0
```

If not provided an initial value, the method invokes a provided function with the last tuple element as the first argument and the second-to-last tuple element as the second argument.

If provided an initial value, the method invokes a provided function with the initial value as the first argument and the last tuple element as the second argument.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 2.0, 0.0, -3.0 ] );

function fcn( acc, v ) {
    return acc + ( v*v );
}

var v = tuple.reduceRight( fcn, 0.0 );
// returns 13.0
```

A callback is provided five arguments:

-   `acc`: accumulated result.
-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

<a name="method-reverse"></a>

#### tuple.reverse()

Reverses a tuple **in-place** (thus mutating the tuple on which the method is invoked).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 2.0, 0.0, -3.0 ] );

var x = tuple[ 0 ];
// returns 2.0

x = tuple.x;
// returns 2.0

// Reverse the tuple:
tuple.reverse();

var fields = tuple.orderedFields;
// returns [ 'z', 'y', 'x' ]

var z = tuple[ 0 ];
// returns -3.0

// Tuple field assignments do NOT change:
x = tuple.x;
// returns 2.0
```

Invoking this method does **not** affect tuple field assignments.

<a name="method-set"></a>

#### tuple.set( arr\[, offset] )

Sets tuple elements.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var y = tuple[ 1 ];
// returns 0.0

y = tuple.y;
// returns 0.0

// Set the first two tuple elements:
tuple.set( [ -2.0, 2.0 ] );

var x = tuple[ 0 ];
// returns -2.0

x = tuple.x;
// returns -2.0

y = tuple[ 1 ];
// returns 2.0

y = tuple.y;
// returns 2.0
```

By default, the method starts writing values at the first tuple index. To specify an alternative index, provide an index `offset`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var y = tuple[ 1 ];
// returns 0.0

y = tuple.y;
// returns 0.0

// Set the last two tuple elements:
tuple.set( [ -2.0, 2.0 ], 1 );

var x = tuple[ 0 ];
// returns 1.0

x = tuple.x;
// returns 1.0

y = tuple[ 1 ];
// returns -2.0

y = tuple.y;
// returns -2.0

var z = tuple[ 2 ];
// returns 2.0

z = tuple.z;
// returns 2.0
```

<a name="method-slice"></a>

#### tuple.slice( \[begin\[, end]] )

Copies tuple elements to a new tuple with the same underlying data type as the host tuple.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.slice();

var bool = ( p1 === p2 );
// returns false

bool = ( p1.buffer === p2.buffer );
// returns false

var x = p2.x;
// returns 1.0

var y = p2.y;
// returns 0.0

var z = p2.z;
// returns -1.0
```

By default, the method copies elements beginning with the first tuple element. To specify an alternative tuple index at which to begin copying, provide a `begin` index (inclusive).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.slice( 1 );

var fields = p2.fields;
// returns [ 'y', 'z' ]

var y = p2.y;
// returns 0.0

var z = p2.z;
// returns -1.0
```

By default, the method copies all tuple elements after `begin`. To specify an alternative tuple index at which to end copying, provide an `end` index (exclusive).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.slice( 0, 2 );

var fields = p2.fields;
// returns [ 'x', 'y' ]

var x = p2.x;
// returns 1.0

var y = p2.y;
// returns 0.0
```

When a `begin` and/or `end` index is negative, the respective index is determined relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.slice( -p1.length, -1 );

var fields = p2.fields;
// returns [ 'x', 'y' ]

var x = p2.x;
// returns 1.0

var y = p2.y;
// returns 0.0
```

<a name="method-some"></a>

#### tuple.some( predicate\[, thisArg] )

Tests whether at least one tuple element passes a test implemented by a `predicate` function.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

function predicate( v ) {
    return ( v < 0.0 );
}

var bool = tuple.some( predicate );
// returns true
```

A `predicate` function is provided four arguments:

-   `value`: tuple element.
-   `index`: tuple index.
-   `field`: tuple field name.
-   `tuple`: tuple on which the method is invoked.

To set the callback execution context, provide a `thisArg`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, 1.0 ] );

function predicate( v ) {
    this.count += 1;
    return ( v < 0.0 );
}

var ctx = {
    'count': 0
};

var bool = tuple.some( predicate, ctx );
// returns false

var n = ctx.count;
// returns 2
```

<a name="method-sort"></a>

#### tuple.sort( \[compareFunction] )

Sorts a tuple **in-place** (thus mutating the tuple on which the method is invoked).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 2.0, -3.0, 0.0 ] );

var x = tuple[ 0 ];
// returns 2.0

x = tuple.x;
// returns 2.0

// Sort the tuple (in ascending order):
tuple.sort();

var fields = tuple.orderedFields;
// returns [ 'y', 'z', 'x' ]

var y = tuple[ 0 ];
// returns -3.0

// Tuple field assignments do NOT change:
x = tuple.x;
// returns 0.0
```

By default, the method sorts tuple elements in ascending order. To impose a custom order, provide a `compareFunction`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 2.0, -3.0, 0.0 ] );

var x = tuple[ 0 ];
// returns 2.0

x = tuple.x;
// returns 2.0

function descending( a, b ) {
    return b - a;
}

// Sort the tuple (in descending order):
tuple.sort( descending );

var fields = tuple.orderedFields;
// returns [ 'x', 'z', 'y' ]

var z = tuple[ 1 ];
// returns 0.0

// Tuple field assignments do NOT change:
var y = tuple.y;
// returns -3.0
```

The comparison function is provided two tuple elements, `a` and `b`, per invocation, and its return value determines the sort order as follows:

-   If the comparison function returns a value **less** than zero, then the method sorts `a` to an index lower than `b` (i.e., `a` should come **before** `b`).
-   If the comparison function returns a value **greater** than zero, then the method sorts `a` to an index higher than `b` (i.e., `b` should come **before** `a`).
-   If the comparison function returns **zero**, then the relative order of `a` and `b` _should_ remain unchanged.

Invoking this method does **not** affect tuple field assignments.

<a name="method-subarray"></a>

#### tuple.subarray( \[begin\[, end]] )

Creates a new [typed array][@stdlib/array/typed] over the same underlying [`ArrayBuffer`][@stdlib/array/buffer] and with the same underlying data type as the host tuple.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var arr = tuple.subarray();
// returns <Float64Array>[ 1.0, 0.0, -1.0 ]
```

By default, the method creates a [typed array][@stdlib/array/typed] view beginning with the first tuple element. To specify an alternative tuple index at which to begin, provide a `begin` index (inclusive).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var arr = tuple.subarray( 1 );
// returns <Float64Array>[ 0.0, -1.0 ]
```

By default, the method creates a [typed array][@stdlib/array/typed] view which includes all tuple elements after `begin`. To limit the number of tuple elements after `begin`, provide an `end` index (exclusive).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var arr = tuple.subarray( 0, 2 );
// returns <Float64Array>[ 1.0, 0.0 ]
```

When a `begin` and/or `end` index is negative, the respective index is determined relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var arr = tuple.subarray( -tuple.length, -1 );
// returns <Float64Array>[ 1.0, 0.0 ]
```

If the method is unable to resolve indices to a non-empty tuple subsequence, the method returns an empty [typed array][@stdlib/array/typed].

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var arr = tuple.subarray( 10, -1 );
// returns <Float64Array>[]
```

<a name="method-subtuple"></a>

#### tuple.subtuple( \[begin\[, end]] )

Creates a new named typed tuple over the same underlying [`ArrayBuffer`][@stdlib/array/buffer] and with the same underlying data type as the host tuple.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.subtuple();

var bool = ( p1 === p2 );
// returns false

bool = ( p1.buffer === p2.buffer );
// returns true

var len = p2.length;
// returns 3

var x = p2.x;
// returns 1.0

var y = p2.y;
// returns 0.0

var z = p2.z;
// returns -1.0
```

By default, the method creates a new tuple beginning with the first tuple element. To specify an alternative tuple index at which to begin, provide a `begin` index (inclusive).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.subtuple( 1 );

var len = p2.length;
// returns 2

var fields = p2.fields;
// returns [ 'y', 'z' ]

var y = p2.y;
// returns 0.0

var z = p2.z;
// returns -1.0
```

By default, the method creates a new tuple which includes all tuple elements after `begin`. To limit the number of tuple elements after `begin`, provide an `end` index (exclusive).

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.subtuple( 0, 2 );

var len = p2.length;
// returns 2

var fields = p2.fields;
// returns [ 'x', 'y' ]

var x = p2.x;
// returns 1.0

var y = p2.y;
// returns 0.0
```

When a `begin` and/or `end` index is negative, the respective index is determined relative to the last tuple element.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.subtuple( -p1.length, -1 );

var len = p2.length;
// returns 2

var fields = p2.fields;
// returns [ 'x', 'y' ]

var x = p2.x;
// returns 1.0

var y = p2.y;
// returns 0.0
```

If the method is unable to resolve indices to a non-empty tuple subsequence, the method returns `null`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var p1 = factory( [ 1.0, 0.0, -1.0 ] );

var p2 = p1.subtuple( 10, -1 );
// returns null
```

<a name="method-to-json"></a>

#### tuple.toJSON()

Serializes a tuple as [JSON][json].

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ] );

var obj = tuple.toJSON();
// returns { 'x': 1.0, 'y': 0.0, 'z': -1.0 }
```

<a name="method-to-locale-string"></a>

#### tuple.toLocaleString( \[locales\[, options]] )

Serializes a tuple as a locale-specific `string`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ], 'int32' );

var str = tuple.toLocaleString();
// returns '1,0,-1'
```

<a name="method-to-string"></a>

#### tuple.toString()

Serializes a tuple as a `string`.

```javascript
var factory = namedtypedtuple( [ 'x', 'y', 'z' ] );

var tuple = factory( [ 1.0, 0.0, -1.0 ], 'int32' );

var str = tuple.toString();
// returns 'tuple(x=1, y=0, z=-1)'
```

The returned `string` uses the tuple `name` as specified when creating a tuple factory.

```javascript
var opts = {
    'name': 'Point'
};

var factory = namedtypedtuple( [ 'x', 'y', 'z' ], opts );

var tuple = factory( [ 1.0, 0.0, -1.0 ], 'int32' );

var str = tuple.toString();
// returns 'Point(x=1, y=0, z=-1)'
```

<a name="method-values"></a>

#### tuple.values()

Returns an iterator for iterating over tuple elements.

```javascript
var factory = namedtypedtuple( [ 'x', 'y' ] );

var tuple = factory( [ 1.0, -1.0 ] );

// Create an iterator:
var it = tuple.values();

// Iterate over tuple elements...
var v = it.next().value;
// returns 1.0

v = it.next().value;
// returns -1.0

var bool = it.next().done;
// returns true
```

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

* * *

## Notes

-   Named typed tuples are **not** immutable. In order to create immutable named typed tuples, invoke `Object.freeze()` on returned tuples.

    <!-- TODO: use stdlib `Object.freeze` package -->

    ```javascript
    var factory = namedtypedtuple( [ 'x', 'y' ] );

    var tuple = factory( [ 1.0, -1.0 ] );

    // Make the tuple immutable:
    tuple = Object.freeze( tuple );
    ```

-   Tuple fields are **non-enumerable**. To return the list of tuple fields, use [`tuple.fields`](#prop-fields).

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

* * *

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var namedtypedtuple = require( '@stdlib/dstructs-named-typed-tuple' );

var fields = [ 'x', 'y' ];
var opts = {
    'name': 'Point'
};

var Point = namedtypedtuple( fields, opts );

var p = new Point( [ 1.0, -1.0 ] );

// Tuple elements can be accessed by index or name:
var x = p[ 0 ];
// returns 1.0

x = p.x;
// returns 1.0

var y = p[ 1 ];
// returns -1.0

y = p.y;
// returns -1.0

// Sort tuple elements while retaining name access:
p.sort();
console.log( 'p[0]=%d, p[1]=%d, x=%d, y=%d', p[ 0 ], p[ 1 ], p.x, p.y );

// Retrieve the tuple fields in index order:
console.log( p.orderedFields );
// => [ 'y', 'x' ]

// Serialize the tuple as a string:
console.log( p.toString() );

// Serialize the tuple a JSON string:
console.log( JSON.stringify( p ) );
```

</section>

<!-- /.examples -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

* * *

## See Also

-   <span class="package-name">[`@stdlib/array-typed`][@stdlib/array/typed]</span><span class="delimiter">: </span><span class="description">create a typed array.</span>

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2025. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/dstructs-named-typed-tuple.svg
[npm-url]: https://npmjs.org/package/@stdlib/dstructs-named-typed-tuple

[test-image]: https://github.com/stdlib-js/dstructs-named-typed-tuple/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/dstructs-named-typed-tuple/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/dstructs-named-typed-tuple/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/dstructs-named-typed-tuple?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/dstructs-named-typed-tuple.svg
[dependencies-url]: https://david-dm.org/stdlib-js/dstructs-named-typed-tuple/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/dstructs-named-typed-tuple/tree/deno
[deno-readme]: https://github.com/stdlib-js/dstructs-named-typed-tuple/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/dstructs-named-typed-tuple/tree/umd
[umd-readme]: https://github.com/stdlib-js/dstructs-named-typed-tuple/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/dstructs-named-typed-tuple/tree/esm
[esm-readme]: https://github.com/stdlib-js/dstructs-named-typed-tuple/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/dstructs-named-typed-tuple/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/dstructs-named-typed-tuple/main/LICENSE

[@stdlib/array/buffer]: https://github.com/stdlib-js/array-buffer

[json]: http://www.json.org/

<!-- <related-links> -->

[@stdlib/array/typed]: https://github.com/stdlib-js/array-typed

<!-- </related-links> -->

</section>

<!-- /.links -->
