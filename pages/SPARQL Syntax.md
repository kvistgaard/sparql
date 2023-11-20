- [[SPARQL]] uses a variant of [[Turtle]][¹](((61ef8d42-f778-4f31-95f3-1b76bd13f743))).
- ## Basic [syntax]([[Syntax]])
  collapsed:: true
	- | **Symbol** | **Meaning**                                      | **Example**                                           |
	  | PREFIX     | Declares prefix shortcuts                        | **PREFIX** dbr: \<http://dbpedia.org/resource/> |      
	  | SELECT     | Query result clause                              | **SELECT** ?country ?capital                          |
	  | ?x         | Variable x                                       | SELECT **?country ?capital**                          |
	  | {}         | Set of query patterns                            | **{**?country dbo:capital ?capital .**}**             |
	  | .          | End of triple pattern                            | ?country dbo:capital ?capital **.**                   |
	  | ;          | Next triple pattern has the same subject         | ?country a dbo:Country**;**                           |
	  |            |                                                  |                                                       |
	  |            |                                                  | dbo:capital ?capital .                                |
	  | FILTER     | Condition for a variable                         | **FILTER** ( LANG(?capital) = \"en\" )                |
	  | LANG()     | Returns the language tag of a literal.           | FILTER ( **LANG(**?capital**)** = \"en\" )            |
	  | \#         | Comment. This line is ignored by SPARQL engines. | **\#**All countries with their population and capital |
	  |ORDER BY   | Sort the results by                              | **ORDER BY** ?population                              |
	  | DESC()     | Sort in descending order                         | ORDER BY **DESC(**?population**)**      |              
	  | LIMIT      | Limits the number of results                     | **LIMIT** 20                                          |
- ## Variables
  collapsed:: true
	- A query variable is marked by the use of either "?" or "$".
	- The"?" or "$" is not part of the variable name.
	- In a query, $x and ?x identify the same variable.
	- All queries in this wiki use only "?".
	- Allowed characters are [a-z], [A-Z], [0-9], _, · and diacritics. Hyphens are not allowed.
	- When using several words, it is recommended to put them either in CamelCase (example: NumberOfItems) or use underscore (Number_Of_Items).
- ## Brackets
  collapsed:: true
	- Curly **{ }** (aka “braces”)
		- Query conditions: triple patterns, filters, bindings, etc
		  `{?x a foaf:Person}`
	- Round **( )** (aka “parentheses”)
		- Mostly for function arguments
		  `FILTER ( LANG(?capital) = "en" )`
	- Angled  **<>**
		- Full URIs in triple patterns or prefix declarations
		  `PREFIX dcat: <http://www.w3.org/ns/dcat#>`
	- Sqaure  **[ ]**
		- A blank node or a set of triples with blank node as a subject
- ---
- [[Note]]s
  collapsed:: true
	- [1] [[Turtle]] compared to SPARQL [(see in the SPARQL spec)](https://www.w3.org/TR/2014/REC-turtle-20140225/#sec-diff-sparql)
	  id:: 61ef8d42-f778-4f31-95f3-1b76bd13f743
		- The SPARQL 1.1 Query LanguageF (SPARQL) uses a Turtle style syntax for its TriplesBlock production. This production differs from the Turtle language in that:
			- SPARQL permits RDF Literals as the subject of RDF triples.
			- SPARQL permits variables (`?name` or `$name`) in any part of the triple of the form.
			- Turtle allows prefix and base declarations anywhere outside of a triple. In SPARQL, they are only allowed in the Prologue (at the start of the SPARQL query).
			- SPARQL uses case insensitive keywords, except for 'a'. Turtle's @prefix and @base declarations are case sensitive, the SPARQL dervied PREFIX and BASE are case insensitive.
			- 'true' and 'false' are case insensitive in SPARQL and case sensitive in Turtle. TrUe is not a valid boolean value in Turtle.