# Task 2 – Change Requests & Traceability Matrix (RTM)
## 2.1 Version-Controlled Change Log

| Version | CR | Req. ID | Status | Old text | New text | Reason | Git tag / commit |
| --- | --- | --- | --- | --- | --- | --- | --- |
| v1.1 | CR-01 | FR-05 | **Modified** | The robot shall enter Safe Mode when a critical battery or thermal condition is detected. | The robot shall enter Safe Mode within 3 seconds when chamber or battery temperature exceeds the critical threshold or battery capacity falls below the emergency level. | Mission Control needs a time limit and defined thresholds so that vaccines and battery are protected predictably. | `v1.1-CR01` / `<commit hash>` |
| v1.2 | CR-02 | FR-10 | **Modified** | The system shall support communication with multiple robots simultaneously. | The system shall support at least 20 simultaneously connected robots. | The pilot serves 20 clinics, so the fleet size must be a fixed, testable number. | `v1.2-CR02` / `<commit hash>` |
| v1.3 | CR-03 | FR-01 | **Modified** | Only authenticated operators shall be permitted to issue robot commands. | The system shall require authenticated and role-authorised operators before accepting any robot command. | Authentication proves identity only; a role check is needed so that, for example, a viewer cannot send commands. | `v1.3-CR03` / `<commit hash>` |

## 2.2 Rewritten Requirements 

| Req. ID | Requirement | Type | Priority | Verification Method | Status |
| --- | --- | --- | --- | --- | --- |
| FR-01 | The system shall require authenticated and role-authorised operators before accepting any robot command. | FR | Critical | Test, Inspection | **Modified** (CR-03) |
| FR-05 | The robot shall enter Safe Mode within 3 seconds when chamber or battery temperature exceeds the critical threshold or battery capacity falls below the emergency level. | FR | Critical | Test, Simulation | **Modified** (CR-01) |
| FR-10 | The system shall support at least 20 simultaneously connected robots. | FR | High | Test | **Modified** (CR-02) |

**Glossary added by the CRs:** critical chamber temperature = below 0.0 °C or above 10.0 °C; critical battery temperature = above 60 °C; emergency battery level = capacity below 10 %. (`CriticalBattery` at 20 % is a different, earlier event that causes a return to the warehouse, SR-04.)

## 2.3 Why the New Wording Is More Measurable or Testable

| CR | Weakness of the original | Improvement in the new wording | How it is tested (pass/fail) |
| --- | --- | --- | --- |
| CR-01 | "Critical" was undefined and there was no time limit, so any delay would pass. | Adds a **time bound (3 s)**, names the **three trigger conditions** (chamber temperature, battery temperature, battery capacity) and a measurable "emergency level". | Inject each condition; measure time between condition timestamp and SAFE_MODE log entry; pass if at most 3 s. Boundary tests at the threshold value (TC-06, TC-07, TC-08). |
| CR-02 | "Multiple" has no upper or lower limit; even 2 robots would satisfy it. | Gives a **numeric minimum (20)**, matching the pilot fleet. | Connect 20 simulated robots at the same time for 1 h; pass if all stay connected and send telemetry every 10 s; boundary test with 19, 20 and 21 robots (TC-12, TC-13). |
| CR-03 | "Authenticated" checks identity only; permission is not specified, and "permitted" does not say **when** the check happens. | Adds **role authorisation** and the **order of checking** ("before accepting"). | Decision-table test with four combinations (authenticated Yes/No × authorised Yes/No); only Yes/Yes is accepted; check the log shows the rejection reason (TC-02, TC-03). |

## 2.4 Impact Analysis of the Change Requests

| CR | Directly modified | Related requirements | Related model elements | Constraint |
| --- | --- | --- | --- | --- |
| CR-01 | FR-05 | SR-04, NFR-04 | ST-06; T19–T24; OP-21, OP-07, OP-14 | C-10 |
| CR-02 | FR-10 | NFR-03, FR-08, NFR-01 | OP-22, OP-24 | – |
| CR-03 | FR-01 | FR-02, NFR-02, FR-09 | T16, T17, T25, T26, T35, T38, T39; OP-18 | C-12 |

## 2.5 Multi-Layer Requirements Traceability Matrix (RTM)

Layers: Requirement → State / Transition → Operation → Constraint → Test Case → Risk Level.

| Req. ID | State / Transition | Operation | Constraint | Test Case | Risk Level |
| --- | --- | --- | --- | --- | --- |
| FR-01 | ST-01..ST-07; T16, T17, T25, T26, T35, T38, T39 | OP-18 | C-12 | TC-01, TC-02, TC-03, TC-04, TC-20 | Critical |
| FR-02 | T01, T16, T17, T35 | OP-18 | C-12 | TC-01, TC-04 | High |
| FR-03 | ST-01, ST-02; T01, T13, T16, T17, T38, T39 | OP-19 | C-11 | TC-01, TC-10 | High |
| FR-04 | ST-02, ST-03; T02, T03, T10, T11, T12, T14 | OP-20 | C-11 | TC-05, TC-11 | High |
| FR-05 | ST-06; T19–T25, T15 | OP-21, OP-07, OP-14 | C-10 | TC-06, TC-07, TC-08, TC-20 | Critical |
| FR-06 | ST-02, ST-04, ST-05, ST-01; T04, T05, T06, T13, T14 | OP-16, OP-19 | C-09, C-11 | TC-01, TC-10, TC-11 | High |
| FR-07 | CH-04, CH-05, CH-06 | OP-04, OP-05, OP-06, OP-07 | C-10 | TC-14 | High |
| FR-08 | ST-01..ST-07 | OP-22 | – | TC-19, TC-12 | Medium |
| FR-09 | ST-01..ST-07 (every transition) | OP-17, OP-09 | C-12 | TC-19, TC-02 | High |
| FR-10 | – | OP-22, OP-24 | – | TC-12, TC-13 | High |
| NFR-01 | T01 | OP-18 | – | TC-01, TC-04 | Medium |
| NFR-02 | – | OP-18 | C-12 | TC-02, TC-03 | High |
| NFR-03 | – | OP-22 | – | TC-12, TC-13 | Medium |
| NFR-04 | CH-04, CH-05, CH-08 | OP-04, OP-05, OP-14 | C-10 | TC-14, TC-18 | High |
| NFR-05 | – | OP-09 | – | TC-21 | Medium |
| SR-01 | ST-02, ST-05; T36, T37 | OP-23 | C-01 to C-07 | TC-16, TC-17 | Critical |
| SR-02 | ST-07; T24, T27–T35 | OP-24 | C-08, C-12 | TC-18, TC-04 | Critical |
| SR-03 | CH-04 → CH-07; ST-06; T20, T21, T23 | OP-12, OP-13, OP-09 | C-09, C-13 | TC-15 | Critical |
| SR-04 | ST-02..ST-05; T07, T08, T09, T18 | OP-19, OP-21 | C-10, C-11 | TC-09, TC-06 | Critical |

**Risk level:** Critical = failure can cause injury, collision or loss of vaccine batch; High = mission failure or security breach; Medium = degraded service.

## 2.6 Test Cases (21)

**Scenario flow used for traceability:** Step 1 command received → Step 2 authenticated (and authorised) → Step 3 executed → Step 4 status reported → Step 5 logged.

| TC ID | Title | Scenario step(s) | Input / action | Expected result | Covers |
| --- | --- | --- | --- | --- | --- |
| TC-01 | Valid mission end-to-end | 1–5 | Authorised operator sends DeliveryRequest; robot in IDLE; no faults | Accepted; NAVIGATING within 2 s (T01); DELIVERING at destination (T04); RETURNING (T05); IDLE (T06); telemetry and log entries for every step | FR-01, FR-02, FR-03, FR-06, FR-09, NFR-01 |
| TC-02 | Unauthenticated command | 1, 2 | Send command with no session or expired session | Rejected (REJECT_AUTH) within 1 s; no state change; rejection logged | FR-01, FR-09, NFR-02, C-12 |
| TC-03 | Authenticated but unauthorised role | 1, 2 | Viewer role sends DeliveryRequest | Rejected (REJECT_ROLE); robot unchanged; log shows operator ID and reason | FR-01 (CR-03), NFR-02, C-12 |
| TC-04 | Stale command (link delay) | 1, 2, 5 | Valid command with timestamp 45 s old | Rejected (REJECT_STALE); logged; robot unchanged | FR-02, SR-02, NFR-01, C-12 |
| TC-05 | Obstacle handling | 3, 4 | Obstacle injected while NAVIGATING, then while RETURNING; removed for 2 s | AVOIDING_OBSTACLE within 500 ms (T02, T10); resume to correct target (T03, T11); telemetry reports each change | FR-04, T02, T03, T10, T11 |
| TC-06 | Safe Mode – battery emergency | 3, 4, 5 | Battery set to 9 % in NAVIGATING, AVOIDING_OBSTACLE, DELIVERING, RETURNING | SAFE_MODE within 3 s in every state (T20–T23); alert sent; logged | FR-05 (CR-01), C-10 |
| TC-07 | Safe Mode – temperature | 3, 4, 5 | Chamber temperature set to 10.5 °C; separately battery temperature 61 °C | SAFE_MODE within 3 s; alert; logged | FR-05 (CR-01), C-10 |
| TC-08 | Safe Mode – boundary values | 3 | Battery exactly 10 %, then 9.9 %; chamber 10.0 °C, then 10.1 °C | At the threshold: no Safe Mode; just beyond: SAFE_MODE within 3 s | FR-05 (CR-01) |
| TC-09 | CriticalBattery in every state | 3, 4 | Battery 20 % in NAVIGATING, AVOIDING_OBSTACLE, DELIVERING, IDLE; two events at once | NAVIGATING and AVOIDING_OBSTACLE → RETURNING within 2 s (T07, T08); DELIVERING completes or aborts within 60 s then RETURNING (T09); IDLE blocks new missions (T18); priority rule applied | SR-04, T07, T08, T09, T18 |
| TC-10 | Illegal request and transition suite | 1, 3 | DeliveryRequest and DestinationReached injected in IDLE; DeliveryRequest in all other states | Never DELIVERING from IDLE (T13); non-IDLE requests rejected REJECT_BUSY (T16, T17, T38, T39) | FR-03, FR-06, T13, C-11 |
| TC-11 | Avoiding-obstacle faults | 3 | DestinationReached while AVOIDING_OBSTACLE; obstacle never cleared for 120 s | No DELIVERING (T14); after 120 s RETURNING and operator alert (T12) | FR-04, T12, T14, C-11 |
| TC-12 | 20 simultaneous robots | 1–5 | 20 simulated robots connected for 1 h, telemetry every 10 s, 1 command each | All connected; no telemetry loss; MCC CPU at most 70 %; display delay at most 2 s | FR-10 (CR-02), NFR-03, FR-08 |
| TC-13 | Fleet boundary (19, 20, 21 robots) | 1 | Connect 19, 20 and then 21 robots | 19 and 20 work; 21st is handled gracefully (accepted or clearly rejected) without affecting the first 20 | FR-10 (CR-02), NFR-03 |
| TC-14 | Chamber correction verified by sensors | 3, 4, 5 | Set temperature to 9 °C: (a) cooler works; (b) cooler disabled | (a) CONSERVING after 3 consecutive in-range readings within 300 s; (b) PROTECTION at 300 s, light reduced, alert within 5 s | FR-07, NFR-04, OP-05, OP-07 |
| TC-15 | Door open during conservation | 3, 4, 5 | Open door while NAVIGATING; open door in DELIVERING with authorised hand-over | Moving: chamber SUSPENDED within 1 s, alert within 5 s, robot SAFE_MODE (T20). DELIVERING: allowed. No auto-resume; resume only after OP-13 checks | SR-03, C-09, C-13, OP-12, OP-13 |
| TC-16 | Railway crossing entry rule | 3, 4, 5 | ARLCCS simulator: barrier closed; train approaching; train present; barrier open and clear | Robot holds at least 5 m before line unless Barrier_Open and no train (T36, T37); enters only when clear; every case logged | SR-01, C-01 to C-05 |
| TC-17 | Crossing sensor failure / disagreement | 3, 4, 5 | Fail one crossing sensor; sensors A and B disagree; stale ARLCCS data (3 s) | Crossing treated as unsafe; robot holds; alert; logged | SR-01, C-06, C-07 |
| TC-18 | Link loss and recovery | 3, 4, 5 | Stop MCC heartbeat for 15 s in IDLE, NAVIGATING, AVOIDING_OBSTACLE, DELIVERING, RETURNING, SAFE_MODE; restore after 30 s; another run without restore for 120 s | LINK_LOST with stop within 3 s (T28–T31); deferred in AVOIDING (T32); SAFE_MODE unaffected (T27); resume (T33); after 120 s RETURNING (T34); no crossing entry | SR-02, NFR-04, C-08 |
| TC-19 | Telemetry and log completeness | 4, 5 | Run TC-01 and TC-06; compare MCC display and log with the real event sequence | Telemetry every 10 s and within 2 s of state change; every command, authentication result, transition and alarm logged with timestamp, operator ID, robot ID | FR-08, FR-09 |
| TC-20 | Safe Mode exit control | 1, 2, 3 | Safe Mode reset by unauthorised role, by authorised role with conditions still bad, and by authorised role with conditions normal; DeliveryRequest during SAFE_MODE | Only the last reset works and leads to IDLE (T25); never directly to NAVIGATING or DELIVERING (T15); request rejected (T26) | FR-05, FR-01, T15, T25, T26 |
| TC-21 | Operator usability | 1, 4 | 10 trained operators perform 5 benchmark tasks (issue delivery, read alarm, etc.) | Delivery request in at most 60 s and 5 steps; alarm visible within 2 s with text and colour; at least 90 % without error; SUS at least 70 | NFR-05 |

## 2.7 Test Cases to Re-run After Each Change Request

**Must re-run** = directly tests the changed requirement. **Regression** = interacts with it.

| CR | Must re-run | Regression (also re-run) | Reason |
| --- | --- | --- | --- |
| CR-01 (FR-05) | TC-06, TC-07, TC-08, TC-20 | TC-05, TC-09, TC-14, TC-15, TC-18 | New 3 s limit and thresholds; other tests can trigger Safe Mode or depend on state behaviour. |
| CR-02 (FR-10) | TC-12, TC-13 | TC-01, TC-18, TC-19 | New fleet size; mission, link handling and logging must still work under 20 robots. |
| CR-03 (FR-01) | TC-01, TC-02, TC-03 | TC-04, TC-10, TC-19, TC-20, TC-21 | Role check changes command acceptance, log content and Safe Mode reset. |

## 2.8 Coverage of the Scenario Flow

| Scenario step | Test cases |
| --- | --- |
| 1. Command received | TC-01, TC-02, TC-03, TC-04, TC-10, TC-13, TC-20, TC-21 |
| 2. Authenticated and authorised | TC-01, TC-02, TC-03, TC-04, TC-20 |
| 3. Executed | TC-01, TC-05, TC-06, TC-07, TC-08, TC-09, TC-10, TC-11, TC-14, TC-15, TC-16, TC-17, TC-18 |
| 4. Status reported | TC-01, TC-05, TC-06, TC-09, TC-12, TC-19, TC-21 |
| 5. Logged | TC-01, TC-04, TC-06, TC-12, TC-19 |

## 2.9 Completeness Check

| Task requirement | Satisfied |
| --- | --- |
| Rewrite affected requirements and mark Modified with old text, new text, reason | Sections 2.1 and 2.2 |
| Explain why new wording is more measurable or testable | Section 2.3 |
| Multi-layer RTM (Req → State → Operation → Constraint → Test → Risk) | Section 2.5 |
| At least 8 test cases traceable to scenario steps | Section 2.6 (21 test cases) |
| Test cases to re-run per CR | Section 2.7 |
