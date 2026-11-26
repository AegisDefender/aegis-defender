# Evaluation report template

Status: **Template — no test results recorded**

## Run identity

- Report author and date:
- Authorization and scope reference (public-safe identifier):
- Run IDs and repetitions:
- Product edition, build and package hash:
- OS, firewall, applications and integrations:
- Hardware and topology:
- Effective sensor and enforcement modes:
- External reputation/shared-intelligence dependencies:
- Attack framework, model and operator settings, if applicable:

## Method

Describe the baseline, fresh-state/reset procedure, traffic labels, benign controls, attacker objective, independent success observation, connection probe interval and clock uncertainty.

## Results

| Scenario / run | Mode | Detection | Decision | Independent enforcement | Objective succeeded? | Benign impact | Evidence reference |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Not run | — | — | — | — | — | — | — |

## Measurements

Record sample sizes and denominators, detection/decision/enforcement latency, objective success rate, CPU/RAM/backlog and service latency. Separate triggering requests from follow-on requests and rule-file checks from packet-path outcomes.

## Findings

- Observed behavior:
- Unexpected or failed outcomes:
- Not exercised:
- Inconclusive observations:
- Build/configuration-specific limitations:
- Reproduction procedure and sanitized artifact hashes:

## Cleanup

Record restoration of firewall rules, test accounts, synthetic data, shared intelligence and trusted management access.
