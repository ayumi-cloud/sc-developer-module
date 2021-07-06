## Summer CMS Developer Encoding API

### Encoding

This api is for converting and cleaning Latin1 (ISO 8859-1), Windows-1252 and UTF8.

If you apply the PHP function `utf8_encode()` to an already-UTF8 string it will return a garbled UTF8 string, this api addresses that issue.

Sometimes you have to deal with services that are unreliable in terms of encoding, possibly mixing UTF8 and Latin1 in the same string. You don't need to know what the encoding of the string. It can be `Latin1` (`ISO 8859-1`), `Windows-1252` or `UTF8`, or the string can have a mixture of them. 

#### Credit

This api is a **modified version** of the work done by [forceutf8](https://github.com/neitanod/forceutf8) and uses v2.0.4.

#### Examples

xxx

Value | Return | Description
---|---|---
aggressiveClean | string | Aggressive cleaning - all tags and stuff inside will be removed.
checkUtf8Encoding | boolean | Check for invalid UTF8 encoding and invalid byte.
compactAnyExplodedWords | string | Compact any exploded words.
contains | boolean | Determine if a given string contains a given sub-string.
convertAllTabsToSpaces | string | Convert all tabs to spaces.
convertCharacterEntitiesToASCII | string | Convert character entities to ascii.
deleteLeading | string | Delete leading characters.
deleteTrailing | string | Delete trailing characters.
endsWith | boolean | Determine if a given string ends with a given value.
ensureLeading | string | Ensure that a string is starts with a special string.
ensureTrailing | string | Ensure that a string is ends with a special string.
fullStringClean | string | Clean strings against XSS attacks.
healNaughtyHTMLElements | string | Heal naughty html elements.
healNaughtyScriptingElements | string | Heal naughty scripting elements.
is | boolean | Determine if a given string matches a given pattern.
isEvilPath | boolean | Check if contains evil path.
isSerialized | boolean | Check value to find if it was serialized.
isString | boolean | Check for a valid string.
makesPhpTagsSafe | string | Make php tags safe.
pregQuote | string | Wrapper for `preg_quote` supporting strings and array of strings.
randomString | string | Random string for PHP7 or greater.
removeDisallowedJavaScriptInLinksOrImgTags | string | Remove disallowed javascript in links or img tags.
removeJavaScriptEventHandlers | string | Remove javascript event handlers.
removeJavaScriptHardRedirects | string | Remove javascript hard redirects.
removeNullCharacters | string | Remove null characters.
startsWith | boolean | Determine if a given string begins with a given value.
strangeThingsAreSubmitted | string | Clean strange things that submitted.
strposa | boolean | Checks an array for a match.
validateStandardCharacterEntities | string | Validate standard character entities.
validateUTF16TwoByteEncoding | string | Validate utf-16 two byte encoding.

(*) Subject to adding more api properties from the creation of new developer features.
