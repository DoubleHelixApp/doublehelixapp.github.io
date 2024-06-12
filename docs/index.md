# Welcome to DoubleHelix

DoubleHelix is a tool designed for manipulating and extracting data from files representing whole-sequenced human genomes. It provides functionality to load and transform genomic data. DoubleHelix is heavily reliant on and provides a more user-friendly interface to a suite of existing tools called [samtools](https://samtools.github.io/).

### Launch
DoubleHelix runs on Windows, Linux, and MacOS. Follow the installation procedure below according to your OS.
The only currently supported way to install `DoubleHelix` is with a PyPI package.
This requires `python` and `pip` installed. If you think `python` is a snake, you should try the [pyinstaller](#pyinstaller-release) release. Note DoubleHelix is still in alpha state and many things are not working or they may break unexpectedly.

=== "Windows"
    ```batch
    python -m pip install doublehelix
    helix
    ```
=== "Debian-based distros"
    > WARNING:
    > DoubleHelix is not thoroughly tested on Linux. Please see the [troubleshooting](#troubleshooting) section.
    ```bash
    sudo apt install libqt6waylandclient6 samtools bcftools tabix -y
    python -m pip install doublehelix
    helix
    ```
=== "MacOS"
    > WARNING:
    > DoubleHelix is not thoroughly tested on MacOS. Please see the [troubleshooting](#troubleshooting) section.
    ```bash
    TBD
    python -m pip install doublehelix
    helix
    ```

#### PyInstaller release
A PyInstaller release is a single file that can be downloaded and executed to run DoubleHelix. 
It can be downloaded from this page: [windows](https://github.com/DoubleHelixApp/DoubleHelix/actions/workflows/python-pyinstaller-win.yml), [linux](https://github.com/DoubleHelixApp/DoubleHelix/actions/workflows/python-pyinstaller-linux.yml). To use them, simply download the file and open it.

Unless differently indicated, this is not a recommended way to run DoubleHelix for the time being. The build is disabled most of the time so you'll likely find an old version of DoubleHelix there. Also, it's less tested than the PyPI package. If you want to go ahead and try it anyway, see the [troubleshooting](#troubleshooting) section.

### Development
This section explains how to configure DoubleHelix for development.

_Note: The best experience for developing is with [VS Code](https://code.visualstudio.com/) as this project already contains sensible settings for VS code._

=== "Windows"
    ```batch
    git clone https://github.com/DoubleHelixApp/DoubleHelix
    cd DoubleHelix
    python -m venv .venv
    .venv\Scripts\activate
    python -m pip install -e .
    helix
    ```
=== "Debian-based distros"
    ```bash
    sudo apt install libqt6waylandclient6 samtools bcftools tabix -y
    git clone https://github.com/DoubleHelixApp/DoubleHelix
    cd DoubleHelix
    python -m venv .venv
    source ./.venv/bin/activate
    python -m pip install -e .
    helix
    ```
=== "MacOS"
    ```
    TBD.
    ```

#### pre-commit
This repository uses [pre-commit](https://pre-commit.com/#intro) to ensure linting, formatting, and isort are executed before committing.
Its usage is optional but highly recommended. To install:
```
python -m pip install pre-commit
pre-commit install
```

## Troubleshooting

Error | Description
------|------------
**Symbol lookup error** after launching DoubleHelix from the command line on Linux/WSL| It's likely you have an old version of Qt installed. On Debian-based distros, it's likely the version of `libqt6waylandclient6` or one of its dependencies is too old and the Python module for Qt is trying to fetch some symbols from it that were added in a subsequent version. You can try to run a `sudo apt update && sudo apt upgrade` but if that doesn't work unfortunately you need to upgrade the Qt version manually, use another distribution (or stick with the CLI once it is available).
**Something else does not work on Linux/DoubleHelix is not starting on Linux**| DoubleHelix is tested almost exclusively on Windows for the time being. On Windows, all the executables needed beside DoubleHelix are shipped with another PyPI package upon which DoubleHelix depends. Installing through `pip` is hence sufficient to get `DoubleHelix` working. On Linux `DoubleHelix` expects all the executables to be available under `PATH`. Consequently, some dependencies need to be installed manually. The installation section provides the dependencies list for Debian-based distros, on other distros the command may change. Fetching existing executables from `PATH` means DoubleHelix will have no control no control over the version of the dependencies. Ubuntu on WLS is using a fairly old build of samtools for example. This means some features (i.e., FASTA conversion) won't work. This will change in the future once DoubleHelix stops relying on distro executables but frankly, this is not a priority at the moment. You're anyway more than welcome to open an issue if something is not working correctly.
**Windows Defender is complaining a lot** when launching the pyinstaller distribution, potentially uploading the .exe to the cloud for virus scanning or straight up detecting the binary as malware| Windows Defender is not very happy with unsigned executables. You can rest assured that DoubleHelix does not contain any malware though. DoubleHelix is completely open-source and the way the pyinstaller build is made can be seen in these GitHub Actions: [Windows](https://github.com/DoubleHelixApp/DoubleHelix/blob/main/.github/workflows/python-pyinstaller-win.yml), [Linux](https://github.com/DoubleHelixApp/DoubleHelix/blob/main/.github/workflows/python-pyinstaller-linux.yml). One of the long-term goals is to get a certificate and start signing the binary but this won't happen anytime soon.

## FAQs

**Q: How does it differ from [WGSE](https://wgse.io)?**

A: In terms of features, DoubleHelix was inspired by WGSE but their similarities end here. DoubleHelix and WGSE are completely different products and they don't share any code. Here's a comparison table between these two software:

| Feature | DoubleHelix | WGSE |
|:---:|:---:|:---:|
| GUI | Tkinter | PyQtSide6 |
| Reference genome | Able to recognize more than 90 reference genomes. It can scale easily. | Supports a limited number. It cannot scale. |
| Progress bar | [Yes](advanced-topics.md#progress-bar) | No |
| HTML Export | Yes | No |
| CLI | Yes (partial) | No |
| Installation | PyPI package/PyInstaller, possibly a normal installer in the future | Batch/Bash |
| UnitTests | Yes, covering 29% of the software at the moment | No
| Automatic CrashReports | Yes (sentry) | No |
| CI | Yes (GitHub action) | No |

Despite increasing performances was not the goal of DoubleHelix, in a few benchmarks done by its author it seemed also faster than WGSE. Performances are not checked regularly and are vastly dependent on the performance of other tools upon which DoubleHelix is reliant, so maybe this is not the case anymore.

On the other side, DoubleHelix is less stable than WGSE as it's a younger product. Some features are still not yet fully implemented. 
DoubleHelix is also made with different goals. For example, there's no plan to add ancestry-related features in DoubleHelix itself. The long-term goal is to have a plug-in system that will allow third parties to develop and maintain certain features.