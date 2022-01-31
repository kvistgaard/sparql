type:: [[Function/On strings]]
The ENCODE_FOR_URI function corresponds to the XPath fn:encode-for-uri function. It returns a simple literal with the lexical form obtained from the lexical form of its input after translating reserved characters according to the fn:encode-for-uri function. See [spec](https://www.w3.org/TR/sparql11-query/#func-encode). #URI
title:: ENCODE_FOR_URI

- One popular application is for generating URIs from strings.
- `ENCODE_FOR_URI(string literal)`
-