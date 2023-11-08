type:: [[Ontology]]

- The specification of SKOS-XL is available as a [separate document](https://www.w3.org/TR/skos-reference/skos-xl.html) and as a [section within the SKOS specification](https://www.w3.org/TR/skos-reference/#xl).
- This page describes the resulting extended ontology SKOS + SKOS-XL which is what in practice is referred to as SKOS-XL.
- ## Prefixes
  collapsed:: true
	- ```sparql
	  # SKOS prefixes in the form used in SPARQL 
	  PREFIX skos:   <http://www.w3.org/2004/02/skos/core#>
	  PREFIX skosxl: <http://www.w3.org/2008/05/skos-xl#>
	  ```
- ## Class Diagram
  collapsed:: true
	- ![image.png](../assets/SKOS-XLdiagram.png){:height 628, :width 746}
		- #+BEGIN_NOTE
		  Doesn't show all object properties and none of the annotation properties. See the complete class and property hierarchies below.
		  #+END_NOTE
- ## Classes
  collapsed:: true
	- skos:Collection
		- skos:OrderedCollection
	- skos:Concept
	- skos:ConceptScheme
	- **skosxl:Label**
- ## Properties
  collapsed:: true
	- ### Annotation properties
	  collapsed:: true
		- rdfs:label
			- skos:prefLabel
			- skos:altLabel
			- skos:hiddenLabel
		- skos:note
			- skos:definition
			- skos:changeNote
			- skos:editorialNote
			- skos:example
			- skos:historyNote
			- skos:scopeNote
	- ### Object properties
	  collapsed:: true
		- skos:hasTopConcept
		- skos:inScheme
		- skos:member
		- skos:memberList
		- skos:semanticRelation
		  collapsed:: true
			- skos:broaderTransitive
				- skos:broader
					- skos:broadMatch
			- skos:narrowerTransitive
				- skos:narrower
					- skos:narrowMatch
			- skos:related
				- skos:relatedMatch
			- skos:mappingRelation
				- skos:broadMatch
				- skos:closeMatch
					- skos:exactMatch
		- skos:topConceptOf
		- **skosxl:altLabel**
		- **skosxl:hiddenLabel**
		- **skosxl:labelRelation**[*](https://www.w3.org/TR/skos-reference/#xl-label-relations)
		- **skosxl:prefLabel**
	- ### Datatype properties
		- skos:notation
		- **skosxl:literalForm**
- ## Queries
  collapsed:: true
	- Get all properties and classes of [[SKOS-XL]] (including [[SKOS]])
		- ```sparql
		  SELECT DISTINCT ?Class ?aProperty ?oProperty ?dProperty
		  
		  WHERE {
		  {VALUES ?ns {"http://www.w3.org/2008/05/skos-xl#" "http://www.w3.org/2004/02/skos/core#"}
		  ?Class a owl:Class .
		  FILTER (strstarts(str(?Class), ?ns))}
		  
		  UNION
		  {
		  VALUES ?ns {"http://www.w3.org/2008/05/skos-xl#" "http://www.w3.org/2004/02/skos/core#"}
		  ?aProperty a owl:AnnotationProperty.
		  FILTER (strstarts(str(?aProperty), ?ns))
		  }
		    
		  UNION
		  
		  {VALUES ?ns {"http://www.w3.org/2008/05/skos-xl#" "http://www.w3.org/2004/02/skos/core#"}
		  ?oProperty a owl:ObjectProperty .
		  FILTER (strstarts(str(?oProperty), ?ns))}
		  
		  UNION
		  {VALUES ?ns {"http://www.w3.org/2008/05/skos-xl#" "http://www.w3.org/2004/02/skos/core#"}
		  ?dProperty a owl:DatatypeProperty .
		  FILTER (strstarts(str(?dProperty), ?ns))}
		  
		  }
		  ORDER BY  ?dProperty ?oProperty ?aProperty
		  ```
			- #VALUES #UNION #STRSTARTS #Query