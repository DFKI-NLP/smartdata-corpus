# DFKI SmartData Corpus

This repository contains the DFKI SmartData Corpus, a dataset of 2598 German-language documents which has been annotated with fine-grained geo-entities, such as _streets_, _stops_ and _routes_, as well as standard named entity types. It has also been annotated with a set of 15 traffic- and industry-related n-ary relations and events, such as _Accidents_, _Traffic jams_, _Acquisitions_, and _Strikes_. The corpus consists of newswire texts, Twitter messages, and traffic reports from radio stations, police and railway companies. It allows for training and evaluating both named entity recognition algorithms that aim for fine-grained typing of geo-entities, as well as n-ary relation extraction systems.

You can find the full description of the corpus here: [http://www.dfki.de/lt/publication_show.php?id=9427](http://www.dfki.de/lt/publication_show.php?id=9427)

The corpus is provided in two formats - AVRO and JSON, using the train/test split described in the paper. For details on the schema used for storing annotations, see below.

 * [SmartData Corpus (AVRO+JSON)](v1.0-20180119/)

## Use
The DFKI SmartData Corpus is released as [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/). If you use this data, you should cite the accompanying paper:

_A German Corpus for Fine-Grained Named Entity Recognition and Relation Extraction of Traffic and Industry Events. Martin Schiersch, Veselina Mironova, Maximilian Schmitt, Philippe Thomas, Aleksandra Gabryszak, Leonhard Hennig. Proceedings of LREC, 2018._ [(bib)](paper.bib) [(pdf)](https://www.dfki.de/web/forschung/projekte-publikationen/publikationen/publikation/9427/)


## Format

The corpus consists of Documents which store the original text and all annotations, according to the following AVRO schema:

 * [document.avsc](document.avsc)

You can use the following JAVA tools to read the AVRO version of the corpus:

 * [Corpus Reader Tools](sdw-tools-1.0-SNAPSHOT.jar)

To read the corpus, use the following code snippet:

   ```java
   File inputFile = new File("train.avro");
   DataFileReader<Document> reader = AvroUtils.createReader(inputFile);
   while (reader.hasNext()) {
      Document doc = reader.next();
      // do something
   }

   ```

Each document contains a list of ConceptMentions, which correspond to Named Entities and other typed concepts (e.g. trigger phrases):

   ```java
   for (ConceptMention c : doc.getConceptMentions()) {
       String nerTag = c.getType();
       String value = c.getNormalizedValue();
       int start = c.getSpan().getStart();
       int end = c.getSpan().getEnd();
       String originalText = doc.getText().substring(start, end);
       // etc ...
   }
   ```

Similarly, you can retrieve RelationMentions:

   ```java
   for (RelationMention r : doc.getRelationMentions()) {
       String relationType = c.getName();
       int start = c.getSpan().getStart();
       int end = c.getSpan().getEnd();
       String originalText = doc.getText().substring(start, end);
       for (RelationArgument arg : r.getRelationArguments()) {
           String role = arg.getRole();
           ConceptMention c = arg.getConceptMention();
           // ...
       }
       // ...
   }
   ```

ConceptMentions and RelationMentions are stored at the document level, and for each sentence as well. You can access a sentence's list of RelationMentions using:

   ```java
   for (Sentence s : doc.getSentences()) {
       List<RelationMention> relationMentions = s.getRelationMentions();
       // ...
   }
   ```



## Annotation Guidelines

[SmartData Corpus Annotation Guidelines v1.0 (Feb 2018)](downloads/SmartData_Corpus_Annotation_Guidelines_Feb_2018_v1.0.pdf)
