---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "awsngfw_security_rule Resource - awsngfw"
subcategory: ""
description: |-
  Resource for security rule manipulation.
---

# awsngfw_security_rule (Resource)

Resource for security rule manipulation.

## Example Usage

```terraform
resource "awsngfw_security_rule" "example" {
  rulestack   = awsngfw_rulestack.r.name
  rule_list   = "LocalRule"
  priority    = 3
  name        = "tf-security-rule"
  description = "Also configured by Terraform"
  source {
    cidrs = ["any"]
  }
  destination {
    cidrs = ["192.168.0.0/16"]
  }
  negate_destination = true
  applications       = ["any"]
  category {}
  action        = "Allow"
  logging       = true
  audit_comment = "initial config"
}

resource "awsngfw_rulestack" "r" {
  name        = "terraform-rulestack"
  scope       = "Local"
  account_id  = "123456789"
  description = "Made by Terraform"
  profile_config {
    anti_spyware = "BestPractice"
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **action** (String) The action to take. Valid values are `Allow`, `DenySilent`, `DenyResetServer`, or `DenyResetBoth`.
- **applications** (Set of String) The list of applications.
- **category** (Block List, Min: 1, Max: 1) The category spec. (see [below for nested schema](#nestedblock--category))
- **destination** (Block List, Min: 1, Max: 1) The destination spec. (see [below for nested schema](#nestedblock--destination))
- **name** (String) The name.
- **priority** (Number) The rule priority.
- **rulestack** (String) The rulestack.
- **source** (Block List, Min: 1, Max: 1) The source spec. (see [below for nested schema](#nestedblock--source))

### Optional

- **audit_comment** (String) The audit comment.
- **decryption_rule_type** (String) Decryption rule type. Valid values are `` or `SSLOutboundInspection`.
- **description** (String) The description.
- **enabled** (Boolean) Set to false to disable this rule. Defaults to `true`.
- **id** (String) The ID of this resource.
- **logging** (Boolean) Enable logging at end. Defaults to `true`.
- **negate_destination** (Boolean) Negate the destination definition.
- **negate_source** (Boolean) Negate the source definition.
- **protocol** (String) The protocol. Defaults to `application-default`.
- **rule_list** (String) The rulebase. Valid values are `PreRule`, `PostRule`, or `LocalRule`. Defaults to `PreRule`.

### Read-Only

- **tag** (List of Object) Tags. (see [below for nested schema](#nestedatt--tag))
- **update_token** (String) The update token.

<a id="nestedblock--category"></a>
### Nested Schema for `category`

Optional:

- **feeds** (Set of String) List of feeds.
- **url_category_names** (Set of String) List of URL category names.


<a id="nestedblock--destination"></a>
### Nested Schema for `destination`

Optional:

- **cidrs** (Set of String) List of CIDRs.
- **countries** (Set of String) List of countries.
- **feeds** (Set of String) List of feeds.
- **fqdn_lists** (Set of String) List of FQDN lists.
- **prefix_lists** (Set of String) List of prefix list.


<a id="nestedblock--source"></a>
### Nested Schema for `source`

Optional:

- **cidrs** (Set of String) List of CIDRs.
- **countries** (Set of String) List of countries.
- **feeds** (Set of String) List of feeds.
- **prefix_lists** (Set of String) List of prefix list.


<a id="nestedatt--tag"></a>
### Nested Schema for `tag`

Read-Only:

- **key** (String)
- **value** (String)

