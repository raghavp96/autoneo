# Autoneo

Autoneo makes it easy to build complex graphs in Neo4j.

This tool allows users to represent their graph structure in a JSON schema, with the JSON containing
the properties to load into Neo4j but also how to extract the information from a data source.

### Using autoneo

#### Prequisites

Set up Neo4j to allow imports from external sources. This allows data from CSV files to be loaded into Neo4j (which is how this tool does its job!). 

1. Go to the config file for your instance. (You can find this location by starting neo4j from the command line. There will be a line of output showing the location of the `config` directory. The config file inside it. )
2. Comment out this line: dbms.directories.import=import (Add a #)
3. Uncomment this line: #dbms.security.allow_csv_import_from_file_urls=true (Remove the #)


#### Install autoneo

1. `pip install autoneo`


#### Using autoneo

##### In Code

You can use `autoneo` like:

```
from autoneo import builder

builder.build(
    "path/to/config.json", 
    "path/to/data_dir", 
    "path/to/query_dir", 
    "path/to/csv_dir")
```

See [config.json](https://github.com/raghavp96/autoneo/blob/master/tests/config.json) for an example of how to define a graph. Currently we support extraction from sqlite3 databases and CSV files. Support for other databases formats is on the way.

Data directory will contain `.db` files. Query dir will be where all scripts for retrieving data are placed. CSV dir is where you can drop a CSV for when you don't need a Database file/Query File. If you provide those, then a CSV will be generated by autoneo and placed in this directory.


### Working on the project

To build: `python setup.py sdist bdist_wheel`
To upload: `python -m twine upload dist/*` (Token name: pypi_all_purpose)
To run tests: `nosetests` (to run all tests)

