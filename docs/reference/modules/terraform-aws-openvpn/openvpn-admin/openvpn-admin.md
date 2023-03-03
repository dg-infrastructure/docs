---
title: "openvpn-admin"
hide_title: true
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import VersionBadge from '../../../../../src/components/VersionBadge.tsx';
import { HclListItem, HclListItemDescription, HclListItemTypeDetails, HclListItemDefaultValue, HclGeneralListItem } from '../../../../../src/components/HclListItem.tsx';
import { ModuleUsage } from "../../../../../src/components/ModuleUsage";

<VersionBadge repoTitle="Open VPN Package Infrastructure Package" version="0.25.0" />

# openvpn-admin

<a href="https://github.com/gruntwork-io/terraform-aws-openvpn/tree/main/modules/openvpn-admin" className="link-button" title="View the source code for this module in GitHub.">View Source</a>

<a href="https://github.com/gruntwork-io/terraform-aws-openvpn/releases?q=" className="link-button" title="Release notes for only the service catalog versions which impacted this service.">Release Notes</a>

This module contains a command-line utility that allows users to request new certificates, administrators to revoke
certificates and the OpenVPN server to process those requests.

## New Certificate Request Workflow

![openvpn-request-flow-diagram](/img/reference/modules/terraform-aws-openvpn/openvpn-admin/openvpn-request-flow-diagram.svg)

## Revoke Certificate Workflow

![openvpn-revoke-flow-diagram](/img/reference/modules/terraform-aws-openvpn/openvpn-admin/openvpn-revoke-flow-diagram.png)


<!-- ##DOCS-SOURCER-START
{
  "originalSources": [
    "https://github.com/gruntwork-io/terraform-aws-openvpn/tree/main/modules/openvpn-admin/readme.md",
    "https://github.com/gruntwork-io/terraform-aws-openvpn/tree/main/modules/openvpn-admin/variables.tf",
    "https://github.com/gruntwork-io/terraform-aws-openvpn/tree/main/modules/openvpn-admin/outputs.tf"
  ],
  "sourcePlugin": "module-catalog-api",
  "hash": "06d9f547bf7efd7f9d1608794f73cb74"
}
##DOCS-SOURCER-END -->