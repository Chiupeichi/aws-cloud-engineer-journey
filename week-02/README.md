# Week 2 — IAM and Security Foundations

## Least-privilege policy

[`policies/S3UploaderOnly-policy.json`](policies/S3UploaderOnly-policy.json) allows only `s3:PutObject` and `s3:GetObject` for objects under `arn:aws:s3:::my-training-bucket-peggy/*`. I scoped the policy to one bucket instead of all S3 resources so the identity cannot access unrelated data. The `/*` suffix is required because `PutObject` and `GetObject` are object-level actions; the bucket ARN without that suffix refers only to the bucket itself. The policy intentionally excludes bucket listing, object deletion, bucket administration, IAM actions, and access to other AWS services.

## Test identity and verification

I created an IAM user named `s3-test-user` without AWS Management Console access and attached `S3UploaderOnly-peggy` directly to it. I configured its access key locally under the separate `s3test` CLI profile so that testing would not accidentally use my administrator credentials. Running the following command returned the expected `AccessDenied` response because the policy does not allow `s3:ListAllMyBuckets`:

```bash
aws s3 ls --profile s3test
```

This denial confirms least privilege: authentication succeeded, but an action outside the allowed policy was rejected. AWS credentials, account identifiers, and terminal output containing ARNs are intentionally not stored in this repository.

## IAM Access Analyzer

I created a free external-access analyzer named `week2-external-access-analyzer` in `us-east-1`. Its zone of trust is the current AWS account, and the initial scan showed zero active findings. The analyzer will continue checking supported resources for access granted to principals outside the account.

## Access-denied troubleshooting

When an allowed S3 object operation fails, I should verify the active CLI profile, the exact action, and the exact resource ARN before changing permissions. An object policy must use the `/*` suffix, while bucket-level actions such as `s3:ListBucket` require the bucket ARN without that suffix. I should also check for explicit deny statements and use the IAM Policy Simulator rather than testing with an administrator profile.
