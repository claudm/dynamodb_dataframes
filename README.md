# dynamodb_dataframes
[![Build Status](https://travis-ci.org/mannharleen/dynamodb_dataframes.svg?branch=master)](https://travis-ci.org/mannharleen/dynamodb_dataframes)
[![Coverage Status](https://coveralls.io/repos/github/mannharleen/dynamodb_dataframes/badge.svg?branch=master)](https://coveralls.io/github/mannharleen/dynamodb_dataframes?branch=master)
[![Documentation Status](https://readthedocs.org/projects/dynamodb-dataframes/badge/?version=latest)](https://dynamodb-dataframes.readthedocs.io/en/latest/?badge=latest)
[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/mannharleen)

## Objective

To create an easy to use API for AWS dynamodb that will enable:
1. SQL command line for SQL/DML/DDL operations  
2. SQL API for all those operations, that will return a dataframe (pandas)

## Motivation

Two simple motivations:
1. Make the dynamodb API simpler by using SQL, DML and DDL statements
2. dynamodb doesn't allow joins and other complex transformations (sometimes this is required)

## Objective

1. Creating an API that returns the data in dynamodb as a pandas dataframe. Data transformation made easy!

## Installation

### From github

This is the recommended way (unless I decided to publish this package on pypi)
Simply run the following in the command/shell prompt
```sh
pip3 install git+https://github.com/claudm/dynamodb_dataframes.git boto3 pandas regex
```

## From local filesystem

This should be only used if you are not able to connect to github from the machine where you need to pip install

Download the required version file from https://github.com/claudm/dynamodb_dataframes/tree/master/dist and copy to the machine lets say on into the folder C:\dist\
Then run the following in the command/shell prompt
```sh
pip install dynamodb_dataframes --no-index --find-links file://C:\dist
```

## Usage

### Using the SQL API:

```python
from dynamodb_dataframes import dynamodb_sql_api
from dynamodb_dataframes import dynamodb_sql_api2
import logging

#-- using api1
dynamodb_sql_api.setup()                                #-- this will use default config, see below section on custom config
print (dynamodb_sql_api.sql("show tables"))
print (dynamodb_sql_api.sql("select * from table1ss"))  #-- prints the returned pandas dataframe

#-- using api2
print (dynamodb_sql_api2.sql("select * from table1ss", logging.INFO))      #-- prints the returned pandas dataframe and sets the logging level
```
For more examples visit https://github.com/claudm/dynamodb_dataframes/tree/master/examples

### Using the SQL prompt:

```sh
wget https://raw.githubusercontent.com/claudm/dynamodb_dataframes/master/dynamodb_dataframes/dynamodb_sql_api.py
$ python dynamodb_sql_api.py
sql> show tables;
sql> describe table1ss;
```

## Configuration for dynamodb server

1. For the SQL API, configuration can be made either via a config file or via passing parameters progrmatically
2. For the SQL prompt, configuration will be asked for. If the user presses enters, default values are taken

When initializing the SQL API, you can set the config as follows:
```python
dynamodb_sql_api.setup('/home/config.ini')              #-- if you want to specify location of config file
```

If no configuration is provided, the program defaults to point to local instance of dynamodb, i.e. using the following values:
```bash
[DEFAULT]
region_name = us-east-1
profile_name = default
```
