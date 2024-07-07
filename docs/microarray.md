# Microarray template format

Every microarray template file is made by three different sections:

1. A line containing metadata info for the file itself
2. (Optional) Several lines containing comments
3. Several lines containing IDs, Chromosome number, and position

## 1. Metadata

The metadata line is essentialy a JSON with the following field:

1. `input_format`: specify the format of the lines in the 3rd sections (e.g., `{id}\t{chromosome}\t{position}\n`)
2. `output_format`: specify how a microarray file will be generated starting by the template (e.g., `{id}\t{chromosome}\t{position}\t{result}\n`)
3. `file_extention`: specify the extension of the output file (e.g., `.txt`)
4. `undetermined`: specify what's the placeholder to indicate that a result is not available (e.g., `00`)

## 2. Comments

The comments are lines starting with a #. In the future it will be possible to use Jinjia variables here but at the moment this feature is not implemented.

## 3. Result entries

Each line here must match the format specified in `input_format`.