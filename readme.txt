avro-20180119/recon.avro is the final AVRO used for the LREC release.
The train.avro/test.avro are in train/test-20180119 folders. The Zip file corpus-for-lrec-20180119.zip contains these avros plus their JSON version.

Unclear: Are documents deduplicated (not just by id, by content) ?


Version 2:

Folder: smartdata-corpus-v2.0-20190802-avro
Preprocessing: SmartDataSsplitTokenize.scala with arguments "de /home/leonhard/Dokumente/code/dfki/corpora/smartdata-corpus/avro-20180119/recon.avro /home/leonhard/Dokumente/code/dfki/corpora/smartdata-corpus/smartdata-corpus-v2.0-20190802-avro/smartdata-corpus-complete.avro"
TrainDevTestSplit: DocumentTrainDevTestSplitJob  with arguments /home/leonhard/Dokumente/code/dfki/corpora/smartdata-corpus/smartdata-corpus-v2.0-20190802-avro/trainDevTestSplit-smartdatacorpus.properties

For Stanford Experiment/Model see /media/wde/leonhard/experiments_models/daystream_ner_201908/stanford

