- Classes
	- ```sparql
	  SELECT DISTINCT ?class 
	  WHERE { ?s a ?class . } 
	  ```
	  #Query
- Properties
	- ```sparql
	  SELECT DISTINCT ?property 
	  WHERE { ?s ?property ?o . } 
	  ```
	  #Query
- Properties ranked by use
	- ```sparql
	  SELECT ?p (COUNT (DISTINCT ?o) AS ?nv)
	  
	  WHERE {
	      ?s ?p ?o 
	  }
	  
	  GROUP BY ?p
	  ORDER BY DESC (?nv)
	  
	  ```
	  #Query #COUNT #[[GROUP BY]]