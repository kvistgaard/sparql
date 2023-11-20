type:: [[Function/Aggregate Function]]

- [[Example]]
  collapsed:: true
	- ```sparql
	  PREFIX foaf: <http://xmlns.com/foaf/0.1/>
	  PREFIX foaf: <http://xmlns.com/foaf/0.1/>
	  PREFIX dbo: <http://dbpedia.org/ontology/>
	  SELECT ?author  (COUNT (DISTINCT ?work) AS ?NumberOfWorks)
	  WHERE {
	    ?work a dbo:Artwork .
	    ?work dbo:author ?author . 
	  }
	  GROUP BY ?author
	  HAVING (COUNT (DISTINCT ?work) > 50)
	  ORDER BY DESC(?NumberOfWorks)
	  
	  ```
	  #Query #[[GROUP BY]] #[[ORDER BY]] #DESC