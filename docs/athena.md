# Athena

## Caveats
Queries' resultsets must be stored in an S3 bucket, and that bucket must be in
the same region as the Athena resources queried.

## Using a Local SQL Client to Query Athena
AWS provides 
[JDBC Drivers](https://docs.aws.amazon.com/athena/latest/ug/connect-with-jdbc.html)
for Athena.

Most SQL client written in Java will work with it. 
[DBeaver](https://dbeaver.io/) is one such client. It is also free.

Be aware that DBeaver does won't be able to retrieve resultsets of queries
between different sessions. Running them several times will only stack 
resultsets in the specified output bucket.

## Execute a query

```shell
aws athena start-query-execution \
    --query-string "SELECT * FROM database.table limit 10;"\
    --result-configuration "OutputLocation=s3://output-bucket/"
```