# 🎟️ Event Management System (Frappe)

A custom **Event Management System** built using the **Frappe Framework**, designed to manage events, attendees, ticket sales, and enforce event capacity constraints.

---

## 📌 Features

### 🗓️ Event Management
- Create and manage events
- Store event details such as:
  - Event Name
  - Event Date
  - Event Type
  - Location
  - Description
  - Capacity
- Prevent saving events when capacity rules are violated

---

### 👥 Attendee Management
- Register attendees for events
- Update attendee details
- Link attendees to specific events
- Track attendee status:
  - Registered
  - Cancelled
- View all attendees mapped to an event

---

### 🎫 Ticket Management
- Issue tickets for registered attendees
- Each ticket is linked to:
  - Event
  - Attendee
- Track ticket status (Sold / Cancelled)
- Prevent ticket creation when event capacity is exceeded

---

### 📊 Capacity Validation (Core Logic)
- Automatically checks:
  - Number of participants
 
Participants > Capacity
- Validation implemented using **Frappe Server Scripts**

---

### 📈 Reports (Basic)
- Total tickets sold per event
- Remaining tickets available
- Revenue per event (fixed ticket price assumption)

---

## 🛠️ Tech Stack

- **Framework:** Frappe
- **Language:** Python
- **Database:** MariaDB
- **Frontend:** Frappe UI
- **Version Control:** Git & GitHub
- **Environment:** WSL (Ubuntu on Windows)

---

## 📂 Custom DocTypes

| DocType | Purpose |
|-------|--------|
| Event Master | Stores event details and capacity |
| Event Participant | Child table for participants |
| Attendee | Stores attendee personal details |
| Ticket | Manages ticket sales and linking |

---

## ⚙️ Capacity Validation Logic

Implemented using **Server Script (Before Save)**:

```python
if not doc.capacity:
  frappe.throw("Please set event capacity")

participant_count = len(doc.participants or [])

if participant_count > doc.capacity:
  frappe.throw(
      f"Capacity exceeded! Maximum allowed is {doc.capacity}, "
      f"but you have added {participant_count} participants."
  )

🚀 How to Run the Project
cd ~/event_bench
bench start

Access the app at:
http://127.0.0.1:8000

🧪 How to Test

Create an Event with capacity = 3

Add 4 participants

Try to save

System blocks save with validation message ✔️

📌 Use Case
This project demonstrates:

Business rule enforcement

Real-world capacity validation

Proper relational data modeling

Server-side logic using Frappe

👤 Author

Name: bheullaa
GitHub: https://github.com/bheullaa


🏁 Status

