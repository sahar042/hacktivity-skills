---
name: logging-monitoring
description: "Insufficient Logging & Monitoring offensive playbook from 25 disclosed HackerOne reports (24 medium, 1 low). Use when hunting or reviewing insufficient logging & monitoring. Triggers: endpoints, cloudtrail, service, non-production, api."
license: "For authorized security testing and education only."
---

# Insufficient Logging & Monitoring

> Distilled from **25** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Security-relevant actions aren't logged, or logs omit who/what/when  -  enabling silent recon, privilege enumeration, or undetectable abuse (common in cloud APIs that skip CloudTrail).

## Where to hunt

- Perform sensitive actions (failed auth, permission probes, key use, admin changes) and check whether audit/CloudTrail/app logs record them.
- Compare prod vs non-prod / alternate API endpoints for logging gaps.

## Exploitation playbook

- Enumerate permissions or abuse features on endpoints that don't emit audit events.
- Operate in the blind spot of detection rules that depend on those logs.

## Bypass techniques

- Non-production or alternate regional endpoints; APIs that return errors without audit entries.

## Impact & escalation

- Invisible credential testing and lateral movement; delayed incident response.

## Remediation

- Log authz failures and admin actions everywhere, including non-prod parity; alert on enumeration patterns; never rely on a single telemetry path.

## Concrete payloads & PoCs

_No high-confidence PoC snippets were extracted from the writeups in this class. Open the top disclosed examples and their full report bodies for manual payloads._

## Recurring patterns in this dataset

Most frequent terms across the 25 reports (term (count)): `endpoints` (57), `cloudtrail` (54), `service` (45), `non-production` (42), `api` (42), `enumeration` (39), `permission` (38), `silent` (33), `log` (31), `resulting` (26), `credentials` (26), `aws` (20), `fail` (17), `logs` (15), `found` (15), `iam` (15), `standard` (14), `generating` (13)

## Worked example  -  [report #3022516](https://hackerone.com/reports/3022516)

*Non-Production API Endpoints for the Forecast Service Fail to Log to CloudTrail Resulting in Silent Permission Enumeration* (medium,  - )

> Summary: Typically, when an adversary gains access to stolen AWS IAM credentials they will frequently test those credentials to see what access they have. They do this by performing API calls and seeing which succeed and which fail. There are even automated tools to make this process easier. For defenders and security professionals, this behavior serves as a golden opportunity for detection as it likely involves generating a large number of failed API call attempts. If an adversary could enumerate permissions without logging to CloudTrail, they could perform this activity invisibly. There are many categories of CloudTrail bypass. The specific variant we will be focussed on in this report ha…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#3022516](https://hackerone.com/reports/3022516) | medium |  -  | aws_vdp | Non-Production API Endpoints for the Forecast Service Fail to Log to CloudTrail Resulti… |
| [#3780277](https://hackerone.com/reports/3780277) | medium |  -  | aws_vdp | Non-Production API Endpoints for the Amazon S3 Tables Service Fails to Log to CloudTrai… |
| [#3014785](https://hackerone.com/reports/3014785) | medium |  -  | aws_vdp | (Part 2) Non-Production API Endpoints for the Datazone Service Fail to Log to CloudTrai… |
| [#2981210](https://hackerone.com/reports/2981210) | medium |  -  | aws_vdp | Non-Production API Endpoints for the Datazone Service Fail to Log to CloudTrail Resulti… |
| [#3009411](https://hackerone.com/reports/3009411) | medium |  -  | aws_vdp | Non-Production API Endpoints for the DocumentDB Elastic Service Fail to Log to CloudTra… |
| [#3021451](https://hackerone.com/reports/3021451) | medium |  -  | aws_vdp | Non-Production API Endpoint for the ElastiCache Service Fails to Log to CloudTrail Resu… |
| [#2890071](https://hackerone.com/reports/2890071) | medium |  -  | nextcloud | admin_audit does not log actions on files in a group folder |
| [#2800091](https://hackerone.com/reports/2800091) | medium |  -  | aws_vdp | Non-Production API Endpoints for the bedrock-agent Service Fail to Log to CloudTrail Re… |

*See [reference.md](reference.md) for all 25 reports in this class.*
