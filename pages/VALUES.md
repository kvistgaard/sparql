- A keyword for providing inline data, a list of values inside `{ }`
- [[Example]]
  id:: 61e6cd78-f627-493f-ae7c-04ccf880ad1a
	- ```sparql
	  #title: Notable books on linked data, semantic technologies, and semantic knowledge graphs
	   
	  SELECT DISTINCT ?book ?title (GROUP_CONCAT (DISTINCT ?author; SEPARATOR = ", ") AS ?authors) ?pubDate
	  {
	    VALUES ?book {wd:Q17744504 wd:Q17744476 wd:Q61718117 wd:Q59784970 wd:Q17744339 wd:Q51601248 wd:Q17744488 wd:Q27942623  wd:Q108378522 wd:Q110549106 wd:Q109673922 wd:Q93431614}
	           
	           ?book wdt:P1476 ?title.
	           OPTIONAL {?book (wdt:P50/rdfs:label)|(wdt:P98/rdfs:label)|wdt:P2093 ?author
	                     FILTER (LANG(?author)=""||LANG(?author)="en")}
	           OPTIONAL {?book wdt:P577 ?pubDate}
	  
	  }
	  GROUP BY ?book ?title ?pubDate
	  ```
	  #Wikidata #Query #II #OPTIONAL
- Allows multiple variables
- [[Syntax]]
	- ```sparql
	  #note: this is a snippet, not a valid query
	  
	  VALUES (?x ?y ?z) {(:URI1 "ex" 1) (:URI2 "wye" 2) (:URI3 "zed" UNDEF)}
	  ```
		- The third list has no value for `?z`, shown by the keyword `UNDEF`
	- `()` can be omitted for single values as in the [example above](((61e6cd78-f627-493f-ae7c-04ccf880ad1a)))