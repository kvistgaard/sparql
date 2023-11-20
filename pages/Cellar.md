type:: [[SPARQL Endpoint]], [[RDF Store]]
url:: http://publications.europa.eu/webapi/rdf/sparql
triples:: 1 865 610 770
date:: [[Feb 2nd, 2022]]

- Ontology: [[CDM]]
- Documentation
	- [Cellar - Publications Office of the EU](https://op.europa.eu/en/publication-detail/-/publication/50ecce27-857e-11e8-ac6a-01aa75ed71a1/language-en/format-PDF/source-250197260), [[Jul 11th, 2018]]
- [[Query]] [Examples]([[Example]])
	- All regulation related to "data protection" with links to content in HTML in English.
		- For other topics, replace or add one or more [[Eurovoc]] concepts in the [[VALUES]] list.
		- For other languages formats, change the part with which the ELI is appended in the SELECT statement
		- ```sparql
		  PREFIX cdm: <http://publications.europa.eu/ontology/cdm#>
		  PREFIX euvoc: <http://eurovoc.europa.eu/>
		  PREFIX skosxl: <http://www.w3.org/2008/05/skos-xl#>
		  PREFIX lang:<http://publications.europa.eu/resource/authority/language/>
		  
		  SELECT DISTINCT ?reg (IRI(CONCAT(STR(?eli),"/eng/html")) AS ?HTML_URL) ?title ?topic
		  
		  {
		      VALUES ?topicURI {euvoc:5181}
		      ?reg cdm:resource_legal_eli ?eli;
		      cdm:work_is_about_concept_eurovoc ?topicURI .
		      
		      ?exp cdm:expression_belongs_to_work ?reg .
		      ?exp cdm:expression_uses_language lang:ENG . 
		      ?exp cdm:expression_title ?title .
		  
		      ?topicURI skosxl:prefLabel/skosxl:literalForm ?topic
		      FILTER (LANG(?topic) = "en")
		  }
		  
		  ```
		  #Query #IRI #CONCAT #STR #FILTER
	- African countries with number of EU laws related to them
	  collapsed:: true
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
		  #Query #FILTER #LANG #[[ORDER BY]] #[[GROUP BY]] #[[ORDER BY]] #DESC
	- Who-is-who data for a person, based on family name
	  collapsed:: true
		- ```sparql
		  PREFIX cdm: <http://publications.europa.eu/ontology/cdm#> 
		  PREFIX skos: <http://www.w3.org/2004/02/skos/core#> 
		  PREFIX foaf: <http://xmlns.com/foaf/0.1/> 
		  PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
		  PREFIX euvoc: <http://publications.europa.eu/ontology/euvoc#> 
		  PREFIX org: <http://www.w3.org/ns/org#> 
		  PREFIX vcard: <http://www.w3.org/2006/vcard/ns#>
		  PREFIX person: <http://publications.europa.eu/resource/person>
		  
		  SELECT DISTINCT ?person ?hasMembership ?org ?prefLabel ?familyName ?givenName ?citizenship ?img ?hasHonorificPrefix ?role
		  ?prefLabelRole ?positionComplement ?homepage ?hasEmail ?tel
		  WHERE {
		      ?person rdf:type foaf:Person.
		      ?person org:hasMembership ?hasMembership.
		      FILTER(STR(?familyName)= 'VON DER LEYEN').
		      OPTIONAL {?hasMembership org:organization ?org .
		                ?person foaf:familyName ?familyName. 
		          OPTIONAL {?org skos:prefLabel ?prefLabel. FILTER(LANGMATCHES(LANG(?prefLabel),"en"))}
		          OPTIONAL {?person foaf:givenName ?givenName.}
		          OPTIONAL {?person person:citizenship ?citizenship.}
		          OPTIONAL {?person foaf:img ?img}
		          OPTIONAL {?person vcard:hasHonorificPrefix ?hasHonorificPrefix.}
		          OPTIONAL {?hasMembership org:role ?role. ?role skos:prefLabel ?prefLabelRole. 
		                    FILTER(LANGMATCHES(LANG(?prefLabelRole),"en"))}
		          OPTIONAL {?hasMembership euvoc:positionComplement ?positionComplement. 
		                    FILTER(LANGMATCHES(LANG(?positionComplement),"en"))}
		          OPTIONAL {?hasMembership euvoc:contactPoint ?contactPoint.
		              OPTIONAL {?contactPoint vcard:hasAddress ?hasAddress 
		                  OPTIONAL {?contactPoint foaf:homepage ?homepage}
		                  OPTIONAL {?contactPoint vcard:hasEmail ?hasEmail} 
		                  OPTIONAL {?contactPoint vcard:hasTelephone ?hasTelephone.
		                              ?hasTelephone vcard:hasValue ?tel.}
		                         }
		                  } 
		              } 
		      }
		  ```
		  #Query #OPTIONAL #langMATCHES
	- More examples available [here](https://docs.google.com/presentation/d/1oGZjnkFemOuiitf5xAi7VeDxK8_3rm1O/edit#slide=id.p1).