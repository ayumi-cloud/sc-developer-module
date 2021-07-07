## Summer CMS Developer Escaping API

### Escaping

[HTML Purifier](http://htmlpurifier.org/) is an HTML filtering solution that uses a unique combination of robust whitelists and agressive parsing to ensure that not only are XSS attacks thwarted, but the resulting HTML is standards compliant.

In depth information about configuration parameters can be found here: http://htmlpurifier.org/live/configdoc/plain.html

[DOMPurify](https://cure53.de/purify) sanitizes HTML and prevents XSS attacks. You can feed DOMPurify with string full of dirty HTML and it will return a string (unless configured otherwise) with clean HTML. DOMPurify will strip out everything that contains dangerous HTML and thereby prevent XSS attacks and other nastiness. It's also damn bloody fast. We use the technologies the browser provides and turn them into an XSS filter. The faster your browser, the faster DOMPurify will be.

[JSON5](https://github.com/json5/json5) - a superset of `JSON` which allows comments, trailing commas, single-quoted strings and more. Including a parser to allow encoding and decoding JSON-Object strings into JSON objects and vice versa.

[Laravel (Validation)](https://laravel.com/docs/master/validation) - includes a wide variety of convenient validation rules that you may apply to data, even providing the ability to validate if values are unique in a given database table.

[Symfony (Validation)](https://symfony.com/doc/current/validation.html) - provides a Validator component to handle this for you. This component is based on the JSR303 Bean Validation specification.

[OpenType Sanitizer](https://github.com/khaledhosny/ots) parses and serializes OpenType files (OTF, TTF) and WOFF and WOFF2 font files, validating them and sanitizing them as it goes.

=== TO DO ===

### API's

Summer CMS also uses the following api's to sanitize data, along with it's own custom components:

- [HTML Sanitizer API](https://wicg.github.io/sanitizer-api/)
- [Trusted Types API](https://w3c.github.io/webappsec-trusted-types/dist/spec/)

### Recommendations

Below shows which libraries are being used to clean each coding language:

Programming language | Third party library
---|---
Audio | x
CSS | x
Fonts | OpenType Sanitizer
HTML | HTML Purifier
Images | x
Javascript | DOMPurify
JSON | JSON5
Laravel | HTML Purifier
MathML | DOMPurify
PDF | x
PHP | HTML Purifier
SVG | DOMPurify
Twig | HTML Purifier
Video | x
YAML | x

=== TO DO ===

## Laravel

Below are some basic examples how to use the HTMLPurifier Service Provider with [Laravel](https://laravel.com/) web application framework:

### Example 1 (long code version)

```php
$purifier = $this->app->make('purifier');
$html = '<b>Simple and short';
echo $purifier->clean($html);
```

Result:

```php
// Added the `</b>` tag.
<b>Simple and short</b>
```

### Example 2 (short code version)

```php
$html = '<b>Simple and short';
echo Purifier::clean($html);
```

Result:

```php
// Added the `</b>` tag.
<b>Simple and short</b>
```

### Example 3 (adding custom config)

```php
$html = '<a href="#" target="_blank">test link</a>';
echo Purifier::clean($html, ['HTML.Allowed' => 'a[href|target]']);
```

Result:

```php
// The config settings allowed the `target="_blank"` attribute to be displayed in the result.
<a href="#" target="_blank">test link</a>
``` 

## Twig

Below are some basic examples how to use the HTMLPurifier Service Provider with [Twig](https://twig.symfony.com/) template engine:

### Example 1 (basic code version)

```twig
{% set html = '<script>alert(\'XSS\');</script>123' %}

{{ purify(html) }}
```

Result:

```php
// Removed injected javascript code and added the `<p></p>` tags.
<p>123</p>
```

### Example 2 (adding custom config)

```twig
{% set html = '<a href="#" target="_blank">test link</a>' %}

{% set config = '[\'HTML.Allowed\' => \'a[href|target]\']' %}

{{ purify(html, config) }}
```

Result:

```php
// The config settings allowed the `target="_blank"` attribute to be displayed in the result.
<a href="#" target="_blank">test link</a>
``` 

## Javascript

Below are some basic examples how to use the DOMPurify with [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) and [JavaScript modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules):

### Example 1 (basic code version)

```html
<script type="text/javascript" src="link to the purify.min.js"></script>
```

Afterwards you can sanitize strings by executing the following code:

```js
var dirty = '<option><style></option></select><b><img src=xx: onerror=alert(1)></style></option>';
console.log( DOMPurify.sanitize( dirty ) );
```

The resulting HTML can be written into a DOM element using `innerHTML` or the DOM using `document.write()`.

Result:

```php
// Remove the injected code and bad element tags.
<option></option>
```

### Example 2 (html only code version)

If you only need HTML, which might be a very common use-case, you can easily set that up with the following example:

```js
var dirty = '<option><style></option></select><b><img src=xx: onerror=alert(1)></style></option>';
console.log( DOMPurify.sanitize( dirty , {USE_PROFILES: {html: true}} ) );
```

Result:

```php
// Remove the injected code and bad element tags.
<option></option>
```

### Example 3 (config code version)

```js
var dirty = '<a href="#">abc<b style="color:red">123</b><q class="cite">123</b></a>';
console.log(
    DOMPurify.sanitize(dirty, {
        ALLOWED_TAGS: ["b", "q"],
        ALLOWED_ATTR: ["style"],
        KEEP_CONTENT: true,
    })
);
```  
        
Result:

```php
// Outputs the allowed tags and removes ones not listed.
abc<b style="color:red">123</b><q>123</q>
```        
        
### Example 4 (amd loader version)

If you're using an [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) module loader like [Require.js](http://requirejs.org/), you can load this script asynchronously as well:

```js
import DOMPurify from 'dompurify';

console.log( DOMPurify.sanitize(dirty) );
```

## JSON

The JSON5 Data Interchange Format (JSON5) is a superset of [JSON](https://tools.ietf.org/html/rfc7159) that aims to alleviate some of the limitations of JSON by expanding its syntax to include some productions from [ECMAScript 5.1](https://www.ecma-international.org/ecma-262/5.1/).

### `JSON5.parse()`

Parses a JSON5 string, constructing the JavaScript value or object described by the string. An optional reviver function can be provided to perform a transformation on the resulting object before it is returned.

#### Syntax

```js
JSON5.parse(text[, reviver])
```

#### Parameters

- `text`: The string to parse as JSON5.
- `reviver`: If a function, this prescribes how the value originally produced by   parsing is transformed, before being returned.

#### Return value

The object corresponding to the given JSON5 text.

### `JSON5.stringify()`

Converts a JavaScript value to a JSON5 string, optionally replacing values if a replacer function is specified, or optionally including only the specified properties if a replacer array is specified.

#### Syntax

```js
JSON5.stringify(value[, replacer[, space]])
JSON5.stringify(value[, options])
```

#### Parameters

- `value`: The value to convert to a JSON5 string.
- `replacer`: A function that alters the behavior of the stringification process, or an array of String and Number objects that serve as a whitelist for selecting/filtering the properties of the value object to be included in the JSON5 string. If this value is null or not provided, all properties of the object are included in the resulting JSON5 string.
- `space`: A String or Number object that's used to insert white space into the output JSON5 string for readability purposes. If this is a Number, it indicates the number of space characters to use as white space; this number is capped at 10 (if it is greater, the value is just 10). Values less than 1 indicate that no space should be used. If this is a String, the string (or the first 10 characters of the string, if it's longer than that) is used as white space. If this parameter is not provided (or is null), no white space is used. If white space is used, trailing commas will be used in objects and arrays.
- `options`: An object with the following properties:
  - `replacer`: Same as the `replacer` parameter.
  - `space`: Same as the `space` parameter.
  - `quote`: A String representing the quote character to use when serializing strings.

#### Return value

A JSON5 string representing the value.

### Node.js `require()` JSON5 files

When using Node.js, you can `require()` JSON5 files by adding the following statement.

```js
require('json5/lib/register')
```

Then you can load a JSON5 file with a Node.js `require()` statement. For example:

```js
const config = require('./config.json5')
```

### Example 1 (basic javascript code version)

```js
const JSON5 = require('json5');
console.log(json5.parse("{ hello: 'world' }"));
```

or

```js
<script src="link to the json5 index.min.js"></script>
console.log(json5.parse("{ hello: 'world' }"));
```

Result:

```js
{ hello: 'world' }
```



=== TO DO ===
