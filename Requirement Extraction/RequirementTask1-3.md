# Task 1 – Requirement Extraction
## High-Risk (Safety) Requirements (4)

| Req. ID | Requirement | Type | Priority | Verification Method |
| --- | --- | --- | --- | --- |
| SR-01 | **Railway crossing:** The robot shall enter a level-crossing only when ARLCCS reports Barrier_Open = TRUE, Train_Approaching = FALSE and Train_Present = FALSE with data not older than 2 s; otherwise it shall stop at least 5 m before the crossing line. On ARLCCS sensor failure, barrier failure, communication loss or inconsistent readings the crossing shall be treated as unsafe. | Safety | Critical | Simulation, Test, Analysis |
| SR-02 | **Link loss:** If no MCC heartbeat is received for 15 s, the robot shall stop within 3 s and enter LINK_LOST, keep chamber conservation active, never enter a railway crossing, reject commands older than 30 s, and return to the warehouse autonomously after 120 s without link. | Safety | Critical | Test, Simulation |
| SR-03 | **Chamber door:** If the chamber door opens during conservation, normal operation shall be suspended within 1 s and an operator alert sent within 5 s; normal operation shall resume only after the door is closed and latched, all essential sensors are healthy and temperature and humidity stay within limits for 60 s. | Safety | Critical | Test, Demonstration |
| SR-04 | **Critical battery:** When battery capacity is at most 20 % (CriticalBattery), the robot shall abandon the delivery and start returning within 2 s from NAVIGATING or AVOIDING_OBSTACLE; from DELIVERING it shall complete or abort hand-over within 60 s and then return; it shall never start a new mission while capacity is at most 20 %. | Safety | Critical | Test, Simulation |
