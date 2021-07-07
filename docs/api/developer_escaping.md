## Summer CMS Developer Escaping API

### Escaping

xxxxxxx

#### Credit

This api is a **modified version** of the following vendor packages:

- x
- x

## Laravel

xxx

## Twig

xxx

## Javascript

xxx





#### Examples

```php
$html = '<a href="#" target="_blank">test link</a>';
echo Purifier::clean($html, ['HTML.Allowed' => 'a[href|target]']);
```

Outputs:

```html
<a href="#" target="_blank">test link</a>
```

- [x] Custom config - Twig side.

```twig
{% set html = '<a href="#" target="_blank">test link</a>' %}

{% set config = '[\'HTML.Allowed\' => \'a[href|target]\']' %}

{{ purify(html, config) }}

{% set html = '<script>alert(\'XSS\');</script>123' %}

{{ purify(html) }}
```

Outputs:

```html
<a href="#" target="_blank">test link</a>
<p>123</p>
```

Value | Return | Description
---|---|---
fixUTF8 | string | Will fix the double (or multiple) encoded UTF8 string that look garbled.
toLatin1 | string | Leaves Latin1 characters alone, while converting almost all non-Latin1 to Latin1.
toUTF8 | string | Leaves UTF8 characters alone, while converting almost all non-UTF8 to UTF8.

(*) Subject to adding more api properties from the creation of new developer features.
