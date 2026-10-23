# Lessons Learned

## Troubleshooting sequence

| Observation | Evidence | Decision |
| --- | --- | --- |
| The stack deployed successfully | CloudFormation reported `CREATE_COMPLETE` | Test the application separately from resource creation |
| The web page timed out | Browser evidence showed no HTTP response | Analyze the network path before changing resources |
| TCP port 80 was not reachable | Reachability Analyzer identified the security group | Repair the declared ingress rule in CloudFormation |
| The same path became reachable | The second analysis reported `Reachable` | Verify the browser and preserve the evidence |

## Why the fix belongs in code

Changing the security group only in the AWS console would make the live environment differ from the repository. Updating `infrastructure.yaml` keeps the intended configuration reviewable, repeatable, and available for future deployments.

## What I would add in a follow-on project

A production-oriented follow-on would separate public and private tiers, add load balancing and health checks, and introduce monitoring without changing the troubleshooting evidence preserved in this repository.