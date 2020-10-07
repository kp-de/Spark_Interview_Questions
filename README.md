# Spark Interview Questions

### 1. How will you parse a file with a date field which has multiple date formats? E.g. some records are in MM-DD-YYYY format, some are in YY-MM-DD, some are in YYYY-MM-DD format.

Ans: Scan the file multiple times, parse the date format with one format at a time. In each run, filter out the date field with NULLs (as parsing will fail wherever format is not matching). At the end, union all the data frames with non-null date fields

Performance will be poor because of multiple runs through the same file. Any other suggestions?

### 2. When you have two dataframes with the same name of the field used for joins (say ID field in both the DFs are used for joining), how will you use the post- join dataframe to select that field? Spark will crash with "ambiguous column" issue as the join-result dataframe will have two fields with the same name.

Ans: Multiple options:
1. Rename the column from one of the DFs and use that to join
2. In the post-join DF, use qualified name for columns. e.g. originalDF1.col("col_name"). Spark maintains a relationship of cols from its source DFs based on unique Ids, so it will be able to map columns to their source dataframe(s)
Other options can also be evaluated.

### 3. How will you read from a file with mulit-char delimiters? e.g. '@@#'
Ans: https://medium.com/towards-artificial-intelligence/pyspark-process-multiple-delimited-data-ef99fa05c6f7


### 4. How will you get the YARN application Id for your Spark job?
SparkContext sc = new SparkContext();
      sc.applicationId();
      
 Only works if you have the driver (deployment in client mode)     
      
#### Followup:
#### How will you do this if the job is deployed in cluster deploy-mode( which means the driver is on the cluster somewhere)
You can save applicationId to a file on hdfs/ S3/ any other layer and then read it from there in your code/ email notification (when the file gets created) etc.
