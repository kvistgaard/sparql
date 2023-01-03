type:: [[Function/On strings]]

- For Regular Expression (REGEX) [[Syntax]], see
	- [xpath/regex specification](https://www.w3.org/TR/xpath-functions/#regex-syntax)
	- https://regexone.com/ #Tutorial
- Some frequent patterns
	- starts with "cat", case insensitive
		- `REGEX (?s, "^cat", "i")`
	- ends with "cat", case insensitive
		- `REGEX (?s, "cat$", "i")`
	- contains a number
		- `REGEX (?s, "[0-9]")`