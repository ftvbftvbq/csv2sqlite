#CSV to SQLite Importer

csv2sqlite is a command line application that can transform CSV documents into fully operational SQLite3 databases.

##Key features:

- Mapping file describing how each column is imported;
- Support for data transformations before importing cell;
- Generate tables with normalized data;
- Import results to existing databases;
    
##Planned features:

- Generate foreign keys for normalization tables;
- Generate primary keys automatically;
- The first row of the CSV file can contain the name of each column to be used in the database;
- Generate primary key for specified column
- Supported for data transformations after importing cell (DBMS);

##Mapping file:

Mapping files act like descriptors where each column can have their data type explicitly defined, or automatically assigned. Data can be transformed prior to being imported and even mapped to multiple columns;

##Example usages:

Import simple row data from CSV file and automatically generate primary keys for each record and transform names to uppercase

CSV file:

```csv
mary,23,f,mary@mary.com
john,34,m,john@gmail.com
```

Mapping file:

```json
{
    "table_name": "person",
    "mappings": [
        {
            "csv_index": 0,
            "column_name": "name",
            "transform": "to_upper"
        },
        {
            "csv_index": 3,
            "column_name": "email"
        },
        {
            "csv_index": 2,
            "column_name": "gender"
        },
        {
            "csv_index": 1,
            "column_name": "age"
        }
    ]
}
```

Invocation:

    csv2sqlite --input data.csv --output data.db --mapping map.json