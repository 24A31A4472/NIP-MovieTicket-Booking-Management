<div align="center">

# 🎬 Pega Movie Ticket Booking Management System
**An Enterprise Case Management & Workflow Automation Solution Built on Pega Platform**

[![Pega Platform](https://img.shields.io/badge/Platform-Pega%20Platform-004481?style=for-the-badge&logo=pega&logoColor=white)](https://www.pega.com/)
[![Status](https://img.shields.io/badge/Status-Completed%20%26%20Verified-success?style=for-the-badge)](#)
[![Case Lifecycle](https://img.shields.io/badge/Lifecycle-4%20Stages-blue?style=for-the-badge)](#)

<br/>

[🎥 Watch Project Demo Video](https://drive.google.com/file/d/19hJZ3sCE6ipJrPW4JlPl0A1_pUUJU0Z-/view?usp=drivesdk) • [📄 Implementation Document](#-repository-structure) • [⚙️ Key Features](#-core-technical-features)

</div>

---

## 📺 Project Walkthrough & Demo

> **Live System Demonstration:**  
> 🔗 **[Click here to watch the complete end-to-end case execution video on Google Drive](https://drive.google.com/file/d/19hJZ3sCE6ipJrPW4JlPl0A1_pUUJU0Z-/view?usp=drivesdk)**

---

### 📦 Application Package (RAP)
* [Download Pega Application Export (.zip)](https://drive.google.com/file/d/1XrHl26iH9w3Ou-Dc51x0GM6n9LCiYmF-/view?usp=drivesdk)

## 📖 Overview

The **Movie Ticket Booking Management System** is a low-code enterprise application designed to streamline customer ticket reservations, real-time availability checks, multi-tiered price calculations, queue-based workload distribution, and automated customer correspondence.

Initially drafted using **Pega GenAI Blueprint**, the application was fully customized in **Pega App Studio & Dev Studio** with declarative rules, SLAs, and decision routing logic.

---

## 🔄 Case Lifecycle Architecture

[ Stage 1: Capture Details ] ➡️ [ Stage 2: Availability ] ➡️ [ Stage 3: Approval ] ➡️ [ Stage 4: Booking Execution ]
│                                │                             │                               │
• Request Intake                • Verify Seats                • Customer Approval             • Route to Queue
• Customer & Movie Info         • Agent Availability Check    • Approve / Reject Decision     • Allocate Seats & Notify

### **Detailed Stages & Process Steps:**
1. **Capture Details:** Collects customer email, phone, venue name, preferred movie, and show date/time with mandatory validations.
2. **Availability:** Routes work to the `BookingAgentQueue` to verify seat count and validate theater capacity.
3. **Approval:** Presents an itemized summary to the `Customer` persona for explicit booking confirmation or cancellation.
4. **Booking Execution:** Dynamically assigns seat numbers, generates a unique `Ticket ID`, dispatches an email confirmation, and marks the case as `RESOLVED-COMPLETED`.

---

## ⚙️ Core Technical Features

### 🧮 1. Dynamic Declarative Calculation
* **Rule Type:** Declare Expression (`TotalCost`)
* **Computation Logic:** Automatically updates when ticket counts change to eliminate human calculation error.
  $$\text{Total Cost} = \text{Ticket Price} \times \text{Number Of Tickets}$$

### 🔀 2. Business Logic Routing
* **Rule Type:** Conditional Step Routing
* **Queue Distribution:**
  * If `Show Type == "Premium"` $\rightarrow$ Routed to **`PremiumShowQueue`**
  * Otherwise $\rightarrow$ Routed to **`StandardShowQueue`**

### ⏱️ 3. Service Level Agreement (SLA)
* **Goal:** `1 Day` (Urgency increases by `+10`)
* **Deadline:** `2 Days` (Urgency increases by `+20`)
* **Purpose:** Prevents booking request abandonment and enforces prompt processing.

### ✉️ 4. Dynamic Correspondence
* **Trigger:** Case Resolution (`RESOLVED-COMPLETED`)
* **Content:** Automatically generates and dispatches an email to the customer containing the generated `Ticket ID`, `Seat Numbers`, `Venue`, and `Total Cost`.

---

## 🗄️ Data Model & Entities

| Data Object | Key Properties | Data Types | Purpose |
| :--- | :--- | :--- | :--- |
| **`Movie`** | `Movie Name`, `Genre`, `Country by Code` | Text, Text, Text | Stores movie catalog and classifications |
| **`Show`** | `Show Date`, `Show Time`, `Seat Capacity`, `Show Type`, `Ticket Price` | Date, Time, Integer, Text, Decimal | Manages schedules, pricing, and hall limits |

---

## 👥 Personas & Work Queues

* **Personas:**
  * `Customer`: Submits request, reviews summary, and approves/rejects booking.
  * `Booking Agent`: Manages inventory validation and seat allocation.
* **Work Queues:**
  * `BookingAgentQueue`: Validates seat counts.
  * `StandardShowQueue`: Allocates regular seating.
  * `PremiumShowQueue`: Allocates VIP/Premium seating.

---

## 📁 Repository Structure

```text
├── README.md                              # Application documentation & architecture
├── MovieTicket_AnithaDevi_Donga.docx      # Complete submission report (10 User Stories & Evidence)
└── docs/                                  # Workflow diagrams
