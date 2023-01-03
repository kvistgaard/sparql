# SPARQL Exercise solutions
SPARQL Endpoints
|Name|Endpoint URL|
|--|--|
|DBpedia|https://dbpedia.org/sparql|
|Wikidata|https://query.wikidata.org|
|CELLAR|http://publications.europa.eu/webapi/rdf/sparql|
|EU Knowledge Graph|https://query.linkedopendata.eu|
|Open Data Portal|https://data.europa.eu/sparql – [enhanced editor](https://data.europa.eu/data/sparql)|
|EC Data Platform|https://test-linked.ec-dataplatform.eu/sparql (test server)|
#### Q.2 Which of the leaders of member states of the European Union are independent politicians, according to DBpedia.


Q.2.1. Find EU member states with the following query:

```sparql
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX dbc: <http://dbpedia.org/resource/Category:>
PREFIX dbo: <http://dbpedia.org/ontology/>
SELECT DISTINCT ?MS ?leader
WHERE {
?MS    a           dbo:Country;
       dct:subject dbc:Member_states_of_the_European_Union }
```
- Q.2.2. Find all country leaders
- Q.2.3. Find the independent politicians among them

```sparql
PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbp: <http://dbpedia.org/property/>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX dbc: <http://dbpedia.org/resource/Category:>
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT DISTINCT ?MS ?leader
WHERE {
?MS    a           dbo:Country;
       dct:subject dbc:Member_states_of_the_European_Union ;
       dbp:leaderName ?leader .                   #Q.2.2
 
?leader dbp:party dbr:Independent_politician .    #Q.2.3
}
```
#### Q.3 Based on the query from Q.2, find the total number of children of EU leaders (of which Dbpedia “knows”).

```sparql

SELECT (COUNT (DISTINCT ?child) AS ?Number_of_children)

{
?MS a dbo:Country; 
    dct:subject dbc:Member_states_of_the_European_Union ;
    dbp:leaderName ?leader . 

?leader dbo:child ?child.
} 
```

```sparql
SELECT ?leader (COUNT (DISTINCT ?child) AS ?Number_of_children)

{
?MS a dbo:Country; 
    dct:subject dbc:Member_states_of_the_European_Union ;
    dbp:leaderName ?leader . 

?leader dbo:child ?child.
} 

GROUP BY ?leader
ORDER BY ?Number_of_children
```
#### Q.4 .....

```sparql
SELECT DISTINCT ?MS ?leader ?Age
 
WHERE {
?MS a           dbo:Country;
    dct:subject dbc:Member_states_of_the_European_Union ;
    dbp:leaderName ?leader .
?leader dbo:birthDate ?birthDate .
 
BIND (SUBSTR(STR(?birthDate),0,4) AS ?YearBorn)
BIND (SUBSTR(STR(NOW()),0,4) AS ?CurrentYear)
BIND (xsd:int(?CurrentYear)-xsd:int(?YearBorn) AS ?Age) }

 
ORDER BY ?Age
```
#### Q.5 ...

```sparql
SELECT ?monthBorn (COUNT (?leader) AS ?LB)
WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
?MS a            dbo:Country; 
        dct:subject dbc:Member_states_of_the_European_Union;
        dbp:leaderName ?leader . 
?leader dbo:birthDate ?birthDate . 
BIND (MONTH(?birthDate) AS ?monthBorn) 
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
GROUP BY ?monthBorn
ORDER BY ?monthBorn
```
#### Q.6 ...

```sparql
# Q.6.1
SELECT DISTINCT ?MS ?leader 
 
WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
?MS a           dbo:Country;
    dct:subject dbc:Member_states_of_the_European_Union;
    dbp:leaderName  ?leader .
 
FILTER NOT EXISTS {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?leader foaf:depiction ?image .}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​    #Q.6.1.a
#FILTER NOT EXISTS {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?leader dbo:child ?children .}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​  #Q.6.1.b
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```

```sparql
# Q.6.2
#All leaders of MS of the EU, with their children and image, if available​
 
SELECT DISTINCT ?MS ?leader ?children ?image
 
WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
 
?MS a              dbo:Country; 
    dct:subject    dbc:Member_states_of_the_European_Union; 
    dbp:leaderName ?leader . 
 
OPTIONAL {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?leader dbo:child ?children .}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
OPTIONAL {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?leader foaf:depiction ?image .}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​   
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
 
ORDER BY DESC(?children)
```

```sparql
# Q.6.3

SELECT 
COUNT (DISTINCT ?leader_No_children) AS ?NUM_leader_No_children
COUNT (DISTINCT ?leader_No_image) AS ?NUM_leader_No_image 
 
WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
?MS a dbo:Country; dct:subject dbc:Member_states_of_the_European_Union .
 
      {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?MS dbp:leaderName ?leader_No_children . 
      FILTER NOT EXISTS {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?leader_No_children dbo:child ?children}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
      }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
 
      UNION 
 
      {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?MS dbp:leaderName ?leader_No_image . 
      FILTER NOT EXISTS {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?leader_No_image foaf:depiction ?image}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
      }​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```
#### Q.7 (Homework) In the VocBench project OP_TRAINING_EuroVoc_MT5211,
1. Get all concepts together with their preferred label, literal form in one EU language, and the number of alternative labels sorted in descending order.
2. Get all concepts without alternative label
- As list of results, showing their literal form in one EU language;
- As number.

```sparql
SELECT ?concept ?prefLabelURI ?prefLabel (COUNT (DISTINCT ?altLabel) as ?altLabels)

WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    ?concept a skos:Concept ;
    skosxl:prefLabel ?prefLabelURI ;
    skosxl:altLabel ?altLabel .
?prefLabelURI skosxl:literalForm ?prefLabel .
    
FILTER (LANG(?prefLabel) = "en")
    
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 

GROUP BY ?concept ?prefLabelURI ?prefLabel
ORDER BY DESC(?altLabels)
```

```sparql
SELECT ?concept ?prefLabelURI ?prefLabel 

WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    ?concept a skos:Concept;
    skosxl:prefLabel ?prefLabelURI .
?prefLabelURI skosxl:literalForm ?prefLabel .
    
FILTER (LANG(?prefLabel) = "en")
FILTER NOT EXISTS {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​?concept skosxl:altLabel ?altLabelURI}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
```
#### Q.8

```sparql
SELECT ?concept ?prefLabelURI ?prefLabel (COUNT (DISTINCT ?altLabel) as ?altLabels)

WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
    ?concept a skos:Concept ;
    skosxl:prefLabel ?prefLabelURI ;
    skosxl:altLabel ?altLabel .
?prefLabelURI skosxl:literalForm ?prefLabel .
    
FILTER (LANG(?prefLabel) = "en")
FILTER (STRSTARTS(STR(?concept), "http://eurovoc.europa.eu/"))    
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​

GROUP BY ?concept ?prefLabelURI ?prefLabel
ORDER BY DESC(?altLabels)
```
#### Q.9

```sparql
SELECT ?concept ?prefLabel

WHERE {​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
?concept a skos:Concept .
?concept skosxl:prefLabel   ?label .
?label   skosxl:literalForm ?prefLabel .
FILTER (lang ( ?prefLabel )="en")
FILTER REGEX (?prefLabel, "wild", "i")
}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
```
#### Q.10

```sparql
SELECT *
{​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ ?concept skosxl:hiddenLabel/skosxl:literalForm ?hiddenLabel .}​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​ 
```
#### Q.11 Find in Cellar all SKOS notes in one EU language.

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

SELECT DISTINCT * 

WHERE {
  ?s ?noteType ?note .
  ?noteType rdfs:subPropertyOf* skos:note .
  
FILTER (LANG(?note) = "en")
    
}

LIMIT 10
```
#### Q.12 Explore Wikidata
#### Q.13 Find the 1000 most populated cities from Wikidata and show their Chinese labels.

```sparql

SELECT DISTINCT ?city ?cityLabel ?population
{
  ?city wdt:P31/wdt:P279* wd:Q515;
             wdt:P1082 ?population;
             rdfs:label ?cityLabel .
#FILTER (LANG(?cityLabel) = "zh")
FILTER LANGMATCHES(LANG(?cityLabel), "zh")
}
ORDER BY DESC (?population)
LIMIT 10
```
#### Q.14 Get the following data from Wikidata about head of states of Member States of the EU:
Q.14.1 Get image grid of all head of states of Member States of the EU.

```sparql
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
SELECT DISTINCT ?ms ?msLabel ?hos ?hosLabel ?hosImage 
 
WHERE {
  ?ms wdt:P463 wd:Q458;
      wdt:P35 ?hos .
  ?hos wdt:P18 ?hosImage ;
  
      SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
```
Q.14.2. Find spouses of these heads of state, if available.


```sparql
SELECT DISTINCT ?ms ?msLabel ?hos ?hosLabel ?spouseLabel 
 
WHERE {
  ?ms wdt:P463 wd:Q458;
      wdt:P35 ?hos .
 
      OPTIONAL {?hos wdt:P26 ?spouse .}
  
      SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}

ORDER BY DESC(?spouseLabel)
LIMIT 10
```
Q.14.3. Find the start dates of all head of states of EU members, for which there is information in Wikidata.


```sparql
SELECT DISTINCT ?ms ?hos ?hosLabel ?msLabel ?start
 
WHERE {
  ?ms wdt:P463 wd:Q458;
      p:P35 [ ps:P35 ?hos;
            pq:P580 ?start] .
  
      SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
ORDER BY ?msLabel
```
#### Q.15 (Homework) Get the population growth of all current EU member states in the last 20 years on a line chart using the query service of Wikidata.

```sparql

#defaultView:LineChart
SELECT ?date ?population ?msLabel 
 
WHERE {
  ?ms wdt:P463 wd:Q458;
      p:P1082 [ps:P1082 ?population ;
               pq:P585 ?date].
  FILTER (?date > "1990-01-01T00:00:00Z"^^<http://www.w3.org/2001/XMLSchema#dateTime>)
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}

ORDER BY ?date
```
#### Q.16 Based on the query for influences in the age of Enlightenment, get the influences of Hume, Descartes, Locke, and Kant .

```sparql

SELECT DISTINCT ?a ?aLabel (GROUP_CONCAT (?bLabel ; SEPARATOR = ", ") AS ?influencedBy)

{
 VALUES ?a { wd:Q37160 wd:Q9191 wd:Q9353 wd:Q9312}
  
  ?a wdt:P31 wd:Q5;
    wdt:P569 ?birth;
    wdt:P737 ?b .
 ?b wdt:P31 wd:Q5 ;
    rdfs:label ?bLabel .
 
 FILTER (LANG(?bLabel) = "en")
 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
 
 }
GROUP BY ?a ?aLabel
```
#### Q.17 For the 4 philosophers from Q.16, extend the query by getting the short description about them, extracted by Dbpedia from Wikipedia.

```sparql


SELECT DISTINCT ?a ?aLabel ?description (GROUP_CONCAT (?bLabel ; SEPARATOR = ", ") AS ?influencedBy)

{
 
SERVICE <http://dbpedia.org/sparql> {
   VALUES ?a { wd:Q37160 wd:Q9191 wd:Q9353 wd:Q9312}
                  ?DBitem owl:sameAs ?a;
                   rdfs:comment ?description.
                   FILTER (LANG(?description) = "en")   } 

SERVICE <https://query.wikidata.org/bigdata/namespace/wdq/sparql>
  {?a wdt:P31 wd:Q5;
    wdt:P569 ?birth;
    rdfs:label ?aLabel;
    wdt:P737 ?b .
 ?b wdt:P31 wd:Q5 ;
    rdfs:label ?bLabel .
   
 FILTER (LANG(?aLabel) = "en")
 FILTER (LANG(?bLabel) = "en")
 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
  }
                                   
 }
GROUP BY ?a ?aLabel ?description
```
#### Q.18 (Homework) Get from Wikidata all paintings painted on wood as image grid, including information on when they were created, if available.

```sparql
# [endpoint=https://query.wikidata.org/bigdata/namespace/wdq/sparql]
#defaultView:ImageGrid
SELECT DISTINCT ?painting ?paintingLabel ?image ?inception
WHERE
{
  ?painting wdt:P31/wdt:P279* wd:Q3305213;
            wdt:P18 ?image;
            p:P186 [ ps:P186 wd:Q287; pq:P518 wd:Q861259 ].
  OPTIONAL {?painting wdt:P571 ?inception }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]". }
}

LIMIT 20
```
#### Q.19 (Homework) In VocBench, from OP_TRAINING_place, find all concepts that:
1. have `skos:prefLabel` in English;
2. have **only** English `skos:prefLabel`;
3. have `skos:prefLabel` or `skos:altLabel` in any of the languages of the Baltic or Nordic EU member states.

```sparql
# Q.19.1

PREFIX skosxl: <http://www.w3.org/2008/05/skos-xl#>

SELECT ?concept ?prefLabel_EN
{
?concept skosxl:prefLabel/skosxl:literalForm ?prefLabel_EN 
FILTER (LANG(?prefLabel_EN) = "en")
}
```

```sparql
# Q.19.2
PREFIX skosxl: <http://www.w3.org/2008/05/skos-xl#>
SELECT ?concept ?prefLabel_EN
{
?concept skosxl:prefLabel/skosxl:literalForm ?prefLabel_EN 
FILTER (LANG(?prefLabel_EN) = "en")
    
FILTER  NOT EXISTS {?concept skosxl:prefLabel/skosxl:literalForm ?prefLabel . 
                            FILTER (LANG(?prefLabel) != LANG(?prefLabel_EN))}
}
```

```sparql
# Q.19.3

PREFIX skosxl: <http://www.w3.org/2008/05/skos-xl#>

SELECT ?concept ?label
{
VALUES ?tag {"da" "et" "fi" "lt" "lv" "sv"}
?concept (skosxl:prefLabel|skosxl:altLabel)/skosxl:literalForm ?label
FILTER (LANG(?label) = ?tag)
}
```
#### Q.20 Compare the number of preferred labels with the same literal form in OP_TRAINING_country and OP_TRAINING_place in English, French, Spanish and Italian.

```sparql
SELECT ?tag (COUNT (DISTINCT ?label) as ?NoL)

{
VALUES ?tag {"en" "fr" "es" "it" }
    ?country skosxl:prefLabel/skosxl:literalForm ?label
     FILTER (LANG(?label) = ?tag)
    
    SERVICE <repository:OP_TRAINING_place_core> {
        ?place skosxl:prefLabel/skosxl:literalForm ?label
       FILTER (LANG(?label) = ?tag)
    }
}
GROUP BY ?tag
ORDER BY ?NoL
```
#### Q.21 Find all named graphs on CELLAR and the EC Data Platfom, sort them by number of triples and get their meta-data, if available.

```sparql
# [endpoint=https://linked.ec-dataplatform.eu/sparql]
SELECT DISTINCT ?g ?gp ?go (COUNT (?s) as ?nt)
WHERE {
    GRAPH ?g { ?s ?p ?o }
    OPTIONAL {?g ?gp ?go}
}
GROUP BY ?g ?gp ?go
ORDER BY DESC(?nt)
LIMIT 20
```
#### Q.22 Get all member states of EU from Wikidata, their population and the corresponding concept in CELLAR from the country NAL.

```sparql
# [endpoint=https://query.wikidata.org/bigdata/namespace/wdq/sparql]

prefix at: <http://publications.europa.eu/ontology/authority/> 
prefix atold: <http://publications.europa.eu/resource/authority/> 

SELECT DISTINCT ?concept ?country ?population
{   ?country wdt:P298 ?code;
           wdt:P463 wd:Q458 ;
           wdt:P1082 ?population .
  SERVICE <http://publications.europa.eu/webapi/rdf/sparql>
          { ?concept skos:inScheme atold:country;
                     at:authority-code ?code}      
  }
```

```sparql
# version with all prefixes to be used e.g. at https://yasgui.triply.cc

PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
prefix at: <http://publications.europa.eu/ontology/authority/> 
prefix atold: <http://publications.europa.eu/resource/authority/> 
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

SELECT DISTINCT ?concept ?country ?population
{   ?country wdt:P298 ?code;
           wdt:P463 wd:Q458 ;
           wdt:P1082 ?population .
  SERVICE <http://publications.europa.eu/webapi/rdf/sparql>
          { ?concept skos:inScheme atold:country;
                     at:authority-code ?code}      
  }

```
#### Q.23 Which properties in the ERA (http://era.europa.eu/knowledge-graph) and CORDIS graph (https://linked.ec-dataplatform.eu/cordis) are used more than 100000 times? Get them grouped by named graph, showing the number of distinct objects for each property.

```sparql
# [endpoint=https://linked.ec-dataplatform.eu/sparql]

SELECT ?g ?p (COUNT (DISTINCT ?o) AS ?nv)
FROM NAMED <https://linked.ec-dataplatform.eu/cordis>
FROM NAMED <http://era.europa.eu/knowledge-graph>

WHERE {
  GRAPH ?g { ?s ?p ?o }
}

GROUP BY ?g ?p 
HAVING (COUNT (DISTINCT ?o) > 100000)
ORDER BY ?g DESC (?nv)
```
#### Q.24 Using the solution of Q.22, construct a graph with triples asserting that the country concept of the NAL is the same as (using `owl:sameAs`) the corresponding item from Wikidata.

```sparql
# [endpoint=https://query.wikidata.org/bigdata/namespace/wdq/sparql]

PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wd: <http://www.wikidata.org/entity/>
prefix at: <http://publications.europa.eu/ontology/authority/> 
prefix atold: <http://publications.europa.eu/resource/authority/> 
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

CONSTRUCT {?concept owl:sameAs ?country}
{   ?country wdt:P298 ?code;
           wdt:P463 wd:Q458 .
  SERVICE <http://publications.europa.eu/webapi/rdf/sparql>
          { ?concept skos:inScheme atold:country;
                     at:authority-code ?code}      
  }
```
