# Represent and capture concept and attribute versioning in the geological time scale
A vocabulary that tries to document the different versions of the international geologic time scale. 

There are continuous changes in the international geologic time scale, e.g. adding and removal of concepts, or changes in the attribute of concepts. A semantic model was developed to represent those versioning changes. A case study was done to capture all the changes in the International Chronostratigraphic Chart from 2004 to 2018. In the work we have reused the ontologies and vocabularies developed by Dr. Simon Cox and his colleagues. Their vocabularies are archived at a folder on the GeoSciML website http://resource.geosciml.org/vocabulary/timescale/. 

A SPARQL endpoint has been set up for the developed vocabulary at http://virtuoso.nkn.uidaho.edu:8890/sparql/. To query the vocabulary, a user needs to specify the graph name <http://deeptimekb.org/iscallnew> . Below is an example: 

```
########### Use case 1: Find the values of base boundary time and undertainty 
########### of Jurassic in the 2012-08 ISC chart #########
prefix dc: <http://purl.org/dc/elements/1.1/> 
prefix dcterms: <http://purl.org/dc/terms/> 
prefix foaf: <http://xmlns.com/foaf/0.1/> 
prefix geo: <http://www.opengis.net/ont/geosparql#> 
prefix gts: <http://resource.geosciml.org/ontology/timescale/gts#> 
prefix isc: <http://resource.geosciml.org/classifier/ics/ischart/> 
prefix owl: <http://www.w3.org/2002/07/owl#> 
prefix rank: <http://resource.geosciml.org/ontology/timescale/rank/> 
prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> 
prefix samfl: <http://def.seegrid.csiro.au/ontology/om/sam-lite#> 
prefix sf: <http://www.opengis.net/ont/sf#> 
prefix skos: <http://www.w3.org/2004/02/skos/core#> 
prefix sosa: <http://www.w3.org/ns/sosa/> 
prefix thors: <http://resource.geosciml.org/ontology/timescale/thors#> 
prefix time: <http://www.w3.org/2006/time#> 
prefix ts: <http://resource.geosciml.org/vocabulary/timescale/> 
prefix vann: <http://purl.org/vocab/vann/> 
prefix void: <http://rdfs.org/ns/void#> 
prefix xkos: <http://rdf-vocabulary.ddialliance.org/xkos#> 
prefix xsd: <http://www.w3.org/2001/XMLSchema#> 

SELECT ?tconcept ?basetimevalue ?btuncertvalue 
WHERE
{
  GRAPH <http://deeptimekb.org/iscallnew> 
   {
	?tconcept skos:prefLabel "Jurassic"@en ;  

                 dc:description  
                     [   
	                    time:hasBeginning ?baseboundary ;
	                    skos:inScheme ts:isc2012-08
                     ] .
	
        ?baseboundary time:inTemporalPosition ?basetime .
	
        ?basetime dc:description
			         [ 
			             time:numericPosition ?basetimevalue ;
			             skos:inScheme ts:isc2012-08 
			         ]  ;
                          gts:positionalUncertainty ?basetimeuncert .

        ?basetimeuncert   dc:description
					  [ 
					     time:numericDuration ?btuncertvalue ;
					     skos:inScheme ts:isc2012-08 
				      ] .
   }
}

#####################
```

![Different versions of the GTS chart](/gtsversion.png)
