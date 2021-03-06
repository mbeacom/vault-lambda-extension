# Vault Lambda extension Quick Start

Creates the infrastructure required for running a demo of the Vault Lambda extension.
All of the infrastructure is created in `us-east-1` by default, unless you
specify `-var aws_region=...` during `terraform apply`.

* An EC2 instance with a vault server running on it with auto-unseal from KMS
* A new SSH key pair used to SSH into the instance
* IAM role for the Lambda to run as, which will be able to auth against the Vault instance using AWS IAM auth
* Configures Vault
* A Lambda function which requests database credentials from the extension and then uses them to list users on the database

**NB: This demo will create real infrastructure in AWS with an associated
cost. Make sure you tear down the infrastructure once you are finished with
the demo.**

**NB: This is not a production-ready deployment, and is for demonstration
purposes only.**

## Prerequisites

* `bash`, `zip`
* Golang
* Terraform
* AWS account with access key ID and secret access key
* AWS CLI v2 configured with the same account

## Usage

```bash
./build.sh
cd terraform

export AWS_ACCESS_KEY_ID = "<YOUR_AWS_ACCESS_KEY_ID>"
export AWS_SECRET_ACCESS_KEY = "<YOUR_AWS_SECRET_ACCESS_KEY>"
terraform init
terraform apply

# Then run the `aws lambda invoke` command from the terraform output

# Remember to clean up the billed resources once you're finished
terraform destroy
```

## Credit

Adapted from AWS KMS guides in the [vault-guides](https://github.com/hashicorp/vault-guides) repo.
Specifically, mostly from [this guide](https://learn.hashicorp.com/tutorials/vault/agent-aws).
