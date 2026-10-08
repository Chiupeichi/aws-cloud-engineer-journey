# Week 2 — IAM & Security Foundations

## Policy exercise

`policies/S3UploaderOnly-policy.json` allows only `s3:PutObject` and `s3:GetObject` for objects inside the specifically named training bucket. It does not allow listing buckets, deleting objects, changing bucket settings, or accessing any other bucket. The `/*` suffix is required because these are object-level permissions; the bucket ARN by itself refers to the bucket resource, not the objects inside it.

## Expected least-privilege test

With a separate low-privilege profile, this command should be denied because the policy does not include `s3:ListAllMyBuckets` or `s3:ListBucket`:

```bash
aws s3 ls --profile s3test
```

That denial is expected and demonstrates least privilege. Do not test this with an administrator identity, and do not create or commit access keys in this repository.

## Environment note

The Hold My Coffee Free Plan environment does not expose the same IAM-user credential workflow as a standalone AWS account. The policy file is preserved as the Week 2 design exercise; it has not been represented as a completed live deployment unless the separate `s3test` identity and training bucket are actually created and verified.
