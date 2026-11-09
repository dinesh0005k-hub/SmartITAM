# SmartITAM — Automated Hardware Asset Management

[![Platform](https://img.shields.io/badge/Platform-ServiceNow-brightgreen.svg)](https://www.servicenow.com/)
[![Application Scope](https://img.shields.io/badge/Scope-x__2240997__smarti__0-blue.svg)]()
[![Build](https://img.shields.io/badge/Build-Passing-success.svg)]()

**SmartITAM** is a custom scoped ServiceNow application designed to manage and automate the end-to-end hardware asset lifecycle. It eliminates manual asset tracking by integrating real-time stock validation, zero-touch request fulfillment, and an automated closed-loop replacement workflow when assets are decommissioned.

---

## 🔄 End-to-End Lifecycle Workflow

```text
[ End User ] 
      │ (Submit Request via Service Portal / Record Producer)
      ▼
[ Asynchronous Stock Check ] ◄── (GlideAjax + Script Include checks available/refurbished inventory)
      │
      ▼
[ Flow Designer: Hardware Request Handler ]
      │ ──► Allocates Asset & Updates State to 'In Use'
      │ ──► Dispatches User Notification
      ▼
[ Asset Lifecycle Tracking ]
      │ (Active usage, automated state synchronization)
      ▼
[ Asset Retirement ]
      │
      ▼
[ Business Rule: Retire Asset and Request Replacement ]
      │ (Sets Asset State to 'Retired')
      │
      └──────► Automatically triggers a new Hardware Request back to step 1
```

---

## 🚀 Key Modules & Technical Features

### 1. Data Model & Architecture
* **Hardware Request Table (`x_2240997_smarti_0_hardware_request`)**: Extends standard task architecture to capture requester details, asset models, urgency, and fulfillment state.
* **IT Asset Table (`x_2240997_smarti_0_it_asset`)**: Tracks asset inventory, serial numbers, operational status (`In Stock`, `In Use`, `Retired`), and assigned owners.
* **Data Security & Scoping**: Implements granular Role-Based Access Control (ACLs) restricting write access to application administrators while enabling requesters read-only access to their allocated assets.

### 2. Client & Server Scripting
* **Asynchronous Stock Validation**: Utilizes a client-callable **Script Include** paired with a **Catalog Client Script** using `GlideAjax` to query refurbished and in-stock devices dynamically without freezing the client browser.
* **Lifecycle Automation Rule**: A custom server-side **Business Rule** (`Retire Asset and Request Replacement`) running on the Asset table:
  * Triggers when an asset state transitions to `Retired`.
  * Automatically instantiates a replacement record in the Hardware Request pipeline for continuous hardware availability.

### 3. Process Automation (Flow Designer)
* **Flow: `Hardware Request Handler`**
  * Automates fulfillment logic upon request submission.
  * Validates available stock, pairs asset serial numbers, updates the asset state to `In Use`, and notifies the requester upon assignment.

### 4. Operations Dashboard & Analytics
* Centralized dashboard widgets tracking real-time asset health:
  * Hardware requests by state (Pending, In Progress, Closed).
  * Asset status breakdown (Total Inventory, In-Use, Decommissioned).
  * Refurbished stock alerts for quick redeployment.

---

## 🛠️ Tech Stack & Platform Components
* **Platform:** ServiceNow (Scoped Application)
* **Core APIs:** `GlideRecord`, `GlideAjax`, `g_form`, Script Includes, Business Rules
* **Automation:** ServiceNow Flow Designer
* **Service Portal:** Record Producers, Catalog Client Scripts
* **Reporting:** Platform Analytics, Single Score & Donut Reports
* **Source Control:** Git / GitHub Studio Integration

---
