# STS (Simple Token Service)

## Get a session token for a MFA device
```shell
aws sts get-session-token \
    --serial-number arn:aws:iam::999999999999:mfa/mfa.device.name \
    --token [TOKEN]
```

Then set the environment variable:

```shell
export AWS_SESSION_TOKEN=token_from_response
```

But it is best to use proper AWS CLI profiles.