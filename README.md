# Openstarlab Document


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

## Alternatively 
```
sphinx-autobuild source build/html
```