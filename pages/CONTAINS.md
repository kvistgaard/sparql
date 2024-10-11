- Find cases where argument1 contains argument2. The output is `true` or `false`.
- ```sparql
  xsd:boolean  CONTAINS (string literal argument1, string literal argument2)
  ```
- [[Example]]
	- Here's [the example for REGEX](((61fd3a3d-81b5-448d-a76f-d1b0008b7476))) modified to use CONTAINS (Note: the two queries are not equivalent)
	- ```sparql
	  PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
	  PREFIX dbo: <http://dbpedia.org/ontology/>
	  
	  SELECT DISTINCT ?MusicalWork ?Artist
	  
	  WHERE {
	  ?MusicalWorkURI a dbo:MusicalWork;
	                 rdfs:label ?MusicalWork ;
	                 dbo:artist ?ArtistURI .
	  
	  ?ArtistURI rdfs:label ?Artist .
	  
	  FILTER (lang(?MusicalWork) = "en")
	  FILTER (lang(?Artist) = "en")
	  FILTER CONTAINS(?MusicalWork, "Broken")
	  }
	  ORDER BY ?MusicalWork
	  
	  ```
	  #Query #CONTAINS #FILTER #LANG