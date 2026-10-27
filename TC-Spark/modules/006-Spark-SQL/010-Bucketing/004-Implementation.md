# Implementation 

### create a bucketed table:

        df.write\
            .bucketBy(16, 'key') \
            .sortBy('value') \
            .saveAsTable('bucketed', format='parquet')


### How to make the data bucketed

In Spark API we can be used a function bucketBy.

        (
        df.write
        .mode(saving_mode)  # append/overwrite
        .bucketBy(n, field1, field2,field3,field4, ...)
        .sortBy(field1, field2, field3,field4, ...)
        .option("path", output_path)
        .saveAsTable(table_name)
        )