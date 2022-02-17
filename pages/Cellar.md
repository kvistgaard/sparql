type:: [[SPARQL Endpoint]], [[RDF Store]]
url:: http://publications.europa.eu/webapi/rdf/sparql
triples:: 1 865 610 770
date:: [[Feb 2nd, 2022]]

- Ontology: [[CDM]]
- Documentation
	- [Cellar - Publications Office of the EU](https://op.europa.eu/en/publication-detail/-/publication/50ecce27-857e-11e8-ac6a-01aa75ed71a1/language-en/format-PDF/source-250197260), [[Jul 11th, 2018]]
- [[Query]] [Examples]([[Example]])
	- African countries with number of EU laws related to them
		- ```sparql
		  #African countries with number of EU laws related to them
		  
		  PREFIX eurovoc: <http://eurovoc.europa.eu/>
		  PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
		  PREFIX cdm: <http://publications.europa.eu/ontology/cdm#>
		  
		  SELECT ?country_name (count(?law) as ?Number_of_laws) 
		  where {
		  ?country_code skos:prefLabel ?country_name.
		    
		   FILTER (LANG(?country_name) = "en").
		   ?law cdm:work_is_about_concept_eurovoc ?country_code.
		   ?country_code skos:inScheme eurovoc:100280 .
		  }
		  
		  GROUP BY ?country_name
		  ORDER BY DESC(?Number_of_laws)
		  
		  ```
		  #Query #FILTER #LANG #[[GROUP BY]] #[[ORDER BY]] #DESC