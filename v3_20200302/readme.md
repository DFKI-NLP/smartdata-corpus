# Align concepts to tokens

Running de.dfki.lt.spree.daystream.ConceptToTokenAligner:

`java -cp <tap-experiments.jar> de.dfki.lt.spree.daystream.ConceptToTokenAligner v2_20190802 v3_20200302`

Process output:
Input documents: 2436
Input documents with relations: 955
Input relations: 1341

Documents with mismatch: 244
Documents with mismatch and relations: 123
Mismatched relations: 194

Fixed documents: 190
Removed documents: 54

Output documents: 2382
Output documents with relations: 931
Output relations: 1301


# Remove duplicate documents

`java -cp <tap-experiments.jar> de.dfki.lt.spree.daystream.DatasetDeduplication v3_20200302 v3_20200302`

Process output:
Read [1910] docs from [smartdata-corpus-v3.0-20200302]
Wrote [1861] docs to [smartdata-corpus-v3.0-20200302/train/train.avro]
Found [22] duplicates by id
Found [27] duplicates by text signature

Read [236] docs from [smartdata-corpus-v3.0-20200302]
Wrote [228] docs to [smartdata-corpus-v3.0-20200302/dev/dev.avro]
Found [5] duplicates by id
Found [3] duplicates by text signature

Read [236] docs from [smartdata-corpus-v3.0-20200302]
Wrote [230] docs to [smartdata-corpus-v3.0-20200302/test/test.avro]
Found [3] duplicates by id
Found [3] duplicates by text signature

# Add raw content

`java -cp <tap-experiments.jar> de.dfki.lt.spree.daystream.DatasetMergeRawIntoV3 v3_20200302 raw_20200302 v3_20200302`

Train: Replaced raw content in [1303] docs
Dev: Replaced raw content in [145] docs
Test: Replaced raw content in [164] docs

# Fix "end_loc" argument role errors

`java -cp <tap-experiments.jar> de.dfki.lt.spree.daystream.FixArgumentRoleErrors v3.0-20200302 smartdata-corpus-v3.0-20200302`

Train: applied 106 fixes (91 docs), issued 85 checks

Dev: applied 16 fixes (15 docs), issued 8 checks

Test: applied 8 fixes (8 docs), issued 11 checks