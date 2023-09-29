# Testing Individual Python Wheel (.whl) Files with Snyk

## Description
The script below illustrates an approach for testing Python wheel files and their dependencies for open source vulnerabilities using Snyk.

To do this, the script first converts the wheel contents into a `requirements.txt` in a dedicated Python virtual environment and then uses the Snyk CLI to test the generated file.

## Example Script

```bash
#!/bin/bash
#
#
# Usage:
#     scriptname <path to whl file> <snyk test args>

# Notes:
#  * This script assumes the wheel file is available locally

# Create and activate the temporary virtual environment
#
python3 -m venv ./tmp_snyk_venv
source ./tmp_snyk_venv/bin/activate
#
# Install the whl
#
pip install $1
#
# Create the requirements.txt
#
pip freeze > ./requirements.txt
#
# Run the snyk test
#
shift
snyk test --file=./requirements.txt $@

#
# Deactivate and remove the virtual environment
#
deactivate
rm -fr ./tmp_snyk_venv
rm -f ./requirements.txt
#
#
```