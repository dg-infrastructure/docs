---
sidebar_label: "OpenTofu & Terraform Compatibility"
---

# Compatibility with OpenTofu and Terraform

All code in Gruntwork Library is compatible with:

- All versions of [OpenTofu](https://opentofu.org/)
- HashiCorp Terraform versions v1.5.6 and below

## Why the split?

See our blog post [The Future of Terraform Must Be Open](https://blog.gruntwork.io/the-future-of-terraform-must-be-open-ab0b9ba65bca) for details.

## What's special about HashiCorp Terraform v1.5.6?

This is the last version of HashiCorp Terraform that is licensed under the MPLv2 open source license. Any version of Terraform at or below v1.5.6 remains licensed under the MPLv2 license and will continue to work as it always has.

## What if I want to use a version of Terraform above v1.5.6?

Going forward, we recommend that all Gruntwork customers adopt [OpenTofu](https://opentofu.org/) as a "drop-in" replacement for HashiCorp Terraform. We will be developing against OpenTofu releases, testing for compatiability with OpenTofu, and offering full support for any issues you experience with our modules and OpenTofu.

You are welcome to try using versions of Terraform above v1.5.6, however we can't guarantee compatibility, we will not be testing our code with those versions, and we cannot offer support for those versions.

## As a user of Gruntwork Library, do I need to change anything?

No. You can continue using any version of HashiCorp Terraform up to and including v1.5.6.

When you wish to upgrade your Terraform binary, you should replace HashiCorp Terraform with [OpenTofu](https://opentofu.org/).