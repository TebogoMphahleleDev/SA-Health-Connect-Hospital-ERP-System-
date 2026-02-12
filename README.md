# SA Health Connect

**Digitizing South African hospitals for efficiency, transparency, and better patient care.**

🏥 **SA Health Connect** is a modern, full-featured Hospital ERP system designed specifically to address the systemic challenges in South Africa's public healthcare facilities — including long patient waiting times, medicine and supply shortages, staff understaffing & burnout, poor emergency response coordination, lost paperwork, inefficient resource tracking, and limited transparency/accountability.

### Key Challenges Addressed
South African public hospitals frequently face:
- Prolonged waiting times due to manual processes, overcrowding, and poor scheduling
- Chronic shortages of essential medicines, equipment, and even basics like linen
- Severe staff shortages, high turnover, and inefficient shift/attendance management
- Inefficient emergency handling and ambulance coordination
- Lost or inaccessible patient records, leading to repeated tests and errors
- Poor visibility into hospital KPIs, leading to mismanagement and corruption risks
- Inadequate real-time communication between departments, patients, and staff

By digitizing core workflows, the system aims to reduce administrative burden, improve resource allocation, enhance patient safety, and support better governance.

### Tech Stack
- **Frontend**: Angular 17 + Angular Material + RxJS
- **Backend**: Spring Boot 3 + Spring Security (JWT-based authentication & authorization)
- **Database**: PostgreSQL (with relational integrity for complex workflows)

### Modules Overview & Workflows

#### 1. Ambulance & Emergency Management
**Goal**: Real-time tracking, faster response, hospital preparation, and prioritization of critical cases.

**Workflow**: Request → Assignment → Pickup → In-Transit → Hospital Alert → Arrival

- Patient/app submits emergency (GPS + type)
- Nearest available ambulance assigned
- Live GPS tracking (patient app + hospital dashboard)
- Paramedic marks "Patient Onboard"
- Real-time vitals/status updates → dynamic ETA & hospital prep (e.g., trauma team activation for high-priority cases)

**Entities**: Ambulance, EmergencyRequest, LocationLog, HospitalAlert  
**Key APIs**: `/ambulance/request`, `/ambulance/update-location`, `/ambulance/pickup`, `/hospital/alert`, `/ambulance/eta`  
**Frontend**: Request form, live map, transit status, alert panel

#### 2. Patient Management & Digital Records
**Goal**: Eliminate lost paperwork, centralize history, secure document access.

**Workflow**: Admission → Profile Creation → History Access → Document Upload/Download

- Unique patient ID generation
- Full history (allergies, visits, prescriptions)
- Secure upload/view of PDFs/scans
- Role-based access + audit logs

**Entities**: Patient, MedicalHistory, DocumentUpload  
**Key APIs**: `/patients/{id}`, `/patients/upload-doc`, `/patients/{id}/documents`  
**Frontend**: Profile view, history timeline, upload component

#### 3. Pharmacy & Pill Collection
**Goal**: Minimize queues, enable scheduled pickups, prevent errors via verification.

**Workflow**: Prescription → Queue → Notification → QR Pickup → Collection

- Doctor creates prescription
- Pharmacy queue + slot booking
- SMS/push notification to patient
- QR scan confirms collection

**Entities**: Prescription, PharmacyQueue  
**Key APIs**: `/prescription/create`, `/prescription/{patientId}`, `/prescription/collect`, `/queue/status`  
**Frontend**: Prescription list, scan interface, booking form

#### 4. Hospital Kitchen & Meal Management
**Goal**: Safe, correct diet delivery with allergy checks and verification.

**Workflow**: Diet Profile → Meal Prep → Scan & Delivery → Confirmation

- Patient diet/allergy linked
- Ward-based prep
- Wristband/QR scan verifies meal
- Mismatch alerts

**Entities**: Meal, DietType, DeliveryLog  
**Key APIs**: `/meals/{wardId}/{date}`, `/meals/delivered`  
**Frontend**: Kitchen dashboard, scan component

#### 5. Staff Management & Attendance
**Goal**: Accurate clock-in/out, shift planning, automated payroll.

**Workflow**: Clock-In → Shift Tracking → Hours Calculation → Payroll

- App/kiosk clocking
- Shift scheduling & swap requests
- Auto payroll with deductions/bonuses

**Entities**: Staff, Attendance, Shift, Payroll  
**Key APIs**: `/staff/clockin`, `/staff/clockout`, `/staff/attendance`, `/staff/payroll`  
**Frontend**: Dashboard, shift calendar, payroll summary

#### 6. Appointments & Scheduling
**Goal**: Reduce no-shows and optimize doctor time.

**Workflow**: Request → Availability Check → Booking → Reminders

- Patient selects doctor/slot
- Real-time availability
- Notifications & reschedule/cancel

**Entities**: Appointment, DoctorSchedule  
**Key APIs**: `/appointments`, `/appointments/{doctorId}`, `/appointments/cancel`  
**Frontend**: Calendar, list view, notifications

#### 7. Reporting & Analytics
**Goal**: Data-driven decisions, KPIs, compliance audits.

**Workflow**: Data Aggregation → Reports → Visual Dashboard

- KPIs: wait times, response times, stock levels, bed occupancy, etc.
- Audit logs for transparency

**Entities**: Report, Log  
**Key APIs**: `/reports/kpi`, `/reports/logs`  
**Frontend**: Charts, tables, alerts

### High-Level Database Schema
```sql
users
patients
ambulances
emergency_requests
location_logs
prescriptions
pharmacy_queue
meals
diet_types
delivery_logs
staff
attendance
shifts
payroll
appointments
doctor_schedules
reports
audit_logs
