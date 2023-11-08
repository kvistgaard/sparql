public:: false

- ---
	- Property path table -- not used due to the Logseq bug
		- |Syntax|Name|Matches|
		  |--|--|--|
		  |^property|Inverse Path|Inverse path (object to subject).|
		  |property1 / property2|Sequence Path|A sequence path of property1 followed by property2.|
		  |property\|property2| Alternative Path| Property1 or property2 (all possibilities are tried).|
		  |property*|Zero Or More|A path that connects the subject and object of the path by zero or more matches of property.|
		  |property+|One Or More|A path that connects the subject and object of the path by one or more matches of property.|
		  |property?|Zero Or One Path|A path that connects the subject and object of the path by zero or one matches of property.|
	-