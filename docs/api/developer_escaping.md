## Summer CMS Developer Escaping API

### Escaping

[HTML Purifier](http://htmlpurifier.org/) is an HTML filtering solution that uses a unique combination of robust whitelists and agressive parsing to ensure that not only are XSS attacks thwarted, but the resulting HTML is standards compliant.

In depth information about configuration parameters can be found here: http://htmlpurifier.org/live/configdoc/plain.html

[DOMPurify](https://cure53.de/purify) sanitizes HTML and prevents XSS attacks. You can feed DOMPurify with string full of dirty HTML and it will return a string (unless configured otherwise) with clean HTML. DOMPurify will strip out everything that contains dangerous HTML and thereby prevent XSS attacks and other nastiness. It's also damn bloody fast. We use the technologies the browser provides and turn them into an XSS filter. The faster your browser, the faster DOMPurify will be.

JSON5 === TO DO ===

## Laravel

Below are some basic examples how to use the HTMLPurifier Service Provider with [Laravel](https://laravel.com/) web application framework:

### Example 1 (long code version)

```php
$purifier = $this->app->make('purifier');
$html = '<b>Simple and short';
echo $purifier->clean($html);
```

Result:

```html
<b>Simple and short</b> // Added the `</b>` tag.
```

### Example 2 (short code version)

```php
$html = '<b>Simple and short';
echo Purifier::clean($html);
```

Result:

```html
<b>Simple and short</b> // Added the `</b>` tag.
```

### Example 3 (adding custom config)

```php
$html = '<a href="#" target="_blank">test link</a>';
echo Purifier::clean($html, ['HTML.Allowed' => 'a[href|target]']);
```

Result:

```html
<a href="#" target="_blank">test link</a> // The config settings allowed the `target="_blank"` attribute to be displayed in the result.
``` 

## Twig

Below are some basic examples how to use the HTMLPurifier Service Provider with [Twig](https://twig.symfony.com/) template engine:

### Example 1 (basic code version)

```twig
{% set html = '<script>alert(\'XSS\');</script>123' %}

{{ purify(html) }}
```

Result:

```html
<p>123</p> // Removed injected javascript code and added the `<p></p>` tags.
```

### Example 2 (adding custom config)

```twig
{% set html = '<a href="#" target="_blank">test link</a>' %}

{% set config = '[\'HTML.Allowed\' => \'a[href|target]\']' %}

{{ purify(html, config) }}
```

Result:

```html
<a href="#" target="_blank">test link</a> // The config settings allowed the `target="_blank"` attribute to be displayed in the result.
``` 

## Javascript

xxx


## JSON

xxx



#### Examples




Value | Return | Description
---|---|---
fixUTF8 | string | Will fix the double (or multiple) encoded UTF8 string that look garbled.
toLatin1 | string | Leaves Latin1 characters alone, while converting almost all non-Latin1 to Latin1.
toUTF8 | string | Leaves UTF8 characters alone, while converting almost all non-UTF8 to UTF8.

(*) Subject to adding more api properties from the creation of new developer features.
