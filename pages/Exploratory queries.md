- Properties in use
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
- Classes
	- ```sparql
	  SELECT DISTINCT ?class 
	  WHERE { ?s a ?class . } 
	  ```
	  #Query
- All triples
	- Asking for all triples makes sense when you know that the dataset is small.
	- Most triple stores will give all accessible data with `SELECT * {?s ?p ?o}` but some my give only the triples in the default graph so it's better to ask explicitly for all the triples in all named graphs.
	- ```sparql
	  SELECT ?g ?s ?p ?o
	  WHERE
	  {
	  	{ ?s ?p ?o }
	  	UNION
	  	{ GRAPH ?g { ?s ?p ?o } }
	  }
	  ```#Query #GRAPH #UNION
	- Total number of triples (from all graphs)
	- ```sparql
	  SELECT (COUNT (?s) as ?Number_of_triples)
	  
	  {
	     { ?s ?p ?o } UNION { GRAPH ?g { ?s ?p ?o } }
	  }
	  ```
	  #Query #COUNT #GRAPH #UNION
- Sample entity and count
	- ```sparql
	  SELECT (SAMPLE(?s) as ?sample) (count(?s) as ?count) ?class
	  
	  WHERE {?s a ?class }
	  
	  GROUP BY ?class
	  ORDER BY DESC(?count)
	  ```
	  #Query #SAMPLE