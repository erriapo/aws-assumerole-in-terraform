# Motivation

[awscli](https://pypi.org/project/awscli/) stores its credentials by default in plaintext in `~/.aws/credentials`. By using  [aws-vault](https://github.com/99designs/aws-vault) we can store them encrypted in a file or in a keyring. The invocation now looks like this:

```bash
$ aws-vault --prompt=terminal exec calvin -- env
Enter passphrase to unlock /home/eigerultra2018/.awsvault/keys/: ______
..snipped..
```

Following best practices, we add an iam-policy to enforce MFA (Virtual MFA) for all IAM users. This forces `aws-vault` to prompt for the token.

```bash
$ aws-vault --prompt=terminal exec calvin -- env
Enter passphrase to unlock /home/eigerultra2018/.awsvault/keys/: ______
Enter token for arn:aws:iam::111111111111:mfa/calvin: 890980
..snipped..
```

All looks good. Now we want to run `terraform` via `aws-vault`. The aws provider has an `assume_role` section that looks promising. 

```HCL
provider "aws" {
  assume_role {
    role_arn     = "arn:aws:iam::ACCOUNT_ID:role/ROLE_NAME"
  }
}
```

aa

```
provider "aws" {
  assume_role {
    role_arn     = "arn:aws:iam::ACCOUNT_ID:role/ROLE_NAME"
    session_name = "SESSION_NAME"
    external_id  = "EXTERNAL_ID"
  }
}
```

Foo

```bash
AWS_VAULT=calvin
AWS_DEFAULT_REGION=us-east-2
AWS_REGION=us-east-2
AWS_ACCESS_KEY_ID=ASIA************
AWS_SECRET_ACCESS_KEY=Vcga********
AWS_SESSION_TOKEN=FQo*************
AWS_SECURITY_TOKEN=FQo************
```

# Scenario

Hello World

![scenario](mfa-delegated-accounts.png)

# Solution

Uses

*


