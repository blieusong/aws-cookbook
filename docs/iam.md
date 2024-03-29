# IAM

## Searching a Given Pattern in all the Policies of an Account
Looking for `pattern`
```shell
for arn version in $(aws iam list-policies --scope Local | jq -r ".Policies[] | [.Arn,.DefaultVersionId] | @csv " | sed 's/"//g' | cut -f1,2 -d, | tr , ' '); do
    echo $arn
    aws iam get-policy-version --no-cli-pager --policy-arn $arn --version-id $version | grep -i "pattern"
done
```

## Finding Who Has Access to a Folder in an S3 Bucket
This script generates a CSV file which lists the users of an account and tells
if they have `s3:GetObject` access to the `/specific/folder` in `bucket_name` 
bucket or not.

```shell
(
    echo "User;Access allowed" && \
    for user in $(aws iam list-users --query 'Users[].Arn' --output text); do
        echo "${user};"\
$(aws iam simulate-principal-policy --policy-source-arn "$user" \
            --action-names "s3:GetObject" \
            --resource-arns "arn:aws:s3:::bucket_name/specific/folder/*" \
        | jq -r ".EvaluationResults[].EvalDecision")
    done
) | tee file.csv
```
