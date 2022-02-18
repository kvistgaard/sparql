type:: Negation

- [[Example]]
	- ```sparql
	  SELECT ?concept ?prefLabelURI ?prefLabel 
	  
	  WHERE {
	      ?concept a skos:Concept;
	      skosxl:prefLabel ?prefLabelURI .
	  ?prefLabelURI skosxl:literalForm ?prefLabel .
	      
	  FILTER (LANG(?prefLabel) = "en")
	  FILTER NOT EXISTS {?concept skosxl:altLabel ?altLabelURI}
	  } 
	  
	  ```
	  #Query #FILTER #LANG #SKOS-XL