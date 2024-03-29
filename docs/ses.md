# SES (Simple Email Service)

## Request production access for SES
Assuming accessing AWS account with profile **my_profile**:

```shell
aws sesv2 put-account-details \
--profile my_profile \
--production-access-enabled \
--mail-type TRANSACTIONAL \
--website-url https://your.website.com \ # doesn't matter
--use-case-description "describe your usecase" \
--additional-contact-email-addresses your.email@gmail.com \
--contact-language EN
```