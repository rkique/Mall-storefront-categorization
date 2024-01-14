Workflow:

1. (Using the Overpass API) Get JSON output files for mall geometries. Most should have type Way.

```
[out:json]; area["ISO3166-2"="US-WA"]->.searchArea; 
// Use ISO3166-2 code for Washington 
( 
node["shop"="mall"](area.searchArea);
way["shop"="mall"](area.searchArea);
relation["shop"="mall"](area.searchArea);
);
//Recurse on way nodes to get node outputs (coordinates)
(._;>;); 
out;
```

1. run build_queries_from_ways to convert the (way) output to the bounds of a new overpass query, this time for individual nodes in the area above. Save these queries as part of a JSON object with the original tags:
```
{
"query": "node(poly:\" 47.6214674 -122.1282555 ..."); \n",
 "tags": {"addr:city": "Bellevue", 
          "addr:street": "Northeast 8th Street",
          ...
          "name": "Crossroads Bellevue"}
}
```
2. run overpass queries, saving each into a separate json file representing a mall

Repeat 1,2,3 as necessary. We now have tagged node outputs for as many malls as desired.

4. Separate output into Jewelry/ Non-Jewelry stores.
5. Visualize this output as desired.