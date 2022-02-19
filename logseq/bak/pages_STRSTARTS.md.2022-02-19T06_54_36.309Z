type:: [[Function/On strings]]

- [[Example]]
	- Find all [[SKOS]] properties in use
		- ```sparql
		  SELECT DISTINCT ?property
		  WHERE {
		      ?s ?property ?o .
		      FILTER (STRSTARTS(STR(?property), "http://www.w3.org/2004/02/skos/core#" ))
		  }
		  
		  ```
		  #Query