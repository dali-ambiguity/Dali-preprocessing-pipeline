# DALI PIPELINE

This is the pre-processing pipeline for Dali (Disagreements and Language Interpretation)
project. The tool contains a pre-processing pipeline and a converter developed at Queen 
Mary University of London for the Dali project. 

## Pre-processing Pipeline

The pipeline takes a Gutenberg/Wikipedia documents as input and processes the documents
with a sentence spliter, a tokenizer, a part-of-speech tagger, a dependency parser and 
a mention extractor. Then it outputs the processed document into supported format (Masxml, 
MMAX, SGF, CONLL12 and Dali). For sentence spliter and tokenizer we used Stanford 
pipeline, for part-of-speech it depends on the parser you choose, if Mate parser is used 
then the PoS is generated by the parser, or if you use Dozat parser, the PoS is annotated 
by the Stanford tagger.

For parsers, the Mate parser is fully included in the dalipipeline-all-inclusive.jar pretrained models can also be downloaded from [this link](https://drive.google.com/file/d/1LZJSKt8Tgkzclv_27jjOdtqAY83naeRw/view?usp=sharing). If you'd like to use Dozat parser, please follow the instructions of [this link](https://github.com/tdozat/Parser-v1) and download the model and the word embeddings. Please test that parser first to make sure it works.

Here is the usage of the pipeline:

Useage: java -Xmx5g -cp dalipipeline.jar dali.main.Pipeline [Options]

| Options | Descriptions |Default|
| :--- | :--- | :---|
| --help,-h | Help ||
| -g,-w | The type of the input document, -g: Gutenberg; -w: Wikipedia; |-g |
| -mate,-dozat | The parser you would like to use for parsing, -mate: Bohnet and Nivre (2012) -dozat: Dozat and Manning (2016); | -mate|
|-startFile|If you use the Dozat parser, you could specify the location of the main file; |DozatParser/P27/network.py|
|-input <dir>|The directory that contains the documents to be processed; |input/|
|-output <dir>	|The directory to output the processed documents; |output/| 
|-tmodel <file>	|The location of the model for part-of-speech; |models/english-bidirectional-distsim.tagger| 
|-pmodel <dir> |The location of the parsing model of the Mate parser or (-save_dir) of the Dozat parser; |models/chen-indomain-mate-Baseline-rescore-model-joint|
|-xsl <file> |The location of the xsl file required by the sgf converter; |models/MASXML2SGF.xsl|
|-dali -masxml -sgf -conll -mmax		|The output format of the documents; |-dali-masxml-sgf|


## Converter

The converter is able to convert between different output format supported by this tool.
Currently the converter support Dali (a binary file generated by the Dali pipeline), 
Masxml, CoNLL 2012, MMAX and SGF (output only) format.

Here is the usage of the converter:

Useage: java -cp dalipipeline.jar dali.main.Converter [Options]

| Options | Descriptions |Default|
| :--- | :--- | :---|
|--help, -h|Help||
|-inFormat [dali or masxml or conll or mmax]|The input file format;| dali|
|-input <dir>	|The directory that contains the documents to be converted; |input/|  
|-output <dir>|The directory to output the converted documents; |output/|
|-xsl <file> 	|The location of the xsl file required by the sgf converter; |models/MASXML2SGF.xsl|
|-dali -masxml -sgf -conll -mmax|The output format of the documents; |-dali-masxml-sgf|

