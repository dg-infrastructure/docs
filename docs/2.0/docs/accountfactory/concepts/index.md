# Gruntwork Account Factory

Gruntwork Account Factory lets you create new AWS accounts with best-practice baselines.

Enterprise customers can create dedicated Infrastructure as Code repositories for new accounts during the vending process. As a result, central platform teams can automate AWS account creation and delegate infrastructure management to individual teams for scalability and autonomy.

This approach empowers developer teams to self-service deploy infrastructure within the confines of IAM roles managed in a centralized access control repository. This approach ensures least-privilege access to AWS resources while enabling flexible, self-service infrastructure deployment.

Gruntwork Account Factory is built on Gruntwork Pipelines, ensuring reliable and automated account provisioning. Account creation requests are tracked in Git as Infrastructure as Code (IaC), triggering Terragrunt plans and applies to set up and baseline the accounts. By following this approach, account provisioning follows the same review and collaboration steps as other infrastructure changes, using pull requests for validation

## Account baselines

Gruntwork Account Factory does more than create AWS accounts—it also provisions a set of customizable baseline resources to prepare accounts for immediate use in production workloads.

These baselines include:

1. Security configurations for services such as [GuardDuty](https://aws.amazon.com/guardduty/), [SecurityHub](https://aws.amazon.com/security-hub/), and [Macie](https://aws.amazon.com/macie/), following best practices.
2. Networking configurations aligned with best practices for [AWS VPCs](https://aws.amazon.com/vpc/).
3. IAM roles designed for least privilege access, enabling CI/CD pipelines to manage AWS resources using [GitHub OIDC](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services).


## White glove support

Enterprise customers benefit from tailored white glove support to customize account baselines and the vending process according to their needs. This support includes:

1. Adjusting security configurations within the account baseline and ensuring compliance with frameworks like CIS from the outset.
2. Modifying networking configurations in the account baseline, including support for [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/) setups and integration of network inspection appliances like [AWS Network Firewall](https://aws.amazon.com/network-firewall/).
3. Customizing access control for delegated infrastructure management repositories, automatically assigning specific teams the necessary permissions to manage IaC for newly created accounts.

