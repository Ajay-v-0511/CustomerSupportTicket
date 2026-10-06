# Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce

## 📌 Project Overview

The **Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce** is a Salesforce-based automation solution designed to reduce manual effort in customer support operations.

The system analyzes customer support ticket descriptions, automatically classifies tickets into **High, Medium, or Low priority**, and performs appropriate backend actions using **Salesforce Flow and Agentforce**.

For High-priority tickets, the system automatically creates an urgent handling task and assigns the ticket to a senior support agent.

---

## 🎯 Objectives

- Automatically classify support tickets as **High, Medium, or Low** priority.
- Retrieve the latest support ticket associated with a customer Account.
- Analyze ticket descriptions using configured urgency conditions.
- Reduce manual ticket prioritization and assignment.
- Automatically create urgent tasks for High-priority tickets.
- Assign critical tickets to the appropriate support level.
- Provide conversational support through Agentforce.
- Improve support response and resolution efficiency.

---

## ❗ Problem Statement

Customer support teams handle a large number of tickets every day. Manual prioritization can cause critical issues to be overlooked or delayed.

Support agents may need to manually identify urgency, assign tickets, and create tasks, increasing workload and response time.

This project solves the problem by combining **Agentforce AI-assisted analysis with Salesforce Flow automation**.

---

## 💡 Proposed Solution

The proposed system follows this process:

```text
Customer / Support User
          ↓
      Agentforce
          ↓
Support Ticket Priority Analysis
          ↓
   Auto-Launched Flow
          ↓
 Retrieve Latest Ticket
          ↓
 Analyze Description
          ↓
 Priority Classification
     ↙      ↓      ↘
  HIGH    MEDIUM    LOW
    ↓       ↓        ↓
Urgent    Normal   Queue
 Task     Handling Processing
    ↓
Senior Support Agent
```

The documented architecture connects Users/Support Team → Agentforce → Support Ticket Priority Analysis → Auto-Launched Flow → Account & Ticket Data → Priority Decision → Task/Assignment → Agentforce Response.

---

## 🏗️ Technology Stack

| Component | Technology |
|---|---|
| Platform | Salesforce |
| AI / Conversational Layer | Agentforce |
| Automation | Salesforce Auto-Launched Flow |
| Database | Salesforce Custom Object |
| Custom Object | Support Ticket Intelligence |
| Records | Account, Contact, User, Task |
| Logic | Flow Decision & Assignment |
| Output | Agentforce Conversation Response |



---

## 🗃️ Data Model

### Support Ticket Intelligence

**API Name:** `Support_Ticket_Intelligence__c`

| Field | Type | Purpose |
|---|---|---|
| Ticket Number | Auto Number | Unique ticket identifier |
| Customer | Lookup(Account) | Related customer account |
| Contact | Lookup(Contact) | Customer contact |
| Issue Type | Picklist | Technical, Billing, General |
| Description | Long Text | Ticket issue details |
| Priority Level | Picklist | Low, Medium, High |
| Status | Picklist | New, In Progress, Resolved |
| Created Date | Date | Ticket creation date |
| Assigned To | Lookup(User) | Assigned support agent |
| SLA Breach Risk | Checkbox | SLA risk indicator |
| Resolution Time | Number | Resolution time in hours |



---

## 🤖 Agentforce

The project uses an Agentforce subagent named:

**Support Ticket Priority Analysis**

### Responsibilities

1. Ask for the Account Name if it is not provided.
2. Retrieve the latest support ticket for the Account.
3. Read the ticket description.
4. Determine the priority.
5. Trigger backend automation for High-priority tickets.
6. Assign the appropriate support level.
7. Return the handling result to the user.

The Agentforce subagent is specifically scoped to ticket analysis, priority determination, and backend automation.

---

## 🔎 Priority Classification

The current implementation uses configured keywords.

### 🔴 High Priority

If the description contains:

- `urgent`
- `not working`
- `failure`

### 🟡 Medium Priority

If the description contains:

- `issue`
- `slow`
- `delay`

### 🟢 Low Priority

If none of the configured High or Medium priority conditions are matched, the ticket is classified as **Low**.

---

## ⚙️ Salesforce Flow

The system uses an **Auto-Launched Flow** called:

`Support_Ticket_Intellegence`

### Flow Process

```text
Start
  ↓
Get Account
  ↓
Store Account ID
  ↓
Get Latest Ticket
  ↓
Store Ticket ID
  ↓
Analyze Description
  ↓
Set Priority Level
  ↓
Check High Priority
  ↓
Create Urgent Task
  ↓
Set Assigned Agent
  ↓
Generate Final Message
  ↓
End
```

The Flow retrieves the Account and latest ticket, analyzes the description, determines priority, creates a task for High-priority tickets, assigns the support level, and produces the final action message.

---

## 🔄 System Workflow

```text
1. User provides Account Name
             ↓
2. Agentforce receives request
             ↓
3. Latest ticket is retrieved
             ↓
4. Ticket description is analyzed
             ↓
5. Priority is determined
             ↓
6. High / Medium / Low decision
             ↓
7. High → Urgent Task + Senior Agent
   Medium → Normal Handling
   Low → Queue for Processing
             ↓
8. Result returned through Agentforce
```

---

## 🧪 Example

### Example 1 — High Priority

**Ticket Description:**

```text
Payment system is not working and the customer cannot complete the transaction.
```

**Result:**

```text
Priority: High
Assigned To: Senior Support Agent
Action: Urgent Ticket Handling task created
```

### Example 2 — Medium Priority

**Ticket Description:**

```text
The application is slow while loading the dashboard.
```

**Result:**

```text
Priority: Medium
Action: Ticket will be handled shortly
```

### Example 3 — Low Priority

**Ticket Description:**

```text
Customer requested general information about the service.
```

**Result:**

```text
Priority: Low
Action: Ticket queued for processing
```

---

## 📥 Input

The primary input is:

```text
Account Name
```

The system uses the Account Name to identify the customer and retrieve the latest associated support ticket.

---

## 📤 Output

The system returns:

- Account ID
- Ticket ID
- Priority Level
- Assigned Agent
- Action Message

These outputs are exposed through the Agentforce conversation.

---

## 🚀 Key Features

- ✅ Automatic ticket prioritization
- ✅ Agentforce conversational interaction
- ✅ Latest ticket retrieval
- ✅ Keyword-based urgency analysis
- ✅ High-priority task creation
- ✅ Automatic support assignment
- ✅ SLA risk checking
- ✅ Reduced manual effort
- ✅ Faster identification of critical issues
- ✅ Scalable Salesforce automation



---

## 📊 Advantages

### 1. Automatic Prioritization
Tickets are automatically classified as High, Medium, or Low.

### 2. Faster Critical Issue Detection
Urgent tickets can be identified and handled first.

### 3. Reduced Manual Work
Ticket analysis, task creation, and assignment are automated.

### 4. Conversational Support
Users can interact with the system through Agentforce.

### 5. Improved Assignment
High-priority tickets can be assigned to a senior support agent.

### 6. Better Response Time
Automation reduces delays in handling critical customer issues.

### 7. Scalable
Salesforce automation can support increasing ticket volumes.

---

## ⚠️ Limitations

- Priority classification currently depends on configured keywords.
- Contextual understanding is limited.
- Accurate Account, Contact, and ticket information is required.
- Flow configuration must be maintained when business rules change.
- Agentforce depends on correct subagent and Flow configuration.
- SLA monitoring is currently limited.
- More advanced assignment rules require additional configuration.
- Advanced analytics are part of future scope.

---

## 🔮 Future Enhancements

Future development can include:

- More sophisticated priority indicators.
- Advanced business rules.
- Improved SLA monitoring and escalation.
- Support for multiple support teams.
- More advanced assignment rules.
- Priority trend analytics.
- Resolution performance analytics.
- Additional Agentforce outputs and variables.
- Improved contextual understanding of ticket descriptions.



---

## 📈 Project Outcome

The system demonstrates how **Salesforce Flow and Agentforce** can work together to automate customer support ticket handling.

The completed workflow retrieves the latest ticket, analyzes its description, classifies priority, creates an urgent task for High-priority cases, assigns a support level, and provides a conversational response.

---

## 👥 Team

| Team Member | Responsibility |
|---|---|
| Ajay V | Salesforce Setup, Agentforce & Automation, SLA Management |
| Aravinth P | Data Modeling, Task & Assignment |
| Kamalnath P | Data Modeling & Automation |
| Abishek V | Priority Classification & Agentforce Conversation |

The project document's sprint plan assigns these responsibilities across the team.

---

## 📌 Project Structure

```text
Customer-Support-Ticket-Priority-Prediction/
│
├── README.md
│
├── Documentation/
│   └── Project Report.docx
│
├── Salesforce/
│   ├── Custom Object
│   │   └── Support Ticket Intelligence
│   │
│   ├── Flow
│   │   └── Support_Ticket_Intellegence
│   │
│   └── Agentforce
│       └── Support Ticket Priority Analysis
│
└── Screenshots/
    ├── Salesforce Setup
    ├── Flow
    ├── Agentforce
    └── Final Output
```

---

## 🏁 Conclusion

The **Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce** provides an automated approach to customer support management.

By combining **Salesforce, Agentforce, and Auto-Launched Flow**, the system reduces manual ticket handling, identifies critical tickets faster, creates urgent tasks, assigns appropriate support levels, and provides clear conversational responses.

This approach can improve support-team productivity and help organizations handle increasing customer-support ticket volumes more efficiently.

---

## 📄 Project Documentation

For complete implementation details, including Salesforce object configuration, Flow logic, Agentforce configuration, testing, project planning, and future scope, refer to the project documentation.

**Project:** Customer Support Ticket Priority Prediction and Automated Assignment System Using Agentforce

**Platform:** Salesforce

**AI:** Agentforce

**Automation:** Salesforce Flow
