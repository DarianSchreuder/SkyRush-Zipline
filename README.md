# SkyRush Zipline Management System

A desktop management application developed in **C# (.NET)** and **Microsoft SQL Server** designed to streamline operations, booking workflows, equipment tracking, and staff management for a commercial zipline tourism business.

---

## System Overview

The **SkyRush Zipline Management System** provides role-based operational management across three distinct access tiers:
* **Owner:** Full administrative access, system reporting, and tour guide management[cite: 1].
* **Secretary:** Operations management including tourist registration, booking workflows, payments, and equipment schedules[cite: 1].
* **Tour Guide:** Operational access for participant check-ins, indemnity waiver verification, and equipment assignment/return[cite: 1].

---

## Core Features

* **Tourist & Waiver Management:** Captures tourist details, medical conditions, and mandatory signed indemnity waivers prior to tour participation[cite: 1]. Enforces automated 2-year retention pruning[cite: 1].
* **Tour Guide Administration:** Tracks guide credentials, contact details, and certification expiry dates with automated renewal notifications[cite: 1].
* **Bookings & Check-In:** Full lifecycle booking management[cite: 1]. Restricts tour departure until all participants have verified waivers and completed check-in[cite: 1].
* **Payment Processing:** Handles EFT and cash payments linked directly to bookings, requiring full settlement before departure[cite: 1].
* **Equipment & Infrastructure Maintenance:** Complete register of gear and course infrastructure, tracking checkout/return times and scheduled service intervals[cite: 1].
* **Management Reporting:** Generates business intelligence reports, including **Equipment Service Reminders** and **Top 5 Most Popular Weeks**[cite: 1].

---

## Database Architecture (3NF)

The relational schema is implemented in **Microsoft SQL Server** and normalized to Third Normal Form (3NF)[cite: 1]:

| Entity | Primary Key | Foreign Keys | Key Attributes |
| :--- | :--- | :--- | :--- |
| **TOURIST**[cite: 1] | `Tourist_ID`[cite: 1] | — | `ID_Number`, `First_Name`, `Last_Name`, `Email`, `Address`, `Medical_Conditions`, `WaiverSignedDate`[cite: 1] |
| **TOUR_GUIDE**[cite: 1] | `TourGuide_ID`[cite: 1] | — | `First_Name`, `Last_Name`, `Contact_Number`, `Email`, `Certification_Number`, `CertificationExpiryDate`[cite: 1] |
| **BOOKING**[cite: 1] | `Booking_ID`[cite: 1] | `TourGuide_ID`[cite: 1] | `Date`, `Time`, `Group_Size`, `Cancel_(Y/N)`[cite: 1] |
| **BOOKING_PARTICIPANT**[cite: 1] | `(Booking_ID, Tourist_ID)`[cite: 1] | `Booking_ID`, `Tourist_ID`[cite: 1] | `CheckInStatus`, `CheckInTime`[cite: 1] |
| **PAYMENT**[cite: 1] | `Payment_ID`[cite: 1] | `Booking_ID`[cite: 1] | `Payment_Date`, `Amount`, `Payment_Status`[cite: 1] |
| **EQUIPMENT**[cite: 1] | `Equipment_ID`[cite: 1] | — | `Equipment_Type`, `Serial_Number`, `Purchase_Date`, `Last_Service_Date`, `Next_Service_Date`[cite: 1] |
| **EQUIPMENT_ASSIGNMENT**[cite: 1] | `(Booking_ID, Tourist_ID, Equipment_ID)`[cite: 1] | `Booking_ID`, `Tourist_ID`, `Equipment_ID`[cite: 1] | `AssignmentDateTime`, `ReturnedDateTime`[cite: 1] |
| **INFRASTRUCTURE**[cite: 1] | `Infrastructure_ID`[cite: 1] | — | `Infrastructure_Type`, `Location`, `Last_Inspection_Date`, `Next_Inspection_Date`[cite: 1] |

---

## Tech Stack & Prerequisites

* **Development Platform:** C# (.NET Framework / .NET Core / Windows Forms or WPF)[cite: 1]
* **Database Engine:** Microsoft SQL Server 2019+ or LocalDB[cite: 1]
* **IDE:** Microsoft Visual Studio 2022 (with *.NET desktop development* workload)
* **Database Tooling:** SQL Server Management Studio (SSMS)

---

## Getting Started

### 1. Database Setup
1. Open SQL Server Management Studio (SSMS) and connect to your SQL Server instance[cite: 1].
2. Create a new database named `SkyRushDB`[cite: 1]:
   ```sql
   CREATE DATABASE SkyRushDB;
   GO
