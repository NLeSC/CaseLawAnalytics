# CaseLawAnalytics
This repository contains code for the case law query app: an application to query Dutch law cases and extract a network to use in the [case law visualization app](https://github.com/NLeSC/case-law-app).

It includes code for setting up a blazegraph instance with "Hoge Raad" (high court) cases from [Rechtspraak.nl](https://www.rechtspraak.nl). This is not a requirement for a working query app.

This code is still under development.

Prerequisites:
* Python 3

Install the python requirents with `pip install -r requirements.txt`.


## The query app
First, clone the repository and run in the root of the repository:

`pip install .`

To run the query app:

`export FLASK_APP=blazegraph_querier/main.py`

and run the app:

`flask run`

To run tests:

`pytest test/`

## Blazegraph
Prerequisites: 
* Java 7

First, download the [Blazegraph executable jar](http://sourceforge.net/projects/bigdata/files/bigdata/2.1.4/blazegraph.jar/).

Modify the property `com.bigdata.journal.AbstractJournal.file` in the file `[CaseLawAnalytics repository]/blazegraph/RWStore.properties` to indicate where Blazegraph should store the .jnl file containing the data.
Then, run blazegraph with the properties file included in this repository:

`java -server -Xmx4g -Dbigdata.propertyFile=<path_to_repo>/blazegraph/RWStore.properties -jar blazegraph.jar `


### Load data into Blazegraph
The code for parsing the data from rechtspraak.nl and loading it into blazegraph can be found in `rechtspraak_query_app.parser`. Run the script `scripts/populate_blazegraph` to store all 'Hoge Raad' cases in Blazegraph.

To not overload the rechtspraak.nl server, it is best to first download the [complete collection of rechtspraak.nl](http://static.rechtspraak.nl/PI/OpenDataUitspraken.zip). 
