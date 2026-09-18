# Software Requirements Specification (SRS)

Project: Smart Parking Platform

Version: 1.1

Date: 09.17.2026

## 1. Introduction

### 1.1 Purpose

This document defines the requirements for the $oftware ¢orp. Smart Parking Platform. It describes the systems users, functional behavior, quality expectations, business rules, and use cases that will later assist us in our estimations, scheduling, design, and implementation.

### 1.2 Scope

The Smart Parking Platform is a double sided parking management solution. The drivers use a mobile application to locate the participating parking facilities, view the availability and rates, reserve parking, make digital payments, receive direction to the facility, gain entry, manage sessions, and view receipts. Parking operators and administrators use a web portal to configure facilities, map the inventory, manage pricing, review reports, and override and manage access. The background processes include removing unused reservations and sending expiration alerts.

### Explicitly Out of Scope

- Physical manufacturing, installation, or hardware maintenance of parking barrier gates, optical scanners, and IoT floor sensors
- Municipal traffic citation enforcement, parking ticket violation processing, and legal collections
- On-site valet or physical attendant staffing operations

## 2. Overall Description

Users: The finished Smart Parking Platform will have several different types of users. Including drivers, parking facility operators and system administrators.

System Environment: The Smart Parking Platform will use both a mobile and web-based environment.

Constraints: The system depends on several outside technologies. Users have to authenticate before they reach protected features, drivers need a supported mobile device, and location based features only work when GPS permissions are granted. Payments run on Stripe. Facilities that want real-time occupancy have to connect compatible sensors to the platform, and QR entry needs compatible scanners and gate hardware. The system also protects sensitive user, payment, and administrative data, and limits administrative features by role.

Assumptions: The Smart Parking Platform assumes that users have reliable internet access while using the application. It also assumes that parking facilities have internet-connected equipment that can communicate with the platform. Drivers are expected to provide account and vehicle information and allow location access when using location-based features. The system assumes that external services such as payment, mapping, messaging, and garage hardware systems are available when their features are needed. It is also assumed that parking operators will keep facility information, pricing rules, operating hours, and parking inventory configurations up to date.

### Evaluation of existing software solutions

- ParkMobile / PayByPhone: Market leaders in municipal and on-street parking. They are widely used and make mobile parking payments convenient, but they mainly track paid parking time rather than whether a vehicle is physically still occupying the space. This can make availability information less accurate.
- SpotHero / ParkWhiz: Strong competitors in off-street garage reservations and advance parking passes. They are useful for pre-booking, but they generally rely more on reserved inventory than direct integration with garage hardware such as barrier gates and live IoT parking sensors.
- Passport Enterprise: A comprehensive municipal parking and enforcement platform with strong backend capabilities. However, it is more focused on administration and enforcement, while the driver experience is less central. It also does not emphasize features such as turn-by-turn navigation and a fully connected driver journey.
- Our Smart Parking Platform: Our solution is designed to connect the driver experience with real-time garage operations. The main difference is the combination of live parking availability, IoT sensor data, garage gate integration, reservations, payments, navigation, and parking-session management within one platform.

## 3. Functional Requirements

- FR1: The system shall allow drivers to create an account and save their basic vehicle information.
- FR2: The system shall verify new driver account by sending a verification code through SMS.
- FR3: The system shall allow drivers to use their current location to search for nearby parking facilities.
- FR4: The system shall show drivers current parking availability, parking rates, operating hours, and available parking types for each facility.
- FR5: The system shall allow drivers to reserve available parking for a selected arrival and departure time.
- FR6: The system shall temporarily hold the selected parking availability during checkout so another driver cannot reserve the same availability at the same time.
- FR7: The system shall allow drivers to make digital payment's through Stripe using the supported payment methods.
- FR8: The system shall generate a QR entry credential after a reservation has been successfully paid for.
- FR9: The system shall provide directions to the selected parking facility through a supported mapping and location service.
- FR10: The system shall allow drivers to check in at a parking facility by scanning their reservation QR code at the entrance.
- FR11: The system shall update the reservation from Reserved to checked in after an entry and update the facility's occupancy information.
- FR12: The system shall allow drivers to extend a parking session when more time and parking capacity is available.
- FR13: The system shall process any additional payment required when a driver extends a parking session.
- FR14: The system shall allow drivers to view their previous parking sessions, transactions, and reservations.
- FR15: The system shall allow drivers to generate and download PDF receipts for previous parking transactions.
- FR16: The system will allow parking operators to create, read, update and delete when needed, facility information such as capacity, parking types, operating hours, floors, and sensor maps.
- FR17: The system shall allow parking operators to create and manage dynamic pricing rules based on conditions such as demand and current occupancy.
- FR18: The system shall allow operators and finance personnel to view and export garage occupancy and revenue reports.
- FR19: The system shall allow attendants to manually open a parking gate when a QR check-in process fails.
- FR20: The system shall record gate overrides, including the employee, time, vehicle information, and reason for the action.
- FR21: The system will allow administrators to modify user roles and permissions and suspend or revoke employee access using role based access.
- FR22: The system shall make reservations automatically expire when the driver does not check in within the grace period and return that parking capacity to available inventory.
- FR23: The system shall automatically warn drivers when an active parking session is approaching its expiration time and allow them to return to the app to extend the session when permitted.

## 4. Non-Functional Requirements

- NFR1: Authentication - The system will require users to authenticate before accessing protected driver, operator, finance, or administrative functions.
- NFR2: Authorization - The system shall use role based access control to restrict system functions based on each user's role.
- NFR3: Connectivity - The system shall require network connectivity for functions that are dependent on real time parking information, payments, notifications, and more.
- NFR4: Hardware Compatibility - The system shall support compatible parking sensors, QR scanners, gate controllers, and other approved hardware.
- NFR5: Data Consistency - The system shall maintain consistent reservation, payment, check-in, occupancy, and parking availability information across the full protfolio.
- NFR6: Security - The system shall protect sensitive information during transmission and storage.
- NFR7: Payment Security - The system shall process digital payments through the approved payment provider and will avoid storing unnecessary payment information.
- NFR8: Usability - The driver mobile application shall provide a graphical user interface for searching, reserving, paying for, entering, and managing parking sessions.
- NFR9: Administrative Usability - The operator web portal shall organize facility management, pricing, reporting, gate controls, and access-management functions in an accessible interface.
- NFR10: Mobile Compatibility - The mobile application shall operate on supported mobile devices that provide internet access, location services, QR-code display capability, and push-notification support.
- NFR11: Web Compatibility - The operator and administrative portal shall operate through the platform's supported modern web browsers.
- NFR12: Integration - The system shall support communication with external payment, mapping, notification, sensor, scanner, and gate-control services.
- NFR13: Auditability - The system shall maintain records of administrative actions, including gate overrides and access-control changes.
- NFR14: Scalability - The system shall be designed to support additional users, parking facilities, reservations, and connected devices without requiring a complete redesign and completely new infrastructure.
- NFR15: Maintainability - The system shall allow facility information, pricing rules, integrations, and configurable system settings to be updated without rebuilding the entire platform.
- NFR16: Privacy - The system shall access driver location information only when a location based task is required and the user has granted the appropriate permission.
- NFR17: Reliability - The system shall preserve completed reservation, payment, check-in, and administrative transaction records if an individual external service temporarily becomes unavailable.
- NFR18: Availability - The system shall be available to users during the supported operating periods of participating parking facilities.

## 5. Use Case Example

Category A: Driver and Mobile Application Interactions

### UC-01: User Account Registration and Profile Setup

- Actor: Driver
- Precondition: The mobile application is installed on the driver's device and the device has internet access.

Steps:

1. The driver launches the mobile application and selects "Register New Account".
2. The driver enters an email address, password, phone number, vehicle license plate, and vehicle category.
3. The system validates the entered information and checks whether the email address is already registered.
4. The system sends a verification code to the driver's phone through SMS.
5. The driver enters the verification code.
6. The system validates the code and activates the account.

Postcondition: The driver's account is active, the vehicle information is saved, and the driver is logged into the application.

### UC-02: Real-Time Interactive Parking Map Search

- Actor: Driver
- Precondition: The driver is authenticated and location services are enabled on the mobile device.

Steps:

1. The driver opens the parking map.
2. The system retrieves the driver's current location.
3. The system searches for participating parking facilities near the driver's location.
4. The system retrieves current parking availability and published parking rates.
5. The system displays nearby facilities on an interactive map.
6. The driver selects a facility.
7. The system displays facility details such as parking availability, parking types, EV charging availability, ADA parking, height restrictions, operating hours, and parking rates.

Postcondition: The driver can view nearby parking facilities and their current parking information.

### UC-03: Reserve Parking

- Actor: Driver
- Precondition: The driver is authenticated and the selected parking facility has reservable capacity for the requested time period.

Steps:

1. The driver selects a parking facility.
2. The driver enters the desired arrival time, departure time, and parking type.
3. The system checks parking availability for the selected time period.
4. The system calculates the reservation cost.
5. The driver reviews the reservation details.
6. The driver selects "Proceed to Checkout".
7. The system creates a temporary reservation hold so another driver cannot reserve the same availability during checkout.

Postcondition: The requested parking capacity is temporarily held for the driver while payment is completed.

### UC-04: Process Digital Payment

- Actor: Driver
- Supporting System: Stripe Payment Service
- Precondition: The driver has an active temporary reservation hold and is on the payment screen.

Steps:

1. The driver selects a saved payment method or enters a supported payment method.
2. The system sends the payment request to Stripe.
3. Stripe processes the payment authorization.
4. Stripe returns the transaction result to the system.
5. The system records the successful transaction.
6. The system confirms the parking reservation.
7. The system generates a unique QR entry credential for the reservation.

Postcondition: The payment is recorded as successful, the reservation is confirmed, and the driver's QR entry credential is available in the application.

### UC-05: Navigate to Parking Facility

- Actor: Driver
- Supporting System: Mapping and Location Service
- Precondition: The driver has a confirmed parking reservation.

Steps:

1. The driver opens the active reservation.
2. The driver selects "Navigate to Facility".
3. The system sends the facility location to the mapping and location service.
4. The mapping and location service returns routing information.
5. The application displays navigation directions.
6. As the driver approaches the facility, the application keeps the QR entry credential easy to access.

Postcondition: The driver arrives at the selected parking facility with the QR entry credential available for check-in.

### UC-06: Check In at Parking Facility via QR Code

- Actor: Driver
- Supporting System: Facility QR Scanner and Gate Controller
- Precondition: The driver has a valid reservation and is at the parking facility entrance during the permitted arrival period.

Steps:

1. The driver presents the QR entry credential to the facility scanner at the entrance.
2. The scanner reads the QR entry credential and sends it to the system for validation.
3. The system verifies the reservation status, time period, and associated vehicle information.
4. The system authorizes entry.
5. The system sends an open command to the gate controller.
6. The gate barrier opens.
7. The system updates the reservation from Reserved to Checked-In.
8. The system records the driver's arrival time.
9. The system updates the facility's occupancy information.

Postcondition: The driver is admitted to the parking facility and the parking session becomes active.

### UC-07: Extend Parking Reservation Duration

- Actor: Driver
- Supporting System: Stripe Payment Service
- Precondition: The driver has an active checked-in parking session and the facility can support the requested extension.

Steps:

1. The driver opens the active parking session.
2. The driver selects "Extend Parking Duration".
3. The driver chooses the amount of additional parking time.
4. The system checks whether more time and parking capacity are available.
5. The system calculates the additional payment required.
6. The driver confirms the extension.
7. The system processes the additional payment.
8. The system updates the reservation expiration time.

Postcondition: The parking session is extended and the updated transaction is recorded.

### UC-08: View Reservation History and Download Receipts

- Actor: Driver
- Precondition: The driver is authenticated and has at least one previous parking transaction.

Steps:

1. The driver opens "Parking History".
2. The system retrieves completed and canceled parking sessions associated with the driver's account.
3. The system displays the driver's previous parking sessions, transactions, and reservations.
4. The driver selects a specific transaction.
5. The system displays the transaction details.
6. The driver selects "Download Receipt PDF".
7. The system generates the requested PDF receipt.

Postcondition: The driver can view past parking activity and download a receipt for the selected transaction.

### UC-09: Configure Facility and Parking Inventory

- Actor: Parking Facility Operator
- Precondition: The operator is authenticated and has permission to manage the parking facility.

Steps:

1. The operator opens "Facility Setup".
2. The operator enters the facility name, address, total capacity, operating hours, number of floors or zones, and supported parking types.
3. The operator defines parking types such as Standard, Compact, EV, and ADA.
4. The operator maps supported parking sensors to physical spaces or parking zones.
5. The operator saves the facility configuration.
6. The system validates the facility information.
7. The system publishes the facility so drivers can find it when searching for nearby parking.

Postcondition: The parking facility and its inventory configuration are active and available to drivers.

### UC-10: Configure Dynamic Pricing Rules

- Actor: Parking Facility Operator or Administrator
- Precondition: The operator is authenticated and authorized to manage facility pricing.

Steps:

1. The operator opens "Rate Management".
2. The operator creates a dynamic pricing rule.
3. The operator selects an occupancy threshold or other permitted pricing condition.
4. The operator defines the associated price adjustment.
5. The system checks the proposed rule against configured pricing limits and business rules.
6. The system alerts the operator if the proposed rule violates a configured restriction.
7. The operator activates an approved pricing rule.
8. The system applies the pricing rule when the configured conditions are met.

Postcondition: The approved dynamic pricing rule is active for the selected parking facility.

### UC-11: Generate Garage Occupancy and Revenue Report

- Actor: Parking Facility Operator or Finance Personnel
- Precondition: The user is authenticated and has reporting permissions.

Steps:

1. The user opens "Analytics & Reports".
2. The user selects a parking facility.
3. The user selects a reporting period.
4. The user selects the desired reporting metrics.
5. The system retrieves the required occupancy and transaction data.
6. The system calculates the requested metrics.
7. The system displays charts and summary information.
8. The user may export the report in a supported format.

Postcondition: The requested occupancy or revenue report is displayed and can be exported when needed.

### UC-12: Manual Gate Override

- Actor: Facility Attendant or Parking Operator
- Precondition: The attendant is authenticated and the gate control system is available.

Steps:

1. The attendant identifies a driver experiencing a gate or QR check-in problem.
2. The attendant opens the "Gate Override" function.
3. The attendant enters the vehicle license plate.
4. The attendant records the reason for the override.
5. The system records the employee, the time of the override, the vehicle information, and the reason for the action.
6. The attendant confirms the override.
7. The system sends the authorized command to open the gate.

Postcondition: The gate opens and the override is recorded in the system audit log.

### UC-13: Manage Users and Role-Based Access Control

- Actor: System Administrator
- Precondition: The administrator is authenticated and authorized to manage system access.

Steps:

1. The administrator opens "User & Access Control".
2. The administrator searches for an employee or administrative user.
3. The system displays the user's current role and permissions.
4. The administrator modifies the user's role or permissions when necessary.
5. The administrator may suspend or revoke access when required.
6. The system updates the user's role-based access control permissions.
7. The system records the administrative change.

Postcondition: The user's access permissions and account status reflect the approved administrative changes.

### UC-14: Expire Unused Reservation and Release Inventory

- Trigger: The reservation grace period expires without a successful driver check-in.
- Precondition: The reservation start time has passed by the configured grace period and the driver has not checked in.

Steps:

1. The system identifies reservations that have passed the permitted check-in grace period.
2. The system verifies that no successful check-in occurred.
3. The system changes the reservation status to No-Show / Expired.
4. The system returns that parking capacity to available inventory.
5. The system applies any configured facility cancellation or no-show policy.
6. The system records the expiration event.
7. The system sends an expiration notification to the driver.

Postcondition: The reservation is closed and the previously reserved parking capacity becomes available again.

### UC-15: Send Parking Expiration Warning

- Trigger: An active parking session reaches the configured expiration-warning threshold.
- Supporting System: Apple Push Notification Service and Firebase Cloud Messaging
- Precondition: The driver has an active checked in parking session and notifications are enabled.

Steps:

1. The system monitors active parking session expiration times.
2. The system identifies a session that has reached the warning threshold.
3. The system creates an expiration warning message.
4. The system sends the notification through the appropriate mobile notification service.
5. The driver's device receives and displays the notification.
6. The system records the notification event.

Postcondition: The driver receives a warning that the parking session is approaching expiration and can return to the application to extend the session when permitted.

## 6. Work Breakdown Structure, Agile Estimation, and Project Schedule

### 6.1 Estimation Approach

The Smart Parking Platform will use a three level Work Breakdown Structure to break the project into smaller, manageable areas of work. Level 1 represents the smart parking platform, level 2 represents the major parts of the platform, and level 3 represents the individual features and tasks that need to be completed.

Story points will be assigned to level 3 tasks using the Fibonacci scale of 1, 2, 3, 5, 8, and 13. The story points are based on how complicated the task is, the risk, and the amount of effort to complete it. The points are used to compare the tasks to each other and do not represent the exact hours to complete the work.

Navigate to Parking Facility (Use Case 5) will be used as the one story point baseline because it is one of the simpler features in the platform. The system sends the selected parking facility location to the mapping service and receives the routing information back. The other tasks will be estimated by comparing them to this baseline.

### 6.2 Three-Level Work Breakdown Structure

1.0 Smart Parking Platform

1.1 Driver Account and Access
    1.1.1 User Registration and Profile Setup (UC-01) [3 SP]

1.2 Parking Discovery and Reservation
    1.2.1 Real Time Interactive Parking Map Search (UC-02) [5 SP]
    1.2.2 Reserve Parking and Temporary Capacity Hold (UC-03) [5 SP]
    1.2.3 Navigate to Parking Facility (UC-05) [1 SP]

1.3 Payment and Driver Session Management
    1.3.1 Process Digital Payment and Generate QR Credential (UC-04) [8 SP]
    1.3.2 Extend Parking Reservation Duration (UC-07) [5 SP]
    1.3.3 View Reservation History and Download Receipts (UC-08) [3 SP]

1.4 Facility Operations and Hardware Integration
    1.4.1 QR Check-In and Gate Control Integration (UC-06) [8 SP]
    1.4.2 Configure Facility and Parking Inventory (UC-09) [8 SP]
    1.4.3 Manual Gate Override and Audit Logging (UC-12) [5 SP]

1.5 Operator, Reporting and Administration
    1.5.1 Configure Dynamic Pricing Rules (UC-10) [8 SP]
    1.5.2 Generate Occupancy and Revenue Reports (UC-11) [5 SP]
    1.5.3 Manage Users and Role-Based Access Control (UC-13) [5 SP]

1.6 Automated Platform Services
    1.6.1 Expire Unused Reservations and Release Inventory (UC-14) [5 SP]
    1.6.2 Send Parking Expiration Warning (UC-15) [3 SP]


### 6.3 Story Point Estimation

| WBS ID | Work Package                                       | Story Points | Reason for Estimate                                                                                                               |
| ------ | -------------------------------------------------- | -----------: | --------------------------------------------------------------------------------------------------------------------------------- |
| 1.1.1  | User Registration and Profile Setup                |            3 | Includes creating an account, saving vehicle information, checking the users information, and sending an SMS code.                |
| 1.2.1  | Real-Time Interactive Parking Map Search           |            5 | Uses the drivers location, searches nearby facilities, and shows current availability, rates, hours, and parking types.           |
| 1.2.2  | Reserve Parking and Temporary Capacity Hold        |            5 | Checks availability, calculates the cost, and holds the parking capacity while the driver completes checkout.                     |
| 1.2.3  | Navigate to Parking Facility                       |            1 | Baseline: Mainly sends the facility location to the mapping service and displays the directions that are returned.                |
| 1.3.1  | Process Digital Payment and Generate QR Credential |            8 | Uses Stripe to process digital payment's, records the transaction, confirms the reservation, and creates the QR entry credential. |
| 1.3.2  | Extend Parking Reservation Duration                |            5 | Checks if more time and parking capacity is available, calculates the extra cost, processes payment, and updates the reservation. |
| 1.3.3  | View Reservation History and Download Receipts     |            3 | Retrieves previous parking sessions and transactions and creates a PDF receipt when the driver requests one.                      |
| 1.4.1  | QR Check-In and Gate Control Integration           |            8 | Checks the QR code, communicates with the gate system, opens the gate, and updates the reservation and occupancy.                 |
| 1.4.2  | Configure Facility and Parking Inventory           |            8 | Allows operators to enter facility information, set up floors or zones, parking types, and map supported sensors.                 |
| 1.4.3  | Manual Gate Override and Audit Logging             |            5 | Allows an authorized employee to open the gate and records the employee, vehicle, time, and reason.                               |
| 1.5.1  | Configure Dynamic Pricing Rules                    |            8 | Allows operators to set pricing rules based on demand or occupancy and checks the rules against pricing limits.                   |
| 1.5.2  | Generate Occupancy and Revenue Reports             |            5 | Retrieves parking and transaction information, calculates the requested results, and allows reports to be exported.               |
| 1.5.3  | Manage Users and Role-Based Access Control         |            5 | Allows administrators to change roles and permissions, remove access when needed, and record the change.                          |
| 1.6.1  | Expire Unused Reservations and Release Inventory   |            5 | Finds reservations that passed the grace period, closes them, returns the parking capacity, and notifies the driver.              |
| 1.6.2  | Send Parking Expiration Warning                    |            3 | Monitors active parking sessions and sends the driver a warning when the session is close to expiring.                            |

### 6.4 Project Schedule and Task Dependencies

| WBS ID | Work Package                                       | Predecessor  | Dependency |  SP | Estimated Duration |
| ------ | -------------------------------------------------- | ------------ | ---------- | --: | -----------------: |
| 1.1.1  | User Registration and Profile Setup                | None         | -          |   3 |             2 days |
| 1.4.2  | Configure Facility and Parking Inventory           | None         | -          |   8 |             4 days |
| 1.5.3  | Manage Users and Role-Based Access Control         | None         | -          |   5 |             3 days |
| 1.2.1  | Real-Time Interactive Parking Map Search           | 1.4.2        | FS         |   5 |             3 days |
| 1.2.2  | Reserve Parking and Temporary Capacity Hold        | 1.1.1, 1.2.1 | FS         |   5 |             3 days |
| 1.3.1  | Process Digital Payment and Generate QR Credential | 1.2.2        | FS         |   8 |             4 days |
| 1.2.3  | Navigate to Parking Facility                       | 1.3.1        | FS         |   1 |              1 day |
| 1.4.1  | QR Check-In and Gate Control Integration           | 1.3.1, 1.4.2 | FS         |   8 |             4 days |
| 1.3.2  | Extend Parking Reservation Duration                | 1.4.1        | FS         |   5 |             3 days |
| 1.3.3  | View Reservation History and Download Receipts     | 1.3.1        | FS         |   3 |             2 days |
| 1.5.1  | Configure Dynamic Pricing Rules                    | 1.4.2        | FS         |   8 |             4 days |
| 1.5.2  | Generate Occupancy and Revenue Reports             | 1.4.1        | FS         |   5 |             3 days |
| 1.4.3  | Manual Gate Override and Audit Logging             | 1.4.1, 1.5.3 | FS         |   5 |             3 days |
| 1.6.1  | Expire Unused Reservations and Release Inventory   | 1.2.2        | FS         |   5 |             3 days |
| 1.6.2  | Send Parking Expiration Warning                    | 1.4.1        | FS         |   3 |             2 days |

Finish-to-Start (FS) means one task should be completed before the next related task begins. Some of the work can also happen at the same time when the tasks do not directly depend on each other. For example, account setup, facility setup, and access control can begin separately, while payment cannot be completed until the reservation process is working.

### 6.5 Project Milestones

Milestone 1: Requirements and Planning Baseline

The SRS, use cases, Work Breakdown Structure, story point estimates, and initial project schedule are completed.

Milestone 2: Core Driver Functions Completed

Driver registration, parking search, and reservation functions are working together.

Milestone 3: Payment and Parking Entry Integration Completed

Stripe payment processing, QR credential generation, and parking facility check-in are connected.

Milestone 4: Operator and Automated Services Completed

Facility management, pricing, reporting, access management, reservation expiration, and parking expiration warnings are available.

Milestone 5: Final Smart Parking Platform Delivery

The full Smart Parking Platform is reviewed, tested, and prepared for final project delivery.

### 6.6 Gantt Chart

![Smart Parking Platform Draft Project Gantt Schedule](images/GANTT_HW2.png)

Figure 1. Smart Parking Platform Draft Project Schedule and Task Dependencies.

| Date       | Milestone                                       |
| ---------- | ----------------------------------------------- |
| 09/18/2026 | Requirements and Planning Baseline              |
| 09/30/2026 | Core Driver Functions Completed                 |
| 10/08/2026 | Payment and Parking Entry Integration Completed |
| 10/11/2026 | Operator and Automated Services Completed       |
| 12/04/2026 | Final Smart Parking Platform Delivery           |
