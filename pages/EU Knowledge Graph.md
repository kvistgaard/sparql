type:: [[SPARQL Endpoint]], [[RDF Store]]
url:: https://query.linkedopendata.eu
triples:: 274 736 517
date:: [[Feb 14th, 2022]]

- [[Example]] queries
	- [▶ Try](https://tinyurl.com/y6uzcnlw)
	  ```sparql
	  #Kohesio projects on a map
	  #defaultView:Map
	  SELECT ?KohesioProject ?location  {
	    VALUES ?country {wd:Q23 wd:Q12} # Estonia, Denmark
	    ?KohesioProject wdt:P35 wd:Q9934 ;
	                    wdt:P32 ?country ; 
	                    wdt:P127 ?location .
	  }
	  ```
	  #Query #VALUES
	-
	- [▶ Try](https://tinyurl.com/y76r5h6)
	  ```sparql
	  SELECT ?countryLabel (xsd:integer(SUM(?EUcontribution)) as ?sum) {  
	    VALUES ?country {wd:Q18 wd:Q14 wd:Q27 } # Portugal, Lithuania, Slovenia  
	    ?KohesioProject wdt:P35  wd:Q9934 ;                  
	                    wdt:P32  ?country ;                   
	                    wdt:P835 ?EUcontribution .  
	    SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en"}
	  }
	  GROUP BY ?countryLabel
	  ```
	  #Query #VALUES #SUM #[[GROUP BY]]
	-
	- [▶ Try](https://tinyurl.com/y9ek83wo)
	  ```sparql
	  SELECT * 
	  { ?s wdt:P841 ?beneficiario ;
	       wdt:P474 ?presupuesto ;
	       wdt:P835 ?contribucion_eu ;
	       wdt:P837 ?porcentaje_financiacion ;
	       wdt:P270288 ?lugar ;
	       wdt:P460 ?codigo_postal ;
	       wdt:P1845 wd:Q2550039 ;
	       wdt:P836 ?resumen ;
	       wdt:P416470 ?id_spanish ;
	       wdt:P20 ?fecha_inicio ;
	       wdt:P33 ?fecha_fin ;
	       wdt:P127 ?coordenadas .
	       FILTER ( LANG(?resumen) = 'es' ).
	                 }
	  ORDER BY DESC(?contribucion_eu)
	  LIMIT 10
	  ```
	  #Query