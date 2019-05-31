# TerraformTest
Create KMS Key in my-dev AWS

It is complete KMS Example

Configuration in this directory creates a KMS key and its alias.


Usage
To run this example you need to execute:

$ terraform init

$ terraform plan

$ terraform apply

Note that this example may create resources which cost money. Run terraform destroy when you don't need these resources.

Found different approaches how to use variables:
--- I - to set the region in execution time:
variable "region" {} is used in scripts but is not set
region  = "${var.region}"
While executing the Terraform it should be set
terraform plan -var region=eu-west-1
terraform apply -var region=eu-west-1

--- II - to use files with predefined variables:
variable "region" {} is used in scripts but is not set

There is an additional file ./modules/terraform.tfvars in which
different variables could be set (for lambda, for cmk_key, etc.).
terraform plan -var-file=./terraform.tfvars
terraform apply -var-file=./terrafom.tfvars

If such kind of files is suitable to be used per region they could be
set and used per region.
For different regions could be created different variable files
(also tf_us.tfvars, tf_eu.tfvars, etc.). Examples:

terraform plan -var-file=./cmk_key/tf_eu-west-1.tfvars
terraform apply -var-file=./cmk_key/tf_eu-west-1.tfvars

Otherwise, it will be very useful if we could set other variables in the
only file terraform.tfvars.
For instance, I have set the region and the environment variables in it
for test purposes.

The I and the II approaches are tested while CMK key is creating and
they work both.
