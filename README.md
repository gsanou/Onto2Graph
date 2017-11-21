# Onto2Graph

Onto2Graph is a tool based on Java that can generate graphs in different formats from ontologies.
The tool is based on OWLAPI library to load the ontologies, and then, it enables to use different
reasoners to infer a graph from the ontology (ELK, HERMIT, STRUCTURAL REASONER AND SYNTACTIC REASONER).
Once the graph is built, different libraries have been integrated into the tool to transform it into various
formats such: RDFXML, GRAPHVIZ, FLATFILE and GRAPHML). The tool implements two different algorithms to carry
through with the conversion: A) without the transitive reduction in which relations inferred from transitive
object properties will be taken into account. B) with transitive reduction where relations inferred from transitive
object properties will not be considered.

# Dependencies

The working of the tool is based on the following libraries:

1. Elk-owlapi reasoner: This library contains the reasoner that is used to infer the classes in the ontology given.
2. HermiT: The other reasoner that has been included in the tool.
3. JGrapht: A graph library that is used to generate graphs from the ontology given.
4. OWLAPI-osgidistribution (version 4.0.2): Library used to manipulate ontologies.
5. Jena-Apache (version 3.0.0.2): Library used to generate the RDFXML Graph.

A pom.xml file is provided. This file contains in a more detailed way all
dependencies required to compile the application.

# Execution

The application does not have a GUI, it is a command line application. These are the parameters that Onto2Graph needs to run:
      
1. -ont: This parameter specifies the path where the ontology is located.
2. -out: It represents the output path where the files generated by the tool will be saved.
3. -r: The reasoner will be used to infer the ontology. Currently, these are the reasoners that have been included:
	3.1. ELK: Elk reasoner is the default option.
	3.2. HERMIT.
	3.3. STRUCTURAL_REASONER.
	3.4. SYNTACTIC_REASONER.

4. -f: This is an optional parameter and it should contain once of the different formatters that have included in the tool:
	4.1. JSONLD,
	4.2. RDFXML, GRAPHVIZ[DEFAULT].
	4.2. GRAPHVIZ [DEFAULT].
	4.3. OBOFLATFILE.
	4.4. GRAPHML.
	4.5. *: The "*" set that all formatters will be applied.
5. -eq: This parameter has to contain a boolean value (TRUE,FALSE[DEFAULT]). It aims at activate the equivalent classes
flag filter. If the flag is false, only the representative classes will be taken. On the contrary, if the flag is true,
representative and equivalent classes will be taken. different node will be added to the graph, else if the flag is false
then for each set of equivalent classes just one node will be created.
6. -op: It is an optional parameter and it represents a list of object properties that will be added to the graph.
The list of object properties should be formatted as array, here you can see an example: ["first_label","second_label",
"third_label"]. In order to include all object properties from the ontology given it is just needed to provide: [*] and
then all object properties from the ontology will be added.
7. -t: This parameter has to contain a boolean value (TRUE,FALSE[DEFAULT]). It aims to activates the transitive
reduction flag. If the flag is true, the transitivity reduction will be applied over the object properties selected
(DEFAULT=False).
8. -nt: This parameters specifies how many threads will be used during the inference process (DEFAULT=4) (Optional).

An example of Onto2Graph execution without object properties would be:

java -jar Onto2Graph-1.0.jar -ont GO_36.owl -out syntactic_reasoner_rdfxml -r SYNTACTIC_REASONER -f RDFXML -t false -nt 4

In this example we are using the following parameters:
-ont: In order to indicate the path where the ontology is located.
-out: The path where the graph will be serialized.
-r: In this example we are going to use the SYNTACTIC_REASONER.
-f: The formatter that will be applied over the ontology file will be RDFXML. So, as a result the tool will provide a
graph in RDFXML format.
-t: In this example, we are not going to apply transitive reduction.
-nt: The number of threads to use will be 4. 

An other example including all objects properties of the ontology would be:

java -jar Onto2Graph-1.0.jar -ont GO_36.owl -out go_elk_rdfxml -r ELK -f RDFXML -eq true -op [*] -t true -nt 4

Unlike the early example, as you can see, here we have object properties. So, in this case the parameters are: 
-ont: The path of the ontology that will be transformed into a graph.
-out: The output path.
-r: We are going to use ELK reasoner.
-f: The formatter that will be applied, in this example will be RDFXML.
-eq: We will include the equivalent classes.
-op: This parameter contains [*] which means all the object properties of the ontology will be included to the parse
process of the ontology.
-t: In this example we are going to apply the transitive reduction over all properties.
-nt: The number of threads to use will be 4.

# Compile and Execute

To use Onto2Graph, there are two ways:
- You can use the jar available in folder target
- You can compile and package the app by yourself using the following Maven commands:
	- mvn clean
	- mvn compile
	- mvn package
 
# License

Copyright 2014 Miguel Ángel Rodríguez-García (miguel.rodriguezgarcia@kaust.edu.sa).

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

