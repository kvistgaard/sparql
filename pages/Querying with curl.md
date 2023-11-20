- [curl](https://curl.se) is a command line tool and a library for transferring data using various network protocols.
- curl can be used to communicate with SPARQL endpoints
- [[Example]]
  collapsed:: true
	- ```shell
	  curl -X POST "https://dbpedia.org/sparql" --data-urlencode "query=SELECT ?artist WHERE { ?artist a dbo:Artist } LIMIT 5"
	  ```
- Popular options
	- `-L` Tells curl to follow any redirects.
	- `-H` Header. Sets the "Accept" header in the HTTP
	  request.
	- `-o`  Specifies the output file name.
	- `-X`  Specifies the HTTP method POST, PUT (not
	  needed for GET)