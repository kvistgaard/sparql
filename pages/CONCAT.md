type:: [[Function/On strings]]

- [[Example]]
	- ```sparql
	  PREFIX cdm: <http://publications.europa.eu/ontology/cdm#>
	  
	  
	  SELECT ?reg (IRI(CONCAT(STR(?eli),"/eng/pdf")) AS ?pdf_URL)
	  
	  {
	    ?reg cdm:resource_legal_eli ?eli .
	  }
	  
	  LIMIT 1000
	  ``` 
	  #Cellar #IRI #Query