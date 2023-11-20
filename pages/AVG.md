type:: [[Function/Aggregate Function]]

- [[Example]]
  collapsed:: true
	- ```sparql
	  PREFIX dbp: <http://dbpedia.org/property/>
	  PREFIX dbo: <http://dbpedia.org/ontology/>
	  
	  SELECT (AVG(?wikiPageLength) as ?AverageWikiPageLength)
	  WHERE {
	    ?work a dbo:Artwork .
	    ?work dbo:wikiPageLength ?wikiPageLength .
	  }
	  ```
	  #Query