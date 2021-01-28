## Summer CMS Developer Validating and Sanitizing Data API

### Validating and Sanitizing

Sanitizing and validating user input is one of the most common tasks in a web application. To make this task easier Summer CMS provides a native filter module that you can use to sanitize or validate data.

Common use cases for the module include cleaning the user input data for the frontend and backend forms, cleaning the data being read and written to the config files, cleaning the data being sent and recieved from the database, cookies, local and session storage, trust tokens etc.

The module also converts formats such as encoding and enconding. For example, an associative array into a JSON object.

For larger more complex sanitization and validation methods third-party libraries have been used as they pffer the highest level of complete protection, below mentions a few third-party libraries being used:

 - [HTML Purifier](http://htmlpurifier.org/) - a `HTML` filter that guards against XSS and ensures standards-compliant output.
 - [DOMPurify](https://github.com/cure53/DOMPurify) - a DOM-only, super-fast, uber-tolerant XSS sanitizer for `HTML`, `MathML` and `SVG`.
 - [JSON5](https://github.com/json5/json5) - a superset of `JSON` which allows comments, trailing commas, single-quoted strings and more. Including a parser to allow encoding and decoding JSON-Object strings into JSON objects and vice versa.
- [Laravel (Validation)](https://laravel.com/docs/master/validation) - laravel includes a wide variety of convenient validation rules that you may apply to data, even providing the ability to validate if values are unique in a given database table.

=== TO DO ===

- `JS` - 

- `YAML`
- `XML`
- `Twig`
- `CSS`

Below shows which library is being used to clean each coding language:

x

Invalid sanitization and validation methods are sent to the error module for the developer to view the stack trace. Also the data is sent to the analytics section for full chart analysis.

### API's

- [HTML Sanitizer API](https://wicg.github.io/sanitizer-api/)
- [Trusted Types API](https://w3c.github.io/webappsec-trusted-types/dist/spec/)

Some libraries already generate Trusted Types that you can pass to the sink functions. For example, DOMPurify supports Trusted Types and will return sanitized HTML wrapped in a `TrustedHTML` object such that the browser does not generate a violation.

### Validating and Sanitizing API

x

(*) Subject to adding more features as time goes on.
