Servicenow-project-Automated-Employee-Onboarding-Off-boarding-System-



📌 Project Overview
This project automates the complete employee onboarding and offboarding lifecycle in ServiceNow using:

Custom Roles
User Groups
Employee Lifecycle Table
Service Catalog
Variables
UI Policies
Flow Designer Automation
Approval Workflows
Task Assignment for IT, Facilities, and Security
The goal is to streamline HR operations, reduce manual effort, and ensure smooth employee transitions.

🔹 Step 1: Role Creation
Navigation:
User Administration → Roles → New

Create the following roles:

Role Name	Purpose
hr.manager	HR managers to initiate and track onboarding/offboarding
it.admin	IT admins for account provisioning/deactivation
facilities.staff	Facilities team for workspace allocation/clearance
security.officer	Security staff for ID cards & building access
Procedure:
Go to Roles
Click New
Enter role name
Add description
Click Submit
🔹 Step 2: Group Creation
Navigation:
User Administration → Groups → New

Create the following groups:

Group Name	Assigned Role
HR – People Ops	hr.manager
IT – Account Provisioning	it.admin
Facilities – Workspace	facilities.staff
Security – Access	security.officer
Procedure:
Click New
Enter group name
Save
Assign corresponding role
Submit
🔹 Step 3: Employee Lifecycle Table Creation
Navigation:
System Definition → Tables → New

Table Details:
Name: Employee Lifecycle
Label: u_employee_lifecycle
🔹 Step 4: Fields Creation in Employee Lifecycle Table
Important Fields:
Field Name	Type
Employee Name	Reference
Employee ID	String
Department	Reference
Joining Date	Date
Exit Date	Date
Manager	Reference
Request Type	Choice
Status	Choice
Assets Needed	Multiple Choice
Assets to Collect	Multiple Choice
Special Access	Multi-line Text
Access Revocations	Multi-line Text
Procedure:
Open Employee Lifecycle table
Go to Columns
Click New
Define field type
Save
🔹 Step 5: Service Catalog Item Creation
Navigation:
Service Catalog → Catalog Definitions → Maintain Items → New

Catalog Item:
Name: Onboard/Offboard Employee

Configuration:
Catalog → Service Catalog
Category → Services
Short Description → Employee onboarding/offboarding
🔹 Step 6: Variables Configuration
Required Variables:
Variable	Type
Requested for	Reference (sys_user)
Employee ID	Single Line Text
Department	Reference
Joining Date	Date
Exit Date	Date
Manager	Reference
Request Type	Choice
Assets Needed	Multiple Choice
Special Access	Multi-line Text
Assets to Collect	Multiple Choice
Access Revocations	Multi-line Text
🔹 Request Type Choices:
Onboarding
Offboarding
🔹 Asset Choices:
Laptop
Monitor
Headset
Phone
Access Card
Mobile Device
🔹 Step 7: UI Policy Configuration
Purpose:
Dynamically display fields based on selected Request Type.

Policy 1:
Show Joining Date for Onboarding
Condition: Request Type = Onboarding
Action: Joining Date → Visible = True
Policy 2:
Show Exit Date for Offboarding
Condition: Request Type = Offboarding
Action: Exit Date → Visible = True
Navigation:
Service Catalog → Maintain Items → Catalog UI Policies

🔹 Step 8: Flow Designer Configuration
Navigation:
Flow Designer → New Flow

Flow Name:
on or off Boarding Flow

🔹 Trigger Configuration
Trigger Type:
Service Catalog

Condition:
Catalog Item = Onboard/Offboard Employee

🔹 Main Flow Actions
1. Create Employee Lifecycle Record
Table:
u_employee_lifecycle

Field Mapping:
Requested for
Employee ID
Department
Joining Date
Manager
Request Type
Status = New
RITM = Requested Item Record
2. Ask for Approval
Approver:
Manager

Approval Rule:
Anyone approves

3. Create IT Task
Table:
sc_task

Details:
Short Description: Create accounts & assign hardware
Assignment Group: IT – Account Provisioning
Due Date: Joining Date - 1 day
4. Create Facilities Task
Details:
Short Description: Prepare workspace
Assignment Group: Facilities – Workspace
Due Date: Joining Date - 1 day
5. Create Security Task
Details:
Short Description: Issue ID badge & building access
Assignment Group: Security – Access
Due Date: Joining Date
6. Wait for Condition
Table:
sc_task

Condition:
All tasks linked to RITM are Closed Complete

7. Update Employee Lifecycle Record
Status:
Completed

8. Update Requested Item
State:
Closed Complete

9. Send Notification
Recipients:
HR Team
Requester
Message:
“Onboarding complete”

🔹 Rejection Path
If manager rejects:

Update lifecycle status → Rejected
Close request
Notify requester and HR
🔹 Step 9: Testing
Validate:
Catalog item visibility
Variable behavior
UI Policy conditions
Approval workflow
Task generation
Lifecycle tracking
Notifications
📌 Final Outcome
This project delivers:

✅ Automated onboarding ✅ Automated offboarding ✅ Departmental coordination ✅ Approval hierarchy ✅ Real-time task tracking ✅ Improved HR efficiency ✅ Reduced operational errors

🚀 Technologies Used
ServiceNow
Flow Designer
Service Catalog
UI Policies
Custom Tables
Roles & Groups
Approval Engine
📂 Project Modules
User Administration
Employee Lifecycle Table
Catalog Item
Variable Management
UI Policies
Flow Automation
Task Management
Notifications
🏁 Conclusion
The Employee Lifecycle Automation system provides an end-to-end enterprise solution for managing onboarding and offboarding workflows efficiently within ServiceNow.

It ensures process standardization, accountability, and seamless collaboration across HR, IT, Facilities, and Security teams.
