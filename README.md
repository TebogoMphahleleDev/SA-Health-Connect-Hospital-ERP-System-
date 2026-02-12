# SA-Health-Connect-Hospital-ERP-System-

🏥 SA Health Connect – Full Hospital ERP Planning with Workflows

Tagline: Digitizing South African hospitals for efficiency, transparency, and patient care.

Tech Stack:

Frontend: Angular 17 + Angular Material + RxJS

Backend: Spring Boot 3 + Spring Security (JWT)

Database: PostgreSQL

Optional Mobile: Ionic

DevOps: Docker, GitHub/GitLab, CI/CD

 Modules Overview & Workflows

We’ll define modules, backend entities & APIs, frontend components, and detailed workflows for each.

1️ Ambulance & Emergency Management

Goal: Real-time ambulance tracking, patient pickup, hospital prep, emergency prioritization.

Workflow: Ambulance Request → Pickup → Hospital Alert

Patient submits emergency request via app (GPS captured, emergency type).

System assigns nearest available ambulance.

Ambulance en route: live GPS tracking → displayed on patient app & hospital dashboard.

Paramedic arrives → verifies patient location → presses “Patient onboard”.

System updates status → In Transit → triggers Hospital Alert:

Patient info (name, ID, emergency type)

ETA

Vitals if available

Hospital workflow:

Normal emergency: relevant staff notified

High-level emergency: all available doctors scrambled → trauma room prepared

Paramedics update patient condition en route → hospital prep adjusts in real-time

Backend Entities & APIs:

Ambulance, EmergencyRequest, LocationLog, HospitalAlert

APIs:

POST /ambulance/request

PUT /ambulance/{id}/update-location

POST /ambulance/pickup

POST /hospital/alert

GET /ambulance/{requestId}/eta

Frontend Components:

ambulance-request-form, ambulance-map, transit-status, hospital-alert-panel

2️ Patient Management & Digital Records

Goal: Reduce lost paperwork, manage history, upload/download medical documents.

Workflow: Patient Admission → Record Access → Document Upload

Patient profile created → unique patient ID.

Doctors and nurses access patient history → prescriptions, previous visits, allergies.

Upload medical documents → PDFs or scans.

Role-based access → only authorized personnel view sensitive data.

Hospital admin can audit logs for compliance.

Backend Entities & APIs:

Patient, MedicalHistory, DocumentUpload

APIs:

GET /patients/{id} → fetch profile

POST /patients/upload-doc

GET /patients/{id}/documents

Frontend Components:

patient-profile, medical-history-view, document-upload

3️ Pharmacy / Pill Collection

Goal: Reduce queues, schedule pickups, QR verification.

Workflow: Prescription → Queue → Pickup → Notification

Doctor uploads prescription → system assigns patient ID.

Pharmacy receives prescription → adds to queue.

Patient receives SMS/notification → schedule pickup slot.

Patient arrives → QR scanned at pharmacy → marks collected.

System updates queue → next patient notified.

Backend Entities & APIs:

Prescription, PharmacyQueue

APIs:

POST /prescription/create

GET /prescription/{patientId}

PUT /prescription/{id}/collect

GET /queue/{pharmacyId}

Frontend Components:

prescription-list, pickup-scan, booking-form

4️ Hospital Kitchen & Meal Management

Goal: Ensure correct diet delivery, allergy safety, ward tracking.

Workflow: Diet → Meal Prep → Delivery → Confirmation

Patient dietary profile stored → allergies & diet type.

Kitchen prepares meals per ward → logs meals.

Delivery staff scan patient wristband → verifies meal.

Delivered status updated in ERP → alerts if mismatch.

Backend Entities & APIs:

Meal, DietType, DeliveryLog

APIs:

GET /meals/{wardId}/{date}

PUT /meals/{id}/delivered

Frontend Components:

meal-dashboard, meal-scan

5️ Staff Management & Attendance

Goal: Clock-in/out, payroll, scheduling, shift tracking.

Workflow: Staff Clock-In → Shift Tracking → Payroll

Staff clocks in via app / kiosk → timestamp stored.

Shifts scheduled → ERP tracks hours worked.

Payroll calculated automatically → includes bonuses, deductions.

Staff dashboard shows upcoming shifts & hours worked.

Backend Entities & APIs:

Staff, Attendance, Shift, Payroll

APIs:

POST /staff/clockin

POST /staff/clockout

GET /staff/attendance/{staffId}

GET /staff/payroll/{staffId}

Frontend Components:

attendance-dashboard, shift-view, payroll-view

6️ Appointments & Scheduling

Goal: Manage doctor appointments and availability.

Workflow: Appointment Request → Booking → Notification

Patient requests appointment → select doctor & time slot.

System checks doctor availability → confirms booking.

Notification sent to patient & doctor.

Doctor reschedules / cancels → system updates patient.

Backend Entities & APIs:

Appointment, DoctorSchedule

APIs:

POST /appointments

GET /appointments/{doctorId}

PUT /appointments/{id}/cancel

Frontend Components:

booking-calendar, appointment-list, notification-panel

7️ Reporting & Analytics

Goal: Provide hospital KPIs, audit logs, and management insights.

Workflow: Data → Reports → Dashboard

Backend aggregates hospital data → patients, staff, prescriptions, meals, ambulance response times.

Reports generated → daily/weekly/monthly.

Frontend dashboard shows KPIs → charts, tables, alerts.

Backend Entities & APIs:

Reports, Logs

APIs:

GET /reports/kpi

GET /reports/logs

Frontend Components:

dashboard-charts, audit-logs

 Database Schema (High-Level)
users
patients
ambulances
emergency_requests
location_logs
prescriptions
pharmacy_queue
meals
staff
attendance
shift
payroll
appointments
reports
logs


Relationships

Patient → Appointments (1:M)

Patient → Prescriptions (1:M)

Staff → Attendance (1:M)

Ambulance → EmergencyRequest (1:M)

Meal → Patient (M:1)
