---
pagination_label: Update to Terraform 13
---

# Intro

This guide will walk you through how to update the [Gruntwork Reference
Architecture](https://gruntwork.io/reference-architecture/) and any code that depends on the
[Gruntwork Infrastructure as Code Library](https://gruntwork.io/infrastructure-as-code-library/) to
[Terraform 0.13](https://www.terraform.io/upgrade-guides/0-13.html). Terraform 0.13 introduces a number of new features
and fixes, but it also has a number of backwards incompatibilities that have to be incorporated into your codebase.

## What you’ll learn in this guide

This guide consists of two main sections:

<div className="dlist">

#### [Core Concepts](1-core-concepts.md)

An overview of Terraform 0.13 and why it is important to update your code for compatibility.

#### [Deployment walkthrough](2-deployment-walkthrough/0-step-1-update-your-code-to-be-compatible-with-terraform-0-12.md)

The steps you need to take to update your code relying on the Gruntwork Infrastructure as Code library and your
version of the Gruntwork Reference Architecture to work with Terraform 0.13. Includes a
[version compatibility table](2-deployment-walkthrough/2-step-3-update-references-to-the-gruntwork-infrastructure-as-code-library.md#version-compatibility-table) you can use as a reference to know which Gruntwork Repo version
tag is compatible with Terraform 0.13.

</div>


<!-- ##DOCS-SOURCER-START
{"sourcePlugin":"Local File Copier","hash":"9ce84b5d01352a6d8dbc986f0c086ea3"}
##DOCS-SOURCER-END -->