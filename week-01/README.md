# Week 1 — Cloud Fundamentals & Account Setup

## Status

The local AWS Cloud Engineer environment is ready, and PropertyLite was verified locally in Week 0.

This cohort uses the **Hold My Coffee Free Plan** AWS project rather than a standard standalone AWS root account. Therefore, some handbook steps are not available in this environment:

- Root MFA cannot be configured because IAM > Root access management exposes only curated root actions, not MFA settings.
- The IAM user wizard does not provide console-password creation, so a console administrator user was not created.
- Billing is managed by the Free Plan page instead of the standard AWS Budgets workflow.

## Evidence recorded

- AWS Console access verified.
- Free Plan balance: `$0.00` due and `$100.00` credits remaining at the time of setup.
- Root access management page inspected without selecting or executing destructive actions.
- AWS CLI and Terraform installed locally.

## Concepts

AWS secures the infrastructure that runs its services, while the customer secures the resources and data placed in those services. The root identity has the highest level of control and should not be used for daily work. IAM identities and roles provide controlled access to AWS resources. Regions are separate geographic locations, and Availability Zones are isolated locations within a Region. A budget or credit-limit check is important because cloud resources can continue to incur cost after a terminal window is closed.

## CLI note

The local CLI is installed, but this Free Plan project has not provided a standalone IAM access key for local CLI authentication. Never commit credentials or paste them into GitHub.
