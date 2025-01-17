# NeXus development tools

The NeXus development tools are used to validate NeXus class definitions
and generate all files needed for documentation building with sphinx.

## Quick reference

Install all requirements

```bash
python3 -m pip install -r requirements.txt
```

Run all tests

```bash
pytest dev_tools
```

Generate the build files

```bash
python3 -m dev_tools impatient --prepare
python3 -m dev_tools manual --prepare
```

Build the PDF manuals

```bash
sphinx-build -M latexpdf build/impatient-guide/ build/impatient-guide/build
cp build/impatient-guide/build/latex/NXImpatient.pdf build/manual/source/_static/NXImpatient.pdf

sphinx-build -M latexpdf build/manual/source/ build/manual/build
cp build/manual/build/latex/nexus.pdf build/manual/source/_static/NeXusManual.pdf
```

Build the HTML manuals

```bash
sphinx-build -b html -W build/impatient-guide/ build/impatient-guide/build/html
sphinx-build -b html -W build/manual/source/ build/manual/build/html
```

Auto-formatting and syntax checking to the developer tools themselves

```bash
black dev_tools
isort dev_tools
flake8 dev_tools
```

## Prepare environment (optional)

Create a fresh python environment

```bash
python3 -m venv nexusenv
```

Activate the environment on Linux or MacOS

```bash
source nexusenv/bin/activate
```

Activate the environment on Windows

```bash
nexusenv\Scripts\activate.bat
```

## Command line interface

```bash
python3 -m dev_tools --help
```

### Single NeXus class definition

This subcommand provides syntax checking and documentation building
(print, save and diff) for a single NeXus class definition

```bash
python3 -m dev_tools nxclass --help
```

For example the difference between the existing documentation of
a NeXus class definition and the generated documentation

```bash
python3 -m dev_tools nxclass nxaperture --diff
--- build

+++ source

@@ -1,4 +1,4 @@

-.. auto-generated by script ../../../../utils/nxdl2rst.py from the NXDL source NXaperture.nxdl.xml

+.. auto-generated by dev_tools.docs.rst from the NXDL source base_classes/NXaperture.nxdl.xml
```
