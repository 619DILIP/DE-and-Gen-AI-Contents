## Description 

- Hadoop supports 7 types of file formats: 
  - Text files/ CSV files
  - JSON files
  - Avro files
  - RC files
  - ORC files
  - Parquet files
  - Sequence files

**Text/CSV File Format:**

- Text files or CSV files are the most common files used by big data developers for storing text based inputs and comma seperated inputs. But these files do not support block compression and thus the read operation in CSV files are slower than other files formats. These files are recommended for data storage when we have data of less size. From excel it is easy to convert to CSV file format but all the data are stored without any formula, macro, etc that were applied to excel data.  

- For Example: 
```csv
Id,Name,Marks,Subjects 
100,henry,77.7,history
101,mark,66.6,physics
102,jacks,88.8,science
```

**JSON File Format:**

- JSON file stores the data in key value pairs and are human readable like text files. Here each key is a coulmn name which stores the value and each key value is seperated by colon(:). JSON files are good alternative for XML and are used for transferring data over the network. 

- For Example: 

```json
{[
{
    "Id" : 100
    "Name" : "Henry"
    "Marks" : 77.7
    "Subjects" : "History"
},
{
    "Id" : 101
    "Name" : "Marks"
    "Marks" : 66.6
    "Subjects" : "Physics"
}
]}

```


**Avro File Format:**

- Avro stores the data in json like format with the schema attached to it. The data and schema are stored in the same file. The Avro files are stored as a serialized binary file which helps in reducing the storage space as well as it is easy to transfer these files over the network. This format is considered the best format for storing large data in hadoop. 

- For Example: 
```json

{
  "type" : "record",
  "name" : "user",
  "namespace" : "my.example",
  "fields" : [
    {
      "name" : "username",
      "type" : "string",
      "default" : "NONE"
    }
  ]
}

```

**Sequence File Format:**

- Sequence files are the flat files which stores the data in binary key-value pairs. MapReduce uses this file to store input/output data. Internally all the mappers stores their intermediate data output using sequence file. 


**RC File Format:** 

- It was the first columnar file supported in hadoop. It has high compression rate and used for fast querying on multiple rows at a time. RC files store the columns of a table into records in columnar fashion. Data cannot be loaded into RC files directly, first it loaded into table and from table we need to overwrite it into RC files. 

![RC](Images/RCFile.PNG)

**ORC File Format:** 

- This file format is an optimized version of RC files where it reduces the original RC file size up to 75 percent. This results in fast data processing speed than other text files sequence files or RC files. Same like RC files, we cannot load data directly into ORC files. 

![ORC](Images/ORCFile.PNG)

**Parquet File Format:**

- It is a column oriented file just like ORC files but it stores the metadata and actual data together in the same file like avro files. It stores the data in advance binary format which helps in effective querying and retrieval of records. This file format is used widely in analytics. 

![Parquet](Images/ParquetFile.PNG)