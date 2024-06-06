# User guide

This page explains the main window of DoubleHelix. Will add some screenshot when the UI will be more mature.

## Main UI

Once opened, you can drag the file you want to open into the UI. A table with basic information about the file will open.


Field|Description
-----|-----------
Directory|Directory that contains the file that is loaded in the app. Double click the field to open the directory in a file manager (if available).
File|Name of the file loaded
File Type|See [file type](#file-type)
Reference|See [reference](#reference). Double click to open a window containing information about similar or identical reference genomes.
Gender|Biological gender of the person who sampled the DNA contained in the loaded file. The field it's available only if index stats are available.
Sorted|Indicates whether the file is sorted (add explanation here)
Indexed|Indicates whether the loaded file has an index file (a .bai or .crai file depending on the format)
Mitochondrial DNA Model|Gapped reference genomes contains are based on known models for the mitochondrial DNA. If the model of the reference associated with the loaded file is known it will be specified here.
Header|Open a window containing information on the header (see [header](#header))
Alignment stats|Open a window containing information on alignment stats (see [alignemnt stats](#alignment-stats))

# Reference

The reference field can have these values:

- Available: DoubleHelix is able to recognize the reference genome used to align the loaded file and the file is on disk
- Downloadable: DoubleHelix is able to recognize the reference genome used to align the file but the file is not on disk. DoubleHelix know its URL and the file can be downloaded.
- Unknown: There is one or more sequences that DoubleHelix is not able to recognize. There's no way for DoubleHelix to obtain a reference genome and the user needs to tell DoubleHelix how to find it. See [ingestion](#ingestion)
- Buildable: DoubleHelix is not able to find a single file that is a perfect match with the references that was used to align the loaded file, but DoubleHelix knows multiple files that can be used together to build a reference.

The reference window can be opened by clicking on the "Reference" field in the main UI. It contains information about the reference genome used to align the file (if it is available) or information about similar reference genomes.

Every column in the reference window are related to a specific reference that has some information matching with the reference used to align the file.

## Header

Header window can be opened by clicking on the "Header" field in the Main UI. It contains a 1:1 representation of the information contained in the header of the loaded file.

### Sequences
Field|Description
-----|-----------
Fillme|Fillme

### Programs

### Read groups

### Comments

