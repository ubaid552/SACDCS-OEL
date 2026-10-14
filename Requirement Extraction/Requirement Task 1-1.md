# Task 1 – Requirement Extraction
## 1.3 Functional Requirements (10)

| Req. ID | Requirement | Type | Priority | Verification Method |
| --- | --- | --- | --- | --- |
| FR-01 | Only authenticated operators shall be permitted to issue robot commands. | FR | Critical | Test, Inspection |
| FR-02 | Before executing any command, the robot's command handler shall validate syntax, parameter range, command age (at most 30 s) and permission in the current robot state; an invalid command shall be rejected with an error code and logged within 1 s. | FR | High | Test |
| FR-03 | On a valid DeliveryRequest received in state IDLE, the robot shall enter NAVIGATING and start moving toward the destination clinic within 2 s; a DeliveryRequest in any other state shall be rejected with REJECT_BUSY. | FR | High | Test, Simulation |
| FR-04 | Within 500 ms of ObstacleDetected while moving, the robot shall stop forward motion and enter AVOIDING_OBSTACLE; it shall resume its previous task only after the obstacle has been absent for 2 s continuously, and shall never deliver while avoiding. | FR | High | Test, Simulation |
| FR-05 | The robot shall enter Safe Mode when a critical battery or thermal condition is detected. | FR | Critical | Test, Simulation |
| FR-06 | The robot shall enter DELIVERING only from NAVIGATING after DestinationReached (within 5 m of the clinic position); it shall release the chamber door only after an authorised hand-over confirmation, then travel back (RETURNING) and become IDLE on arrival at the warehouse. | FR | High | Test, Demonstration |
| FR-07 | When chamber temperature or humidity leaves the batch profile limits for more than 5 s, the chamber controller shall start correction within 5 s and shall declare recovery only after at least 3 consecutive in-range readings from the sensors within the 300 s recovery period. | FR | High | Test, Simulation |
| FR-08 | The robot shall send telemetry (state, position, battery level, chamber temperature, humidity, door status, power source) to the MCC every 10 s and within 2 s of every state change. | FR | Medium | Test |
| FR-09 | The system shall log every command received, authentication result, execution result, state transition and alarm with timestamp (accuracy ±1 s), operator ID and robot ID, and keep the log for at least 12 months; a log-write failure shall raise an operator alert. | FR | High | Test, Inspection |
| FR-10 | The system shall support communication with multiple robots simultaneously. | FR | High | Test |

