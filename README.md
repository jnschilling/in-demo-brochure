# in-demo-brochure
Demo brochure edition for AIS equipment for the use of Skippers :anchor:

# Author of the electronic content ready for sphinx
Jean-Noël Schilling
# Editors of the original brochure 
VTT Expert Group | Authors: Annick Javor, Stefan Bober, Piet Creemers, Jeffrey van Gils, Wim van der Heijden
Contact: website: http://www.ris.eu/expert_groups/vtt, e-mail vtt@ris.eu

# Link to the pdf brochure (2013):

* :uk: [EN-Leaflet operational use of Inland AIS(pdf)](http://www.ris.eu/docs/File/348/leaflet_operational_use_of_inland_ais%20_ed2013_vtteg_2013%20en.pdf)
* :fr: [FR-leaflet utilisation d'appareils AIS intérieur](http://www.ris.eu/docs/File/348/leaflet_utilisation_d_appareils_ais_interieur_edition_2013_fr.pdf)
* [NL-leaflet praktijkgids inland ais](http://www.ris.eu/docs/File/348/leaflet_praktijkgids_inland_ais__edition_2013_nl.pdf)
* :de: [DE-leitfaden zur Nutzung von inland AIS](http://www.ris.eu/docs/File/348/leitfaden_zur_nutzung_von_inland_ais_edition_2013_de.pdf)
* [HU-A belvízi közlekedés AIS üzemeltetési felhasználása](http://www.ris.eu/docs/File/348/leaflet_operational_use_of_inland_ais__edition_hu.pdf)

# Internationalization : how to update the translations

Following the [Sphinx documentation](http://www.sphinx-doc.org/en/master/usage/advanced/intl.html)

## Install [sphinx-intl](https://pypi.org/project/sphinx-intl/)
```python
pip install sphinx-intl
locale_dirs = ['locale/']   # path is example but recommended.
gettext_compact = False     # optional.
```
## Extract translatable messages into pot files.
```python
make gettext
```

## Until now the e-brochure is translated from the english to French, Dutch, Germann and Hungarian  
In case new languages would be added in the future the `conf.py` file needs to be updated accordingly:
```python
language = ['en', 'fr', 'de', 'nl', 'hu'] 
```

## Generate po files in french / german / dutch and hungarian
```python
sphinx-intl update -p _build/gettext -l fr -l de -l nl -l hu
```
Once completed, the generated po files will be placed in the below directories:

* ./locale/fr/LC_MESSAGES/
* ./locale/de/LC_MESSAGES/
* ./locale/nl/LC_MESSAGES/
* ./locale/hu/LC_MESSAGES/

## After translation, it requires to build the translated html (here for french language)
```python
make -e SPHINXOPTS="-D language='fr'" html
```
OR For Windows cmd.exe, run:
```cmd
set SPHINXOPTS=-D language=fr
.\make.bat html
```
Then the default language needs to be updated back to English
```windows
set SPHINXOPTS=-D language=en
.\make.bat html
```
## In case the e-brochure is updated, the translation needs to be updated accordingly
Update your po files by new pot files
If a document is updated, it is necessary to generate updated pot files and to apply differences to translated po files. In order to apply the updates from a pot file to the po file, use the sphinx-intl update command.

```python
make gettext #getting the updated text
sphinx-intl update -p _build/gettext -l fr -l de -l nl -l hu #apply the text into the translations
sphinx-intl update -p locale #creating the po file 
```