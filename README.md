# An Ontology for IT Operations, ITOPS
Authors: Rosario Uceda-Sosa, Nandana Mihindukulasooriya, Sahil Bansal, Seema Nagar, Atul Kumar, Vikas Agarwal, Gaetano Rossiello, Alfio Gliozzo 

Special thanks to Salim Roukos, Ruchi Mahindru and Yu Deng for their help and advice. 

The IT Operations ontology is built from a domain agnostic pipeline that leverages information from Wikidata, Wikipedia and DBPedia. There are three stages in the current pipeline, each extending the previous ones by using a variety of symbolic and ML/DL techniques. 

The outcome of each stage is a turtle (.ttl) file, ITOPS_S1.ttl, ITOPS_S2.ttl and ITOPS_S3.ttl which can be deployed separately and installed in a triplestore. All of them build upon a General Library of Objects (GLO), which
provides a general ontological framework to the domain specific graphs. These files are published under Apache 2.0 license. 

Please check the ITOPS_README.pdf file for further details and sample queries. 

For questions or comments pls email [rosariou@us.ibm.com](mailto:rosariou@us.ibm.com).

## How to query ITOPS ontology

In this section, we illustrate few example queries to extract information from the IT Operations ontology. 

---
#### List programming languages associated to different Adobe software products.

```sparql
prefix glo: <http://www.ibm.com/GLO#>
prefix itops: <http://www.ibm.com/ITOPS#>
prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?value ?valueLabel WHERE {
 ?item glo:subConceptOf itops:Software .
 { 
   ?item rdfs:label ?itemLabel.
   FILTER (CONTAINS(LCASE(?itemLabel), "adobe")) .
 } UNION {
   ?item glo:alias ?alias .
   FILTER (CONTAINS(LCASE(?alias), "adobe")) .
 }
 ?item itops:programming_language ?value .
 OPTIONAL { ?value rdfs:label ?valueLabel . }
}
```
---
#### List all properties in the IT Operations Ontology (datatype, object, and annotation)
```sparql
prefix glo: <http://www.ibm.com/GLO#>
prefix itops: <http://www.ibm.com/ITOPS#>
prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?property ?propertyLabel WHERE {
 {
     ?property rdfs:subPropertyOf glo:topObjectProperty .
 } UNION {
     ?property rdfs:subPropertyOf glo:topDatatypeProperty .
 } UNION {
     ?property rdfs:subPropertyOf glo:topAnnotationProperty .
 }
 ?property rdfs:label ?propertyLabel .
```
