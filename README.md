## Code Review Checklist

In addition to the [Code Review Checklist](https://gist.github.com/kashifrazzaqui/44b868a59e99c2da7b14) you should also look for these Terraform specific code review items

* [ ] Make sure the terraform module is in a seperate repository not in a subfolder.
* [ ] Are all providers used in the terraform scripts [versioned](https://www.terraform.io/docs/configuration/providers.html#provider-versions) to prevent breaking changes in the future?
* [ ] Are modules split into separate `.tf` files where appropriate?
* [ ] Does the repository contain a `README.md` describing the architecture provisioned?
* [ ] Is the Terraform project configured using Azure Storage as remote state backend?
* [ ] Is the remote state backend storage account key is stored a secure location (e.g. Azure Key Vault)?
* [ ] If Terraform code is mixed with application source code, is the Terraform code isolated into a dedicated folder?
* [ ] If the infrastructure is going to different depending on the environment (e.g. Dev, UAT, Production), are the environment specific parameters supplied via `.tfvars` file?
* [ ] Is the project configured to use state file based on the environment and the deployment pipeline configured to supply the state file name dynamically?
* [ ] Are the resource definitions and data sources handled correctly in the Terraform scripts?
    resource : Indicates to Terraform that the current configuration is in charge of managing the life cycle of the object
    data: Indicates to Terraform that you only want to get a reference to the existing object, but don’t want to manage it as part of this configuration
* [ ] Is the code split into multiple reusable modules?
* [ ] Are unit and integration tests used for Terraform code (e.g. [`Terratest`](https://terratest.gruntwork.io/), [`terratest-abstraction`](https://github.com/microsoft/terratest-abstraction))?
* [ ] Are the resource names starting with their containing provider's name followed by an underscore? e.g. resource from the provider `postgresql` might be named as `postgresql_database`?
* [ ] Is `try` function used only with simple attribute references and type conversion functions?, as overuse of `try` function to suppress errors will lead to a configuration that is hard to understand and maintain
* [ ] Are the explicit type conversion functions used to normalize types returned only in module outputs?, as the explicit type conversions are rarely necessary in Terraform because it will convert types automatically where required
* [ ] Is `Sensitive` property on schema set to `true` for the fields that contains sensitive information?. This will prevent the field's values from showing up in CLI output
* [ ] Are resource names more descriptive than "aduser1" and "aduser2" or "fw01" and "fw02".
