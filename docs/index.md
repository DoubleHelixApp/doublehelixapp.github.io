# Welcome to DoubleHelix

DoubleHelix is a tool designed for manipulating and extracting data from files representing whole-sequenced human genomes. It provides functionality to load, parse, filter, transform, and analyze genomic data. The name WGSE is an acronym that stands for "_Whole Genome Sequencing Extract_". 

DoubleHelix is an attempt to re-engineering an existing tool called [WGSE](https://wgse.io). See the [FAQs](#faqs) to see how they differs. WGSE and DoubleHelix are heavily relying on a suite of existing tools called [samtools](https://samtools.github.io/) but they provide a more user-friendly interface.

### Launch
WGSE runs on Windows and Linux. It should work also on MacOS but was never tested on it. Follow the installation procedure below according to your OS.
The only currently supported way to install `DoubleHelix` is with a pypi package.
This require python and pip installed. Note DoubleHelix is still in alpha state and many things are not working or they may broke unexpectedly.

=== "Windows"
    ```batch
    python -m pip install doublehelix
    wgse
    ```
=== "Debian-based distros"
    **IMPORTANT**: DoubleHelix is not thoroughly tested on Linux. Please see the [troubleshooting](#troubleshooting) section.
    ```bash
    sudo apt install libqt6waylandclient6 samtools bcftools -y
    python -m pip install doublehelix
    wgse
    ```

#### PyInstaller release
There's a PyInstaller build the is occasionally executed to build a single-file binary.
The artifacts are here: [windows](https://github.com/DoubleHelixApp/DoubleHelix/actions/workflows/python-pyinstaller-win.yml), [linux](https://github.com/DoubleHelixApp/DoubleHelix/actions/workflows/python-pyinstaller-linux.yml). To use them, simply download the file and open it.

Unless differently indicated, this is not a recommended way to run DoubleHelix for the time being: first of all, the build is disabled most of the time so you'll likely find an old version of DoubleHelix there. Second, it's less tested than the PyPI package. If you want to go ahead and try it anyway, see the [troubleshooting](#troubleshooting) section.

### Development
This section explain how to configure DoubleHelix for development.

_Note: The best experience for developing is with [VS Code](https://code.visualstudio.com/) as this project already contains sensible settings for VS code._

=== "Windows"
    ```batch
    git clone https://github.com/DoubleHelixApp/DoubleHelix
    cd DoubleHelix
    python -m venv .venv
    .venv\Scripts\activate
    python -m pip install -e .
    wgse
    ```
=== "Debian based distros"
    ```bash
    sudo apt install libqt6waylandclient6 samtools bcftools -y
    git clone https://github.com/DoubleHelixApp/DoubleHelix
    cd DoubleHelix
    python -m venv .venv
    source ./.venv/bin/activate
    python -m pip install -e .
    wgse
    ```

#### pre-commit
This repository uses [pre-commit](https://pre-commit.com/#intro) to ensure linting, formatting, and isort are executed before commit.
Its usage is optional but highly recommended. To install:
```
python -m pip install pre-commit
pre-commit install
```

## Troubleshooting

Error | Description
------|------------
**Symbol lookup error** after launching WGSE from command line on Linux/WSL| It's likely you have an old version of Qt installed. On Debian based distro it's likely the version of `libqt6waylandclient6` or one of its dependencies is too old and the python module for Qt is trying to fetch some symbols from it that were added in a subsequent version. You can try to run a `sudo apt update && sudo apt upgrade` but if that doesn't work unfortunately you need to upgrade the Qt version manually, use another distribution (or stick with the CLI once it will be available).
**Something else does not work on Linux/DoubleHelix is not starting on Linux**| DoubleHelix is tested almost exclusively on Windows for the time being. On Windows all the executables needed beside DoubleHelix are shipped with another PyPI package upon which DoubleHelix depends. Installing through `pip` is hence sufficient to get `DoubleHelix` working. On Linux `DoubleHelix` expects all the executables to be available under `PATH`. Consequently there are dependencies that need to be installed manually. The installation section provide the dependencies list for Debian-based distros, on other distros the command may change. Fetching existing executables from `PATH` means DoubleHelix will have no control no control over the version of the dependencies. Ubuntu on WLS is using a fairly old build of samtools for example. This means some feature (i.e., FASTA conversion) won't work. This will change in the future once DoubleHelix will stop relying on distro executables but frankly this is not a priority at the moment. You're anyway more than welcome to open an issue if something is not working correctly.
**Windows defender is complaining a lot** when launching the pyinstaller distribution, potentially uploading the .exe to the cloud for virus scanning or straight up detecting the binary as a malware| Windows defender is not very happy with unsigned executables. You can rest assured DoubleHelix do not contain any malware though. DoubleHelix is completely open-source and the way the pyinstaller build is made can be seen in these GitHub Actions: [Windows](https://github.com/DoubleHelixApp/DoubleHelix/blob/main/.github/workflows/python-pyinstaller-win.yml), [Linux](https://github.com/DoubleHelixApp/DoubleHelix/blob/main/.github/workflows/python-pyinstaller-linux.yml). One of the long-term goal is to get a certificate and start signing the binary but this won't happen anytime soon.


## Configuration

WGSE utilizes two configuration files to define its operational settings. These files provide a way to customize the software's behavior without modifying the code. The files are loaded in a specific order, allowing for overrides.

### File Priority

WGSE prioritizes configuration settings based on the order the files are loaded:

- **Global Configuration File** (configuration/main.ini): The first file loaded is located in a subdirectory of the WGSE path. This file is named wgse.ini by default. Settings defined here serve as the base configuration. This file is mostly useful when developing to have everything in the same folder.
- **Local Configuration File** (~/.wgse/main.ini): The second file loaded resides in the user's home directory within a folder named .wgse. Settings defined in this file can override the settings from the global configuration file.

### Configuration file sample

```ini
[general]
last_path = .

[external]
root = 3rd_party
threads = 24

[repository]
repository = repository
metadata = repository\metadata
temporary = repository\temp

[alignment_stats]
skip = 40000
samples = 20000
```

## FAQs

**Q: How does it differs from the original WGSE?**

A: DoubleHelix is a re-engineering of WGSE with these improvements:

- A new GUI (based on pyqtside)
- An entirely re-written procedure to identify reference genomes that supports more than 90 reference genomes
- A progress bar (not an easy task to implement one, see [here](advanced-topics.md) for the technical details)
- A custom HTML export of file information

It has also some non-visible modification:

- It has many unit-tests
- It has a completely automated crash-report