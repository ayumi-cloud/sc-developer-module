## Summer CMS Developer Encoding API

### Encoding

This api is for converting and cleaning`Latin1` (`ISO 8859-1`), `Windows-1252` or `UTF8`.

If you apply the PHP function `utf8_encode()` to an already-UTF8 string it will return a garbled UTF8 string, this api addresses that issue.

Sometimes you have to deal with services that are unreliable in terms of encoding, possibly mixing UTF8 and Latin1 in the same string. You don't need to know what the encoding of the string. It can be `Latin1` (`ISO 8859-1`), `Windows-1252` or `UTF8`, or the string can have a mixture of them. 

#### Credit

This api is a **modified version** of the work done by [forceutf8](https://github.com/neitanod/forceutf8) and uses v2.0.4.

#### Examples

```php
$utf8_string = Encoding::fixUTF8($garbled_utf8_string);
$utf8_string = Encoding::toUTF8($utf8_or_latin1_or_mixed_string);
$latin1_string = Encoding::toLatin1($utf8_or_latin1_or_mixed_string);
```

By default, `Encoding::fixUTF8` will use the `Encoding::WITHOUT_ICONV` flag, signalling that iconv should not be used to fix garbled UTF8 strings.

This api also provides options for iconv processing, such as `Encoding::ICONV_TRANSLIT` and `Encoding::ICONV_IGNORE` to enable these flags when the iconv class is utilized. The functionality of such flags are documented in the [PHP iconv documentation](http://php.net/manual/en/function.iconv.php).

```php
Encoding::fixUTF8($str); // Will break U+2014
Encoding::fixUTF8($str, Encoding::ICONV_IGNORE); // Will preserve U+2014
Encoding::fixUTF8($str, Encoding::ICONV_TRANSLIT); // Will preserve U+2014
```

Value | Return | Description
---|---|---
fixUTF8 | string | Will fix the double (or multiple) encoded UTF8 string that look garbled.
toLatin1 | string | Leaves Latin1 characters alone, while converting almost all non-Latin1 to Latin1.
toUTF8 | string | Leaves UTF8 characters alone, while converting almost all non-UTF8 to UTF8.

(*) Subject to adding more api properties from the creation of new developer features.
