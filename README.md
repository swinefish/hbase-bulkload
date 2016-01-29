# hbase-bulkload
HBase Bulk Loading from Spark

This will be used to Bulk Load data from CSV files into HBase using Spark. Crucially, although this uses Spark, it is *not* streaming. The streaming works well, but since it is not file aware there is no way to know if a file has been processed, or how many records from a file were processed. This will be essential.

The current plan is as follows:

1. Files are moved into folder
2. Oozie runs python script at regular intervals
3. Get directory listing.
4. Process each file into an RDD
5. Process each line within the RDD
6. If record is sound, put into tuple and increment success
7. If record is bad, append to error file and increment fail
8. Write HFile and bulk load.
9. Write to audit table with filename, datetime, total records, success and fail
10. Move file to processed directory
