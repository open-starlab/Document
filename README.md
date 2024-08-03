# Openstarlab Document
[![Documentation Status](https://readthedocs.org/projects/openstarlab/badge/?version=latest)](https://openstarlab.readthedocs.io/en/latest/?badge=latest)

## Document for the analysis platform

Step 1
```
cd build/html
```
Step 2
```
python -m http.server
```
Open a web browser and type http://localhost:8000 in the address bar. You should see the generated Sphinx documentation served as a website.

## Rebuild the doc
```
pip install -r doc/requirements.txt 
sphinx-autobuild source build/html
```
## To Update this doc
1. Clone this repo
2. Update the content in ./doc/source
3. Test it with rebuild the doc (section above) 
4. Update the version on ./doc/source/conf.py
4. Update this repo 
5. Check the document deployment on https://readthedocs.org/

