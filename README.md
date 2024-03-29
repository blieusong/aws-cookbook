# AWS Cookbook
Collection of AWS commands and scripts that I use on a regular basis.

- [S3](docs/s3.md)
- [Athena](docs/athena.md)
- [Glue](docs/glue.md)
- [SES](docs/ses.md)
- [IAM](docs/iam.md)
- [STS](docs/sts.md)


## Prerequisites
### Dependencies
- [**jq**](https://stedolan.github.io/jq/): A lightweight and flexible 
  command-line JSON processor.
- [**parallel**](https://www.gnu.org/software/parallel/): A shell tool for 
  executing jobs in parallel using one or more computers.
- [**s5cmd**](https://github.com/peak/s5cmd): A fast S3 command line tool written
  in Go.

### Config
In the **aws**' `config` file, set the output to `json`.

```
output = json
```
