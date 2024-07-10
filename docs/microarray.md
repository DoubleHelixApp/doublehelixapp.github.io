# Microarray template format

Every microarray template file is made by three different sections:

1. A line that starts in `##` containing metadata info for the file itself
2. (Optional) Several lines containing comments starting in `#`
3. (Optional) Lines that will be skipped
3. Several lines containing the actual entries of the file

## 1. Metadata

The metadata line is essentialy a JSON with the following field:

1. `input_format`: specify the format of the lines in the 3rd sections (e.g., `{id}\t{chromosome}\t{position}\n`)
2. `output_format`: specify how a microarray file will be generated starting by the template (e.g., `{id}\t{chromosome}\t{position}\t{result}\n`)
3. `file_extention`: specify the extension of the output file (e.g., `.txt`)
4. `undetermined`: specify what's the placeholder to indicate that a result is not available (e.g., `00`)
5. `skip`: how many lines to skip after the header

## 2. Comments

The comments are lines starting with a #. In the future it will be possible to use Jinjia variables here but at the moment this feature is not implemented.

## 3. Result entries

Each line here must match the format specified in `input_format`.

## Example

Putting all together, this is an example of a valid template file:
```
## {"input_format":"{id}\t{chromosome}\t{position}\n", "output_format":"{id}\t{chromosome}\t{position}\t{result}\n", "file_extension":".txt", "undetermined":"--", "skip":1}
# This is a comment
rsid	chromosome	position	genotype
rs00001 chr1    1
```

Using a VCF file to populate a microarray file with this template will produce a file that can be like this as it matches the `output_format` specified above:
```
# This is a comment
rsid	chromosome	position	genotype
rs00001 chr1    1   AA
```