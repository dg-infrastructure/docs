---
title: "Control Tower Account Factory"
hide_title: true
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import VersionBadge from '../../../../../src/components/VersionBadge.tsx';
import { HclListItem, HclListItemDescription, HclListItemTypeDetails, HclListItemDefaultValue, HclGeneralListItem } from '../../../../../src/components/HclListItem.tsx';
import { ModuleUsage } from "../../../../../src/components/ModuleUsage";

<VersionBadge repoTitle="terraform-aws-control-tower" version="0.0.18" />

# Control Tower Account Factory

<a href="https://github.com/gruntwork-io/terraform-aws-control-tower/tree/v0.0.18/modules/landingzone/control-tower-account-factory" className="link-button" title="View the source code for this module in GitHub.">View Source</a>

<a href="https://github.com/gruntwork-io/terraform-aws-control-tower/releases?q=control-tower-account-factory" className="link-button" title="Release notes for only versions which impacted this module.">Release Notes</a>

This is a Terraform module that will trigger the creation of a new AWS account by using Control Tower.

Under the hood, this module uses AWS Service Catalog to trigger Control Tower, as Control Tower does not currently
expose any APIs to trigger it directly.

## Control Tower Service Catalog YAML

The below YAML is copied from the Control Tower product in AWS Service Catalog. It is useful in knowing what
parameters to pass to this Service Catalog product:

*Note: some of the data below (e.g., the `AllowedValues` for `ManagedOrganizationalUnit`) is auto-generated for each
AWS organization, so it will vary from org to org.*

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: AWS Control Tower Account Factory Template (DO NOT DELETE)
Parameters:
  AccountName:
    Description: "Account name, the new managed Account will be created with this name."
    Type: String
    AllowedPattern : ".+"
  AccountEmail:
    Description: "Account email, must be unique for each AWS Account."
    Type: String
    AllowedPattern : "[^\\s@]+@[^\\s@]+\\.[^\\s@]+"
  SSOUserFirstName:
    Description:  "SSO user first name."
    Type: String
    AllowedPattern : ".+"
  SSOUserLastName:
    Description:  "SSO user last name."
    Type: String
    AllowedPattern : ".+"
  SSOUserEmail:
    Description: "SSO user email. A new SSO user will be created for this email, if it does not exist. This SSO user will be associated with the new managed Account."
    Type: String
    AllowedPattern : "[^\\s@]+@[^\\s@]+\\.[^\\s@]+"
  ManagedOrganizationalUnit:
    Description: "Your account will be added to this registered organizational unit. The list includes top-level and nested OUs registered with AWS Control Tower. You can search for an OU by name or ID. To manage these OUs, go to AWS Control Tower."
    Type: String
    AllowedValues:
      - XXX (ou-abcd-12345678)
      - YYY (ou-abcd-91011121)
      - ZZZ (ou-abcd-34151617)
Resources:
  WaitCondition:
    Type: AWS::CloudFormation::WaitCondition
    Properties:
      Handle: WaitHandle
      Timeout: 1
  WaitHandle:
    Type: AWS::CloudFormation::WaitConditionHandle
```

## Sample Usage

<Tabs>
<TabItem value="terraform" label="Terraform" default>

```hcl title="main.tf"

# ------------------------------------------------------------------------------------------------------
# DEPLOY GRUNTWORK'S CONTROL-TOWER-ACCOUNT-FACTORY MODULE
# ------------------------------------------------------------------------------------------------------

module "control_tower_account_factory" {

  source = "git::git@github.com:gruntwork-io/terraform-aws-control-tower.git//modules/landingzone/control-tower-account-factory?ref=v0.0.18"

  # ----------------------------------------------------------------------------------------------------
  # REQUIRED VARIABLES
  # ----------------------------------------------------------------------------------------------------

  # Account email, must be globally unique across all AWS Accounts.
  account_email = <string>

  # The name to use for the new AWS account
  account_name = <string>

  # The name of the organizational unit (OU) in which this account should be
  # created. Must be one of the OUs in your Control Tower dashboard.
  organizational_unit_name = <string>

  # The email address of the user who will be granted admin access to this new
  # account through AWS SSO.
  sso_user_email = <string>

  # The first name of the user who will be granted admin access to this new
  # account through AWS SSO.
  sso_user_first_name = <string>

  # The last name of the user who will be granted admin access to this new
  # account through AWS SSO.
  sso_user_last_name = <string>

  # ----------------------------------------------------------------------------------------------------
  # OPTIONAL VARIABLES
  # ----------------------------------------------------------------------------------------------------

  # If specified, this is assumed to be the file path of a YAML file where the
  # details of the new account created by this module will be written (if the
  # file already exists, the module will merge its data into the file). The
  # expected format of this YAML file is that the keys are the account names and
  # the values are objects with the following keys: id (the account ID), email
  # (the root user email address for the account).
  accounts_yaml_path = null

  # The ID of the AWS Control Tower Account Factory provisioning artifact in AWS
  # Service Catalog to use. On initial creation, we are able to look this up
  # automatically by name, but due to a Terraform or AWS bug
  # (https://github.com/hashicorp/terraform-provider-aws/issues/24362), the
  # lookup fails if you try to modify the account creation details (e.g., you
  # try to modify the SSO user details after the account has been created). In
  # those cases, you have to look up the ID manually by going to the Product
  # List in the AWS Service Catalog console
  # (https://console.aws.amazon.com/servicecatalog/home#admin-products),
  # clicking the 'AWS Control Tower Account Factory' product, and grabbing the
  # ID of the latest product version from the Product Versions table at the
  # bottom.
  provisioning_artifact_id = null

}


```

</TabItem>
<TabItem value="terragrunt" label="Terragrunt" default>

```hcl title="terragrunt.hcl"

# ------------------------------------------------------------------------------------------------------
# DEPLOY GRUNTWORK'S CONTROL-TOWER-ACCOUNT-FACTORY MODULE
# ------------------------------------------------------------------------------------------------------

terraform {
  source = "git::git@github.com:gruntwork-io/terraform-aws-control-tower.git//modules/landingzone/control-tower-account-factory?ref=v0.0.18"
}

inputs = {

  # ----------------------------------------------------------------------------------------------------
  # REQUIRED VARIABLES
  # ----------------------------------------------------------------------------------------------------

  # Account email, must be globally unique across all AWS Accounts.
  account_email = <string>

  # The name to use for the new AWS account
  account_name = <string>

  # The name of the organizational unit (OU) in which this account should be
  # created. Must be one of the OUs in your Control Tower dashboard.
  organizational_unit_name = <string>

  # The email address of the user who will be granted admin access to this new
  # account through AWS SSO.
  sso_user_email = <string>

  # The first name of the user who will be granted admin access to this new
  # account through AWS SSO.
  sso_user_first_name = <string>

  # The last name of the user who will be granted admin access to this new
  # account through AWS SSO.
  sso_user_last_name = <string>

  # ----------------------------------------------------------------------------------------------------
  # OPTIONAL VARIABLES
  # ----------------------------------------------------------------------------------------------------

  # If specified, this is assumed to be the file path of a YAML file where the
  # details of the new account created by this module will be written (if the
  # file already exists, the module will merge its data into the file). The
  # expected format of this YAML file is that the keys are the account names and
  # the values are objects with the following keys: id (the account ID), email
  # (the root user email address for the account).
  accounts_yaml_path = null

  # The ID of the AWS Control Tower Account Factory provisioning artifact in AWS
  # Service Catalog to use. On initial creation, we are able to look this up
  # automatically by name, but due to a Terraform or AWS bug
  # (https://github.com/hashicorp/terraform-provider-aws/issues/24362), the
  # lookup fails if you try to modify the account creation details (e.g., you
  # try to modify the SSO user details after the account has been created). In
  # those cases, you have to look up the ID manually by going to the Product
  # List in the AWS Service Catalog console
  # (https://console.aws.amazon.com/servicecatalog/home#admin-products),
  # clicking the 'AWS Control Tower Account Factory' product, and grabbing the
  # ID of the latest product version from the Product Versions table at the
  # bottom.
  provisioning_artifact_id = null

}


```

</TabItem>
</Tabs>




## Reference

<Tabs>
<TabItem value="inputs" label="Inputs" default>

### Required

<HclListItem name="account_email" requirement="required" type="string">
<HclListItemDescription>

Account email, must be globally unique across all AWS Accounts.

</HclListItemDescription>
</HclListItem>

<HclListItem name="account_name" requirement="required" type="string">
<HclListItemDescription>

The name to use for the new AWS account

</HclListItemDescription>
</HclListItem>

<HclListItem name="organizational_unit_name" requirement="required" type="string">
<HclListItemDescription>

The name of the organizational unit (OU) in which this account should be created. Must be one of the OUs in your Control Tower dashboard.

</HclListItemDescription>
</HclListItem>

<HclListItem name="sso_user_email" requirement="required" type="string">
<HclListItemDescription>

The email address of the user who will be granted admin access to this new account through AWS SSO.

</HclListItemDescription>
</HclListItem>

<HclListItem name="sso_user_first_name" requirement="required" type="string">
<HclListItemDescription>

The first name of the user who will be granted admin access to this new account through AWS SSO.

</HclListItemDescription>
</HclListItem>

<HclListItem name="sso_user_last_name" requirement="required" type="string">
<HclListItemDescription>

The last name of the user who will be granted admin access to this new account through AWS SSO.

</HclListItemDescription>
</HclListItem>

### Optional

<HclListItem name="accounts_yaml_path" requirement="optional" type="string">
<HclListItemDescription>

If specified, this is assumed to be the file path of a YAML file where the details of the new account created by this module will be written (if the file already exists, the module will merge its data into the file). The expected format of this YAML file is that the keys are the account names and the values are objects with the following keys: id (the account ID), email (the root user email address for the account).

</HclListItemDescription>
<HclListItemDefaultValue defaultValue="null"/>
</HclListItem>

<HclListItem name="provisioning_artifact_id" requirement="optional" type="string">
<HclListItemDescription>

The ID of the AWS Control Tower Account Factory provisioning artifact in AWS Service Catalog to use. On initial creation, we are able to look this up automatically by name, but due to a Terraform or AWS bug (https://github.com/hashicorp/terraform-provider-aws/issues/24362), the lookup fails if you try to modify the account creation details (e.g., you try to modify the SSO user details after the account has been created). In those cases, you have to look up the ID manually by going to the Product List in the AWS Service Catalog console (https://console.aws.amazon.com/servicecatalog/home#admin-products), clicking the 'AWS Control Tower Account Factory' product, and grabbing the ID of the latest product version from the Product Versions table at the bottom.

</HclListItemDescription>
<HclListItemDefaultValue defaultValue="null"/>
</HclListItem>

</TabItem>
<TabItem value="outputs" label="Outputs">

<HclListItem name="account_email">
<HclListItemDescription>

The email address of the newly created account

</HclListItemDescription>
</HclListItem>

<HclListItem name="account_id">
<HclListItemDescription>

The ID of the newly created account

</HclListItemDescription>
</HclListItem>

<HclListItem name="organizational_unit_id">
<HclListItemDescription>

The ID of the Organizational Unit (OU) this account was created in.

</HclListItemDescription>
</HclListItem>

<HclListItem name="service_catalog_provisioned_product_arn">
<HclListItemDescription>

The ARN of the Service Catalog product that was provisioned to trigger Control Tower

</HclListItemDescription>
</HclListItem>

<HclListItem name="service_catalog_provisioned_product_id">
<HclListItemDescription>

The ID of the Service Catalog product that was provisioned to trigger Control Tower

</HclListItemDescription>
</HclListItem>

<HclListItem name="service_catalog_provisioned_product_outputs">
<HclListItemDescription>

The outputs of the Service Catalog product that was provisioned to trigger Control Tower

</HclListItemDescription>
</HclListItem>

<HclListItem name="sso_admin_user_email">
<HclListItemDescription>

The email address of the user that has been granted admin access via AWS SSO in this account

</HclListItemDescription>
</HclListItem>

<HclListItem name="sso_user_portal_url">
<HclListItemDescription>

The URL of the AWS SSO login page for this account

</HclListItemDescription>
</HclListItem>

</TabItem>
</Tabs>


<!-- ##DOCS-SOURCER-START
{
  "originalSources": [
    "https://github.com/gruntwork-io/terraform-aws-control-tower/tree/v0.0.18/modules/control-tower-account-factory/readme.md",
    "https://github.com/gruntwork-io/terraform-aws-control-tower/tree/v0.0.18/modules/control-tower-account-factory/variables.tf",
    "https://github.com/gruntwork-io/terraform-aws-control-tower/tree/v0.0.18/modules/control-tower-account-factory/outputs.tf"
  ],
  "sourcePlugin": "module-catalog-api",
  "hash": "8c06d5a027e97fa95b5d75f50fd1fe7f"
}
##DOCS-SOURCER-END -->