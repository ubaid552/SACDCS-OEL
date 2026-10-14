# Task 1 – Requirement Extraction
## 1.4 Non-Functional Requirements (5)

| Req. ID | Requirement | Type | Priority | Verification Method |
| --- | --- | --- | --- | --- |
| NFR-01 | **Performance:** For 95 % of commands, the time from operator submission to the robot acknowledgement shown at the MCC shall be at most 10 s when one-way link delay is at most 4 s; robot-side validation shall take at most 1 s. | NFR | Medium | Test, Simulation |
| NFR-02 | **Security:** All MCC–robot traffic shall use TLS 1.2 or higher; operator sessions shall expire after 15 min of inactivity; an account shall be locked for 15 min after 5 consecutive failed log-ins; no command shall be executed from an unencrypted channel. | NFR | High | Test, Inspection |
| NFR-03 | **Scalability:** The MCC shall handle the pilot fleet (20 robots serving 20 clinics) with MCC CPU load at most 70 % and telemetry display delay at most 2 s, and shall scale to 100 robots by configuration only (no code change). | NFR | Medium | Test, Analysis |
| NFR-04 | **Reliability:** MCC availability shall be at least 99.5 % per calendar month; robot controller MTBF at least 1,000 operating hours; the chamber shall keep the batch within its profile limits for at least 99.9 % of mission time when no single-point fault is present. | NFR | High | Analysis, Test |
| NFR-05 | **Usability:** A trained operator shall issue a delivery request in at most 60 s and 5 interaction steps; every alarm shall appear within 2 s using text and colour (not colour alone); at least 90 % of trained operators shall complete 5 benchmark tasks without error (SUS score at least 70). | NFR | Medium | Demonstration, Test |
