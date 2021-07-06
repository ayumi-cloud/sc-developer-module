## Summer CMS Developer Encoding API

### Encoding

This api is for converting and cleaning`Latin1` (`ISO 8859-1`), `Windows-1252` or `UTF8`.

If you apply the PHP function `utf8_encode()` to an already-UTF8 string it will return a garbled UTF8 string, this api addresses that issue.

Sometimes you have to deal with services that are unreliable in terms of encoding, possibly mixing UTF8 and Latin1 in the same string. You don't need to know what the encoding of the string. It can be `Latin1` (`ISO 8859-1`), `Windows-1252` or `UTF8`, or the string can have a mixture of them. 

#### Credit

This api is a **modified version** of the work done by [forceutf8](https://github.com/neitanod/forceutf8) and uses v2.0.4.

#### Examples

xxx

Value | Return | Description
---|---|---
fixUTF8 | string | L
toISO8859 | string | L
toLatin1 | string | L
toUTF8 | string | Leaves UTF8 characters alone, while converting almost all non-UTF8 to UTF8.
toWin1252 | string | L





(*) Subject to adding more api properties from the creation of new developer features.
