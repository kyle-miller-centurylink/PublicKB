{{{
  "title": "Partner Cloud Integration: CenturyLink Permissions and Access for Optimized AWS Accounts",
  "date": "03-01-2018",
  "author": "Ben Swoboda",
  "attachments": [],
  "contentIsHTML": false
}}}

### Overview

Amazon Web Services Accounts that are hardened by CenturyLink will provide our tools and Operations Staff  permissions as discussed in the Service Guide. The Service Guide provides a high-level overview of those permissions. The goal of this is to provide some more detail (without posting the specific AWS JSON files used). The groups requiring the permissions will be described along with the type of permissions they are expected to have.

### Audience

Users of accounts that already have or are considering CenturyLink Optimization of AWS Accounts. This is for all new AWS accounts created through Cloud Application Manager and any existing account moving into CenturyLink's care.

### Prerequisites

For a new AWS Account:
* The customer must have reviewed the process for creating a [new Amazon Web Services account](partner-cloud-integration-aws-new.md)

For an existing AWS Account:
* The customer must already have an AWS account that has been specifically mentioned in the AWS account transfer process. (Only approved accounts are authorized for this process.)
* The customer must have reviewed the process for transferring an [existing Amazon Web Services account](partner-cloud-integration-aws-existing.md)


### Important Information

#### Root Level Access

Root level access is not provided to CenturyLink users for any account. Root account access should be avoided unless absolutely necessary. This is true for both Master Payer accounts owned by CenturyLink and any linked account owned by the customer.

For existing accounts, the Customer administrator is asked to set up MFA access after configuration and keep their key in a secure location. Customers are also asked never to log in with root account access.

For Master Payers and new accounts created through Cloud Application Manager, MFA access is set up after configuration of the account is complete. The key is kept in an encrypted vault within a domain separated from the main CenturyLink domain.


#### Federated access
All the roles described below except for the Customer Admin maintain a trust with CenturyLink accounts. This allows certain CenturyLink users and automated tools access to customer accounts, inheriting the permissions and restrictions described with the roles below.

#### IAM Access
The following categories explain how CenturyLink automatically provides or restricts access to internal and customer users.

All policies summarized in this document are the result of intensive consultation with AWS MSP specialists, and are designed to be in accordance with partner requirements and suggested best practices. All policies have been reviewed and approved by the vendor and 3rd party auditors.

**Customer Policy**
* **Policy Name**: CTLCustomerPolicy
* **Targeted groups/tools/users**: Any customer user. This policy is applied to all customer IAM Groups.
* **Intent**: To either be added to existing customer IAM groups or to be given to new customer groups. This policy allows the user to manipulate all services within AWS, but restricts certain views and actions that would be confusing or cause conflict in an Optimized account.
* **Change Requests**: CenturyLink expects to improve these policies over time to allow more permissions to the Customer users. If there are any concerns or desired exceptions regarding these policies, please submit a ticket and one of our Product Team members will be glad to discuss it with you.
* **Policy Summary**
> * Restricts the ability to link or unlink from an organization.
> * Restricts deleting CenturyLink-defined IAM policies, roles and additional sundry functions (such as MFA/SAML deletion).
> * Billing/Usage/Budgeting aspects of the portal are restricted to prevent confusion due to CenturyLink consolidated billing. (Optimized accounts have access to this data through Cloud Application Manager's Analytics tools.)


**CenturyLink Developer Policy**
* **Policy Name**: CTLDeveloperPolicy
* **Role Name**: CTLDeveloperRole
* **Targeted groups/tools/users**:Cloud Application Manager's Optimization tool. A limited number of CenturyLink developers have access to the tool.
* **Intent**: The Optimization tool should be able to configure customer accounts, affect IAM permissions, and swiftly remediate any issues.
* **Change Requests**: Because CenturyLink must maintain administrative access, no changes can be made at this time. Please see the [Service Guide](https://www.ctl.io/legal/cloud-application-manager/service-guide/) for details.
* **Policy Summary**:
> * Full access

**CenturyLink Lambda Policy**
* **Policy Name**: CTLAccountControlsLambdaPolicy
* **Role Name**: CTLAccountControlsLambdaRole
* **Targeted groups/tools/users**: Newly created IAM users that are not in IAM Groups
* **Intent**: Our hardening applies continuous auto-remediation steps to ensure your accounts are protected. Newly created IAM users that are not placed within a group will have all their permissions removed. Once they are placed in a group, permissions can be applied again. Newly created IAM groups will automatically have the CTLCustomerPolicy applied. These steps are taken to ensure a seamless experience between Cloud Application Manager and your AWS account. This also allows CenturyLink to ensure your account continues to meet best practice security guidelines.
* **Change Requests**: This policy is intended to help, not hinder you. If you find it is not working in your best interest, please contact CenturyLink.
* **Policy Summary**:
> * Full control of IAM and Config



**Cloud Application Manager Policy**
* **Policy Name**: CTLCAMPolicy
* **Role Name**: CTLCAMRole
* **Targeted groups/tools/users**: Cloud Application Manager
* **Intent**: To permit Cloud Application Manager's application lifecycle management (ALM) capabilities.
* **Change Requests**: [The standard CAM policy](https://www.ctl.io/knowledge-base/cloud-application-manager/deploying-anywhere/using-your-aws-account/) is meant to be customizable. If you would like to alter the ALM capabilities of Cloud Application Manager, please submit a ticket describing the policy you wish to apply.
* **Policy Summary**
> * All the ability to manipulate resources as described [here](../Deploying Anywhere/using-your-aws-account.md)
> * Allows governance for all EC2 functions
> * Full control of typical autoscaling/Cloud Formation/RDS/S3 tasks
> * Allows IAM user/policy creation, deletion, listing and modification.
> * Allows core Cloud Application Manager functionality and delegation for Managed Services Anywhere assistance.

**CenturyLink Analytics Policy**
* **Policy Name**: CTLCloudOptimization
* **Role Name**: CTLCloudOptimization
* **Targeted groups/tools/users**: Cloud Optimization and Analytics tool
* **Intent**: To enable Analytics tools and allow customer users transparency into usage and best practices.
* **Change Requests**: It is not recommended to change the IAM Policy.
* **Policy Summary**
> * Get, List, and Describe capabilities for AWS Certificate Manager, Cloud Formation, CloudFront, Cloud HSM, CloudSearch, CloutTrail, CloudWatch, Config, Data Pipeline, Direct Connect, Dynamo DB, EC2, ECS, Elasticache, Elastic Beanstalk, EFS, ELB, Elastic Map Reduce, Elastisearch, Glacier, IAM, Kinesis, key Management Service, Lambda, RDS, Redshift, Route 53, S3, Simple Email Service, Simple DB, Support, Simple Workflow Service, Simple Notification Service, Simple Queue Service, Storage Gateway, and Workspaces.

**Cloud Application Manager Policy**
* **Policy Name**: CTLCAMPolicy, ReadOnlyAccess
* **Role Name**: CTLCAMRole
* **Targeted groups/tools/users**: Cloud Application Manager, Monitoring Service
* **Intent**: To permit Cloud Application Manager's application lifecycle management (ALM) capabilities and to enable [Monitoring](../Monitoring/CTLCloudMonitoringUI.md).
* **Change Requests**: [The standard CAM policy](../Deploying Anywhere/using-your-aws-account.md) is meant to be customizable. If you would like to alter the ALM capabilities of Cloud Application Manager, please submit a ticket describing the policy you wish to apply.
* **Policy Summary**
> * All the ability to manipulate resources as described [here](../Deploying Anywhere/using-your-aws-account.md)
> * Allows governance for all EC2 functions
> * Full control of typical autoscaling/Cloud Formation/RDS/S3 tasks
> * Allows IAM user/policy creation, deletion, listing and modification.
> * Allows core Cloud Application Manager functionality and delegation for Managed Services Anywhere assistance.
> * Allows ReadOnlyAccess to enable the [Monitoring](../Monitoring/CTLCloudMonitoringUI.md) feature on Cloud Application Manager

**CenturyLink Service Management Policy**
* **Policy Name**: CTLServiceManagmentPolicy
* **Role Name**: CTLServiceManagmentRole
* **Targeted groups/tools/users**: Service Management Staff
* **Intent**:This is not an immediate part of any Optimization scenario but it is enabled by the Cloud Application Manager Account Optimization. Access to a customer's account via this role is only given to a CenturyLink representative when the customer has purchased Service Management from CenturyLink.
* **Change Requests**: You may wish to have this default role removed or altered at any time. Please submit a ticket describing the change you would like.
* **Policy Summary**:
> * Add, Change, and Delete capabilities for all services. No capabilities to edit account details or budgets.*
