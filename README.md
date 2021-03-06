NosFinancesLocales scraper
=========

This project aims at scraping financial data of cities (="communes"), EPCI
(group of cities Cf. [wikipedia](http://fr.wikipedia.org/wiki/%C3%89tablissement_public_de_coop%C3%A9ration_intercommunale)), department and regions from the website
http://www.collectivites-locales.gouv.fr/.

This project uses [scrapy](https://github.com/scrapy/scrapy) to crawl and scrape data.

All the data scraped for the regions is committed as an example here:
 * with variable names as header: [scraped_data/region_all.csv](scraped_data/region_all.csv)
 * with french header: [nosdonnees/region_all.csv](nosdonnees/region_all.csv)


Usage
=====

To crawl data of a give zone type (***city***, ***epci***, ***department*** or ***region***) on a given fiscal
year YYYY, run in the root dir:

`scrapy crawl localfinance -o scraped_data_dir/zonetype_YYYY.json -t jsonlines -a year=YYYY -a zone_type=zonetype`

To scrape data for all available years for a given zone type:

`source bin/crawl_all_years.sh zonetype`

To generate a csv file with all data for a given zonetype and with french
header, run:

`python bin/make_csv.py zonetype`

This command will generate a file in nosdonnees/zonetype_all.csv which you can then
upload on [nosdonnees.fr](http://www.nosdonnees.fr) website.

The last uploaded dataset is currently available [here](http://www.nosdonnees.fr/dataset/donnees-comptables-et-fiscales-des-collectivites-locales).



Requirements
===========
[See requirements.txt file.](requirements.txt)


Tests
=====

## Run all
`unit2 discover`

## Run one test
`python test/test_commune_parsing.py Commune2009ParsingTestCase`

## Download an html file to add a new test
Here are some examples to download html pages for region, department, epci and city at year 2014 :
`curl -X POST -d "REG=025&EXERCICE=2014" http://alize2.finances.gouv.fr/regions/detail.php > test/data/region_2014_account.html`

`curl -X POST -d "DEP=002&EXERCICE=2014" http://alize2.finances.gouv.fr/departements/detail.php > test/data/department_2014_account.html`

`curl -X POST -d "NOMDEP=ALLIER&ICOM=008&DEP=003&TYPE=BPS&PARAM=0&EXERCICE=2014&SIREN=240300418" http://alize2.finances.gouv.fr/communes/eneuro/detail_gfp.php > test/data/epci_2014_account.html`

`curl -X POST -d "ICOM=234&DEP=045&TYPE=BPS&PARAM=0&EXERCICE=2014" http://alize2.finances.gouv.fr/communes/eneuro/detail.php > test/data/commune_2014_account.html`


TODO
====
 * Add some docs, especially indicate the mapping between variable names and
   fields in html pages.


