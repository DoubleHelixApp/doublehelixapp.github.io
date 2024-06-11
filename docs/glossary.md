# Glossary

This files contain a glossary of technical terms and concepts that are used in the documentation.

## Alignement

## File formats

An [aligned](#alignment) file can be stored in different formats described below:

Format | Content | Compressed | Description | Specification
-------|---------|------------|-------------|--------------
SAM    | Textual | No | Base file format for aligned read | [SAM format](https://samtools.github.io/hts-specs/)
BAM    | Binary  | No | Binary version of SAM | [BAM format](https://samtools.github.io/hts-specs/)
CRAM   | Binary  | Yes| Highly compressed version of BAM  | [CRAM format](https://samtools.github.io/hts-specs/)
FASTA  | Textual | No | For each [sequence](#sequence) contains a single letter representing the nucleotide at a specific position. | It doesn't have a formal specification, more information [here](https://en.wikipedia.org/wiki/FASTA_format)
GFF3    | Textual  | No | Annotation data   | [GFF3 format](https://github.com/The-Sequence-Ontology/Specifications/blob/master/gff3.md)
VCF     | Textual  | No | Variant data   |   | [VCF format](https://samtools.github.io/hts-specs/)
BCF     | Binary    | Yes (optional) | Variant data | [BCF format](https://samtools.github.io/hts-specs/)

*NOTE*: The reality is more nuanced than what described in this table, as a SAM file can also contain unaligned reads, CRAM files can store uncompressed data, and there are many more details that are not described here for the sake of brevity. In any case, the table above contain the most common usages of these files, you can find more information by looking at their respective specifications.

TBD: add unaligned formats. FASTQ, Textual, DNA sequences with quality scores, Yes, [FASTQ format](https://en.wikipedia.org/wiki/FASTQ_format)