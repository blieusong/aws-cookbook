# Glue
AWS Glue is a managed ETL service.

## ARNs
### Glue Catalog ARN Format
<pre>
arn:aws:glue:<i>region</i>:<i>account-id</i>:catalog
</pre>

Example:

`arn:aws:glue:eu-west-1:999999999999:catalog`

### Glue Database ARN Format
<pre>
arn:aws:glue:<i>region</i>:<i>account-id</i>:database/<i>database name</i>
</pre>

Example:

`arn:aws:glue:eu-west-1:999999999999:database/salesdb`

### Glue Table ARN Format
<pre>
arn:aws:glue:<i>region</i>:<i>account-id</i>:table/<i>database name</i>/<i>table name</i>
</pre>

Example:

`arn:aws:glue:eu-west-1:999999999999:table/salesdb/salestable`

## Listing All Glue Tables And Their S3 Location
Assuming *accound id* is 999999999999, and saving the output in file 
`tables_location.json`:

```shell
(for database in $(aws glue get-databases --catalog-id 999999999999 | jq ".DatabaseList[]" | jq -r ".Name"); do
     for table in $(aws glue get-tables --database-name $database --catalog-id 999999999999 | jq ".TableList[]" | jq -r ".Name"); do
         aws glue get-table --database-name $database --name $table | jq -c ".Table | {database: .DatabaseName, name: .Name, location: .StorageDescriptor.Location}"
     done
 done) | tee tables_location.json
 ```

 This command also retrieve views, which are not tables. To filter out views,