- [VocBench: SPARQL](http://vocbench.uniroma2.it/doc/user/sparql.jsf) #Documentation
- Queries can be stored in VocBench according to the following patterns:
	- USER – specific for the user, on all projects)
	- PROJECT – specific for the project, on all users of that project
	- PROJECT_USER –  specific to the user and only for that project
	- SYSTEM – visible to all users on all projects
- Query several projects at once
	- [[Example]]
		- ```sparql
		  SELECT * WHERE {
		      ?localConcept a skos:Concept .
		      SERVICE <repository:OP_TRAINING_country_core> {
		          ?countryConcept a skos:Concept .
		      }
		  }
		  ```
		  #[[Federated Query]] #OP
	- In this example the query is executed in a project different than OP_TRAINING and combines results from both
	- #+BEGIN_NOTE
	  The repository name might depend on the installation. In the VocBench installation of the [[Publications Office]], the repository name is the project name appended with `_core`
	  #+END_NOTE
- [[PREFIXES]]
	- ```turtle
	  PREFIX adms: <http://www.w3.org/ns/adms#>
	  PREFIX cc: <http://creativecommons.org/ns#>
	  PREFIX cdm: <http://publications.europa.eu/ontology/cdm#>
	  PREFIX corrStatus: <http://publications.europa.eu/resource/authority/correction-status/>
	  PREFIX dataTypeDefinitions: <http://publications.europa.eu/ontology/euvoc/dataTypeDefinitions#>
	  PREFIX dc: <http://purl.org/dc/elements/1.1/>
	  PREFIX dcat: <http://www.w3.org/ns/dcat#>
	  PREFIX dct: <http://purl.org/dc/terms/>
	  PREFIX eli-o: <http://data.europa.eu/eli/ontology#>
	  PREFIX euvoc: <http://publications.europa.eu/ontology/euvoc#>
	  PREFIX event: <http://purl.org/NET/c4dm/event.owl#>
	  PREFIX externalImports: <http://publications.europa.eu/ontology/euvoc/externalImports#>
	  PREFIX foaf: <http://xmlns.com/foaf/0.1/>
	  PREFIX geosparql: <http://www.opengis.net/ont/geosparql#>
	  PREFIX gn: <http://www.geonames.org/ontology#>
	  PREFIX grddl: <http://www.w3.org/2003/g/data-view#>
	  PREFIX internalImports: <http://publications.europa.eu/ontology/euvoc/internalImports#>
	  PREFIX isothes: <http://purl.org/iso25964/skos-thes#>
	  PREFIX kml: <http://www.opengis.net/kml/2.2>
	  PREFIX legalDescriptions: <http://publications.europa.eu/ontology/euvoc/legalDescriptions#>
	  PREFIX lemon: <http://lemon-model.net/lemon#>
	  PREFIX lexinfo: <http://www.lexinfo.net/ontology/2.0/lexinfo#>
	  PREFIX lexvo: <http://lexvo.org/ontology#>
	  PREFIX linguisticDescriptions: <http://publications.europa.eu/ontology/euvoc/linguisticDescriptions#>
	  PREFIX locn: <https://www.w3.org/ns/locn#>
	  PREFIX org: <http://www.w3.org/ns/org#>
	  PREFIX organisationDescriptions: <http://publications.europa.eu/ontology/euvoc/organisationDescriptions#>
	  PREFIX owl: <http://www.w3.org/2002/07/owl#>
	  PREFIX prov: <http://www.w3.org/ns/prov#>
	  PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
	  PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
	  PREFIX saxon-ext: <http://www.w3.org/2005/xpath-functions>
	  PREFIX sf: <http://www.opengis.net/ont/sf#>
	  PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
	  PREFIX skosxl: <http://www.w3.org/2008/05/skos-xl#>
	  PREFIX spatialDescriptions: <http://publications.europa.eu/ontology/euvoc/spatialDescriptions#>
	  PREFIX tableDescriptions: <http://publications.europa.eu/ontology/euvoc/tableDescriptions#>
	  PREFIX temporalDescriptions: <http://publications.europa.eu/ontology/euvoc/temporalDescriptions#>
	  PREFIX time: <http://www.w3.org/2006/time#>
	  PREFIX vcard: <http://www.w3.org/2006/vcard/ns#>
	  PREFIX void: <http://rdfs.org/ns/void#>
	  PREFIX wgs: <http://www.w3.org/2003/01/geo/wgs84_pos#>
	  PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
	  PREFIX xsi: <http://www.w3.org/2001/XMLSchema-instance>
	  ```