# Project Resource

The Project resource allows the creation and management of Aiven Projects.

## Example Usage

```hcl
resource "aiven_project" "myproject" {
    project = "<PROJECT_NAME>"
    card_id = "<FULL_CARD_ID/LAST4_DIGITS>"
    account_id = aiven_account_team.<ACCOUNT_RESOURCE>.account_id
}
```

## Argument Reference

* `project` - (Required) defines the name of the project. Name must be globally unique (between all
Aiven customers) and cannot be changed later without destroying and re-creating the
project, including all sub-resources.

* `card_id` - (Optional) is either the full card UUID or the last 4 digits of the card. As the full
UUID is not shown in the UI it is typically easier to use the last 4 digits to identify
the card. This can be omitted if `copy_from_project` is used to copy billing info from
another project.

* `account_id` - (Optional) is an optional property to link a project to already an existing account by 
using account ID.

* `default_cloud` - (Optional) defines the default cloud provider and region where services are
hosted. This can be changed freely after the project is created. This will not affect existing
services.

* `technical_emails` - (Optional) defines the email addresses that will receive alerts about 
upcoming maintenance updates or warnings about service instability. It is a good practice to keep
this up-to-date to be aware of any potential issues with your project.

* `copy_from_project` - (Optional) is the name of another project used to copy billing information and
some other project attributes like technical contacts from. This is mostly relevant when
an existing project has billing type set to invoice and that needs to be copied over to a
new project. (Setting billing is otherwise not allowed over the API.) This only has
effect when the project is created.

## Attribute Reference

In addition to all arguments above, the following attributes are exported:

* `available_credits` - is a computed property returning the amount of platform credits available to
the project. This could be your free trial or other promotional credits.
  
* `ca_cert` - is a computed property that can be used to read the CA certificate of the
project. This is required for configuring clients that connect to certain services like
Kafka. This value cannot be set, only read.

* `estimated_balance` - is a computed property returning the current accumulated bill for this 
project in the current billing period.

* `payment_method` - is a computed property returning the method of invoicing used for payments for
this project, e.g. "card".

Aiven ID format when importing existing resource: name of the project as is.
