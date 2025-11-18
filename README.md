# ServiceNow_ITSM_Project9
ServiceNow ITSM – AI-Style Major Incident Auto-Notification Flow
# ServiceNow ITSM – AI-Style Major Incident Auto-Notification Flow

## 🧠 Overview
This project implements an **AI-style Major Incident automation** in ServiceNow using **Flow Designer**, fully compatible with restricted PDIs.

When a new Incident is created with **High priority or critical category** (e.g., Network, Email, Hardware), the flow:

- Escalates the Priority to **Critical**
- Assigns it to a **Major Incident** group
- Adds an **AI-style summary** into Work notes
- Optionally sends a notification email to stakeholders

No GenAI plugin, no scripting, no Predictive Intelligence required – everything is done using standard Flow Designer actions.

---

## 🎯 Use Case

In real ITSM operations, Major Incidents must be escalated quickly and consistently.  
This flow standardizes that behavior and simulates AI-driven reasoning through smart, generated summaries using text + data pills.

---

## ⚙️ Flow Design

### Trigger
- Table: **Incident [incident]**
- When: **Record Created**
- Condition (example):
  - Priority is **2 - High**
  - OR Category is in **Network, Email, Hardware, Access**

### Actions

1. **Update Record – Incident**
   - Record: **Trigger → Record**
   - Fields set:
     - **Assignment group** = `Major Incident Group` (or existing group)
     - **Priority** = `1 - Critical`
     - **Short description** = `[Major Incident] ` + Trigger Short description
     - **Work notes** = AI-style summary using:
       - Trigger Short description
       - Trigger Category
       - Trigger Priority

2. **(Optional) Send Email**
   - To: Major Incident distribution list
   - Subject: `Major Incident Detected – ${trigger.number}`
   - Body includes:
     - Short description
     - Category
     - Escalation note

---

## 🧪 Testing

1. Open `incident.do` and create a new incident:
   - Priority = High
   - Category = Network/Email/etc.
2. Save the incident.
3. Confirm:
   - Priority changed to Critical
   - Assignment group updated
   - Short description prefixed with `[Major Incident]`
   - Work notes contain the AI-style summary

---

## 🧠 What I Learned

- How to design ITSM escalation flows in Flow Designer  
- How to emulate **AI-style reasoning** using Work notes and templates  
- How to work around **PDI limitations** (no GenAI, no PI) and still build meaningful automation  

