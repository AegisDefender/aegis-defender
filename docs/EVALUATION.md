# Evaluation guide

## Objective

Measure whether Aegis detects relevant attack behavior, makes appropriate decisions, enforces them effectively, and interrupts attack objectives while preserving legitimate access.

This is a proposed evaluation protocol. No results are asserted here. An ARTEX-style scenario tests specified techniques; a direct ARTEX test additionally requires identifying the framework version, model, tools and operator instructions.

## 1. Establish the environment

Use systems and traffic sources covered by written authorization. Define target hosts, source addresses, services, permitted techniques, rate limits, test windows, stop conditions and recovery owners. Use isolated test infrastructure and synthetic accounts/data. Keep a separate trusted management path and restorable snapshots.

Obtain the commercial evaluation build from [Aegis](https://aegiscds.com/contact-us). This documentation repository contains no installer. Confirm supported OS, firewall, applications, log formats and privileges with Aegis; use supplied installation instructions rather than guessed commands.

Record:

- Exact product/build identifiers, package hashes, edition and installation date.
- OS, firewall backend, application and integration versions, host resources and network topology.
- Each sensor's effective state and policy: observe, alert, temporary/permanent block, or disabled.
- Allow/ignore rules; escalation mode; mail windows; optional reputation, WAF, Splunk and shared-intelligence settings.
- Log availability, trusted client-IP handling behind proxies, clock synchronization and timestamp precision.
- Initial firewall state and the independent observation method for application access and attack success.

Never assume that enabling one feature enables all sensors or enforcement paths.

## 2. Establish comparable baselines

Replay the same labeled benign and attack traffic against equivalent fresh environments with and without the evaluated Aegis configuration. Keep application patch levels and other security controls equivalent. If a WAF is enabled, record it in both conditions or report separate conditions to attribute results correctly.

Begin with observation mode to confirm parsing, application context and event collection. Then reset state and run the enforcement condition. Test broader network escalation separately in an isolated network containing only authorized sources.

Record both benign workflows and successful attack objectives independently of Aegis logs. A log replay can assess detection logic but cannot prove that a live packet was blocked or an exploit prevented.

## 3. Run the scenario matrix

| Scenario | Evaluation question | Evidence to collect |
| --- | --- | --- |
| CMS reconnaissance | Does context distinguish installed routes, mismatched probes and normal admin navigation? | Application map, labeled requests, decisions and successful benign navigation. |
| Persistent reconnaissance | Are sustained low-rate probes recognized over the intended window? | Timestamped sequence, retained state, decision time and follow-on reachability. |
| Web exploit attempts | Do controlled SQLi, command-injection, traversal and webshell-probe cases produce the expected decisions? | Actual inspected fields, WAF state, detector events and application-side outcome. |
| Distributed web campaign | Does the qualifying attack family correlate across controlled sources? | Source/site/route relationships, participant action records and independent connectivity checks. |
| Service authentication | Do supported SSH, panel and FTP sensors interpret failures and legitimate activity correctly? | Service logs, sensor modes, decisions and valid-user access results. |
| Rotating-IP mail campaign | Are attempts against synthetic accounts linked across sources and configured 1/6/24-hour windows? | Account-safe identifiers, correlation state, actions and legitimate roaming-user controls. |
| Host visibility | Are controlled critical-file changes and suspicious web-process descendants observed? | File/runtime/privilege events and observation latency; score these as monitoring. |
| Firewall enforcement | Do exact-IP temporary/permanent decisions affect the actual test path? | Command outcomes, file/live-rule checks, independent connections, expiry and cleanup. |
| Network escalation | Do evidence and allow/ignore safeguards constrain broader action? | Dry-run candidates, route context, isolated apply results and unaffected trusted traffic. |
| Firewall recovery | Does controlled deny-file rule loss trigger guarded restoration? | Baseline, confirmation events, forensic copy, recovered state and packet-path checks. |
| Operations and resilience | What happens during rotation, restart, input loss, backlog or firewall errors? | Health snapshots, source gaps, resource usage, recovery behavior and operator visibility. |
| Shared intelligence, if supplied | Do publish, expiry and withdrawal operate through the configured components? | Provenance, transport validation, owned rules, withdrawal results and local behavior during disconnect. |

## 4. Evaluate an adaptive attack sequence

Use a representative authorized chain: discovery, endpoint probing, controlled exploitation attempts, authentication attempts and follow-on access. Define the attacker's objective in advance with a harmless marker or synthetic record. Include controlled source rotation and legitimate traffic in the same run.

For actual ARTEX use, record the exact fork/commit, model/provider/version where available, prompts, tool permissions, rate limits, budgets and human interventions. Keep model/API credentials and raw sensitive transcripts out of the public report. Confirm that sending test data to external model services is within the authorization.

Repeat runs from fresh snapshots. Mark the first triggering request separately from later attempts. Determine whether the objective succeeded, when Aegis acted, and which controls caused any interruption. Report variation across runs, including failed or inconclusive runs.

## 5. Measure outcomes

| Metric | Definition |
| --- | --- |
| Objective success rate | Runs in which the independently observed attacker objective succeeded / eligible runs. |
| Detection coverage | Labeled malicious cases with matching detections / malicious cases submitted; identify missing input visibility. |
| Detection latency | Detection timestamp minus independently recorded event timestamp. |
| Decision latency | Policy decision timestamp minus detection timestamp. |
| Enforcement latency | First independently confirmed blocked test connection minus policy decision timestamp. Use bounded probe intervals and report their precision. |
| Follow-on interruption | Subsequent malicious requests or connections blocked after the decision; distinguish already-covered sources from new detections. |
| Benign impact | Legitimate transactions or sources incorrectly blocked / corresponding benign transactions or sources tested. Report each denominator separately. |
| Operational cost | CPU, RAM, backlog and request latency under a documented load profile. |
| Recovery outcome | Observed rule restoration, source continuity, expiry and withdrawal results for each tested failure. |

Report counts, denominators, median and tail latency where sample size permits, clock uncertainty, and probe intervals. A firewall entry is not an independently verified block. A detected request is not necessarily a prevented exploit.

## 6. Report and restore

Use the [report template](EVALUATION-REPORT.md). Label every claim as observed, not exercised or inconclusive. Keep supplied product features separate from roadmap items. Do not generalize a Linux test to Windows, all editions, every ARTEX fork, or an incident whose entry path is unknown.

Stop generators, withdraw test intelligence, restore approved firewall and application state, verify trusted access, and retain protected evidence for review. Publish only sanitized results with versions, effective modes, methodology and enough information to reproduce the scenario.
