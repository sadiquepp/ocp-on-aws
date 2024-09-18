**Installation-Day1/openshift-installer.json:** These permissions are required to install openshift and is used by openshift-installer. This can be via ec2 assumerole if openshift-install is done from an ec2 instance or via an access key and secret key authentication done through aws configure.

**Installation-Day1/ccoctl-permission.json:** When STS is used for operators, these permissions are rquired by ccoctl to create S3 bucket, CloudFront Distribution, IAM Identity Provider, IAM Policies, IAM roles, Policy to Role attachment, etc. This can be via ec2 assume role if ccoctl is run from an ec2 instance or via access key and secret key authentication done through aws configure. If both openshift-install and ccoctl are run from same node, attach both policies. This permission may need to be re-instated on Day 2 for openshift major upgrades eg from 4.15 -> 4.16 to update policies if new permissions are needed by new version of the OCP.   

**Operator-Day1-Day2/sts-assume-by-master-ec2.json:** This policy is created by openshift-installer and attached to the role assigned to the master nodes via iam:PassRole during Day1. This is required for Day1 and Day2. 

**Operator-Day1-Day2/sts-assume-by-worker-ec2.json:** This policy is created by openshift-installer and attached to the role assigned to the worker nodes via iam:PassRole during Day1. This is required for Day1 and Day2. 

**Operator-Day1-Day2/other-policies**: Other policies are assumed by openshift pods for various Day1 and Day2 operations. This uses sts:AssumeRoleWithWebIdentity Federated by an OIDC Identity Provider. The trust relationship tempalate is trust-relationship-template.json. This role, policies and trust relationship are automatically created by **Installation-Day1/ccoctl-permission.json:** on Day1. This is given here for information only.
