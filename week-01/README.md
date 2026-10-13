# Week 1 — AWS Account Security and Cost Controls

## What I learned

The AWS root user is the original account owner and has unrestricted access, so I should use it only for tasks that specifically require root credentials. I protected the root user with MFA and confirmed that signing in again requires a verification code. For everyday work, I created the `Peggy-admin` IAM user and granted it administrator permissions instead of continuing to use the root user. IAM lets me create separate identities and control which AWS actions each identity is allowed to perform. I also enabled MFA for my IAM administrator account and configured the AWS CLI to use that IAM identity. Under the Shared Responsibility Model, AWS protects the underlying cloud infrastructure, while I am responsible for securing my identities, permissions, configurations, and data. I created a zero-spend budget so I can monitor costs and react quickly if AWS usage begins generating charges.

## Evidence

- `root-mfa-enabled.png` — the IAM dashboard confirms that the root user has MFA.
- `budget.png` — the zero-spend budget is healthy and currently shows no spending.
- `aws sts get-caller-identity` — verified that the local AWS CLI authenticates as the `Peggy-admin` IAM user.

## Debug Lab 1.5

When the AWS CLI reported `Unable to locate credentials`, I checked the active AWS environment variables and credential configuration. After configuring a valid IAM access key, default Region, and JSON output, `aws sts get-caller-identity` returned the expected IAM user. Credentials and MFA codes must never be committed to GitHub.
