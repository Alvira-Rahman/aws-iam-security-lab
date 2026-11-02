# Screenshot Evidence: AWS IAM Security Lab

**Alvira Rahman | IAM Setup, Permission Testing, and Incident Documentation**

This index covers all 14 screenshots: eight from the original repository and six from the supporting case-study package.

[Project overview](../README.md) | [Full troubleshooting case study](../docs/TROUBLESHOOTING.md)

## Setup and Baseline

| Screenshot | What it shows |
|---|---|
| [Baseline IAM dashboard](iam-dashboard-baseline-redacted.png) | Root MFA enabled, no active root access keys, and baseline IAM resource counts at the time of capture. |
| [IAM groups](01-IAM-groups%20created.png) | Admins, Developers, and ReadOnly groups listed in IAM. |
| [IAM users](02-IAM-users-created.png) | admin-alvi, auditor-alvi, and dev-alvi, each showing one group membership. |
| [EC2-trusted role](03-IAM-roles-created.png) | EC2-S3-ReadOnly-Role created, with EC2 shown as its trusted service. |

## Permission Tests

| Screenshot | What it shows |
|---|---|
| [Auditor S3 listing](04-auditor-view-s3.png) | The auditor session displaying objects in the website bucket. |
| [Auditor deletion denied](05-auditor-access-denied-delete.png) | Deletion of error.html denied, with zero successful deletions. |
| [Auditor user creation denied](06-auditor-cannot-create-user.png) | The auditor's iam:CreateUser request denied. |
| [Developer bucket creation](07-dev-created-s3-bucket.png) | Successful creation of dev-alvi-test-bucket-2026 in the developer session. |
| [Developer IAM denials](08-dev-cannot-access-iam.png) | Access denials for three named IAM dashboard actions. |

## Deletion Incident

| Screenshot | What it shows |
|---|---|
| [Website bucket before deletion](s3-bucket-contents-before-deletion.png) | Five top-level entries containing the website files and asset folders. |
| [Deletion confirmation](s3-delete-confirmation-root-session.png) | The permanent-deletion confirmation page with the confirmation phrase entered. |
| [Deletion result](s3-delete-result-15-objects.png) | S3 reporting 15 objects, totaling 4.0 MB, deleted with zero failures. |

## Additional Identity and Security Evidence

| Screenshot | What it shows |
|---|---|
| [Proposed user creation](iam-auditor-create-user-attempt.png) | The proposed Broli user with Admins membership before the denied creation request. |
| [IAM user MFA indicators](iam-users-list-no-mfa.png) | A dash in the MFA column for all three users at the time of capture. |

## Evidence Context

- These are historical lab captures, not a check of current account settings.
- The intended group and policy design is recorded in the case study; complete policy attachments are not shown.
- Role creation and trust configuration do not establish runtime EC2-to-S3 access.
- The deletion evidence does not document a recovery procedure or confirm website availability afterward.

The [full case study](../docs/TROUBLESHOOTING.md) explains the test identities, expected and actual results, incident analysis, diagrams, and planned improvements.
