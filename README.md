# MediConnect

![PHP](https://img.shields.io/badge/PHP-8.2%2B-777BB4?style=flat-square&logo=php&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0%2B-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Blade](https://img.shields.io/badge/Blade-Templates-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-38B2AC?style=flat-square&logo=tailwindcss&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-7-646CFF?style=flat-square&logo=vite&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=php,laravel,mysql,tailwind,vite,js,git&theme=light" alt="Technologies used in MediConnect" />
  </a>
</p>

**MediConnect** is a web application for medical appointment management. The system allows patients, doctors, schedules, and appointments to be managed from a platform built with **Laravel**, **Blade**, **MySQL**, and role-based access control.

The project is designed to centralize the appointment workflow between patients, doctors, and administrators, allowing each type of user to access only the features required for their role within the system.

> Note: The application interface is currently in Spanish, as the project is designed for medical appointment management in Spanish-speaking environments.

## Table of Contents

- [Technologies](#technologies)
- [Overview](#overview)
- [Main Features](#main-features)
- [System Roles](#system-roles)
- [Domain Model](#domain-model)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Database](#database)
- [Running Locally](#running-locally)
- [Test Credentials](#test-credentials)
- [Useful Commands](#useful-commands)
- [Project Structure](#project-structure)
- [Technical Documentation](#technical-documentation)
- [Author](#author)
- [License](#license)

## Technologies

- **PHP 8.2+**
- **Laravel 12**
- **MySQL 8.0+**
- **Blade**
- **Tailwind CSS 4**
- **Vite 7**
- **JavaScript**
- **Laravel Session Auth**
- **Eloquent ORM**
- **Composer**
- **npm**

## Overview

MediConnect was developed as a web solution to organize medical appointment management between patients and healthcare professionals. Its goal is to replace manual or scattered processes with a centralized, traceable, browser-accessible platform.

The application includes authentication, role-based authorization, personalized dashboards, doctor management, schedule management, appointment booking, appointment status updates, and control over active or inactive users.

The system follows Laravel's **MVC** architecture, separating business logic into controllers, data persistence into Eloquent models, and presentation into Blade views.

## Main Features

### Authentication and authorization

- User registration.
- Login and logout.
- Session-based authentication with Laravel.
- Route protection through middleware.
- Role-based access control.
- Custom `CheckRole` middleware.
- User redirection according to role.
- Active user validation before allowing access to the system.

### User management

- System user administration.
- Available roles:
  - Patient.
  - Doctor.
  - Administrator.
- User account activation and deactivation.
- Relationship between users and medical profiles.
- Access control based on active or inactive status.
- Soft delete support for users.
- Administrative account management from the admin panel.

### Doctor management

- Doctor registration with professional information.
- Association between doctor and user.
- Medical license number.
- Medical specialty.
- Professional biography.
- Profile photo or profile image URL.
- Active or inactive status.
- Soft delete support to deactivate doctors without permanently deleting their information.
- Restoration of deactivated doctors.
- Automatic synchronization between the doctor profile and its related user.

### Availability schedules

- Schedule registration by doctor.
- Configuration by day of the week.
- Start time and end time.
- Appointment intervals.
- Schedule activation and deactivation.
- Direct relationship between schedules and doctors.
- Base structure to validate availability when booking appointments.

### Medical appointment system

- Appointment booking by patients.
- Association between appointment, patient, and doctor.
- Appointment date and time.
- Consultation reason.
- Additional notes.
- Appointment statuses:
  - Pending.
  - Confirmed.
  - Attended.
  - Cancelled.
- Appointment cancellation.
- Status confirmation or update by doctors.
- Appointment history by patient.
- Upcoming and past appointment views.

### Patient dashboard

- Personalized view for patients.
- Daily appointment summary.
- Pending appointment count.
- Confirmed appointment count.
- Upcoming appointment list.
- Appointment history.
- Doctor information associated with each appointment.
- Access to booking and managing personal appointments.

### Doctor dashboard

- Personalized view for doctors.
- Assigned appointment list.
- Appointments pending confirmation.
- Confirmed appointments.
- Attended appointments.
- Daily schedule.
- Weekly schedule.
- Appointment status updates.
- Patient information for each appointment.
- Time slot generation for the medical workday.

### Administrative panel

- General dashboard for administrators.
- Doctor management.
- User management.
- Schedule management.
- System-wide appointment overview.
- Management of active and inactive doctors.
- Administrative actions to activate, deactivate, edit, or delete records.
- General system statistics.

### Observers and automatic synchronization

- Observers used to automate logic related to doctors and users.
- User role synchronization when a doctor is created, deactivated, or restored.
- When a doctor is deactivated, the related user can be moved to an inactive state.
- When a doctor is restored, the related user can recover the doctor role and active status.
- Important changes are registered through logs.
- Automatic logic is kept separated from controllers.

### Security and validation

- CSRF protection in forms.
- Password hashing.
- SQL Injection prevention through Eloquent ORM.
- Automatic data escaping in Blade views.
- Form validations.
- Route restrictions by role.
- Future appointment date validation.
- Appointment status validation.
- Prevention of unauthorized operations.

## System Roles

MediConnect uses roles to separate responsibilities and permissions within the application.

| Role | Description |
| --- | --- |
| `admin` | Has access to the administrative panel, user management, doctor management, schedules, and appointments. |
| `doctor` | Can review assigned appointments, manage appointment statuses, and view the medical schedule. |
| `patient` | Can book appointments, review upcoming appointments, and view appointment history. |

## Domain Model

The system is organized around the main entities of a medical appointment platform.

| Entity | Purpose |
| --- | --- |
| `User` | Represents system users and stores authentication data, role, and account status. |
| `Doctor` | Represents the professional profile of a doctor associated with a user. |
| `Schedule` | Defines the availability schedules of each doctor. |
| `Appointment` | Represents a medical appointment between a patient and a doctor. |

### Main relationships

- A `User` may have a `Doctor` profile.
- A `User` with the patient role may have many `Appointment` records.
- A `Doctor` belongs to a `User`.
- A `Doctor` may have many `Appointment` records.
- A `Doctor` may have many `Schedule` records.
- An `Appointment` belongs to a patient and to a doctor.
- A `Schedule` belongs to a doctor.

## Prerequisites

Before installing the project, make sure you have the following installed:

- PHP 8.2 or higher.
- Composer.
- MySQL 8.0 or higher.
- Node.js.
- npm.
- Git.

Recommended PHP extensions for running Laravel with MySQL:

```ini
extension=curl
extension=fileinfo
extension=mbstring
extension=openssl
extension=pdo_mysql
extension=mysqli
extension=zip
```

## Installation

Clone the repository:

```bash
git clone https://github.com/CristoferGuillen/Gestion-Citas-Medicas.git
```

Enter the project folder:

```bash
cd Gestion-Citas-Medicas
```

Install PHP dependencies:

```bash
composer install
```

Install JavaScript dependencies:

```bash
npm install
```

Copy the environment file:

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Generate the application key:

```bash
php artisan key:generate
```

## Configuration

Edit the `.env` file and configure the main application values:

```env
APP_NAME=MediConnect
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:8000
```

Configure the MySQL connection:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=mediconnect
DB_USERNAME=root
DB_PASSWORD=your_password
```

Create a database named `mediconnect` before running the migrations.

You can create it from MySQL with:

```sql
CREATE DATABASE mediconnect CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

## Database

Run the migrations:

```bash
php artisan migrate
```

Load the initial data:

```bash
php artisan db:seed
```

You can also reset the database and load seeders in a single command:

```bash
php artisan migrate:fresh --seed
```

> Warning: `migrate:fresh --seed` deletes the existing tables, runs all migrations again, and loads the test data.

### Available seeders

The project includes seeders to create initial development data:

| Seeder | Description |
| --- | --- |
| `DatabaseSeeder` | Main seeder that runs the general data loading process. |
| `DoctorSeeder` | Creates test doctors with related user accounts. |
| `ScheduleSeeder` | Creates availability schedules for doctors. |
| `AppointmentSeeder` | Creates sample medical appointments with different statuses. |

## Running Locally

Run the complete development environment with:

```bash
composer run dev
```

You can also run Laravel and Vite separately.

Terminal 1:

```bash
php artisan serve
```

Terminal 2:

```bash
npm run dev
```

Then open the application at:

```text
http://localhost:8000
```

Main routes:

```text
http://localhost:8000/login
http://localhost:8000/register
http://localhost:8000/dashboard
http://localhost:8000/admin/dashboard
http://localhost:8000/doctor/dashboard
http://localhost:8000/paciente/dashboard
```

## Test Credentials

When running the seeders, the project creates initial users to test the main system roles.

| Role | Email | Password |
| --- | --- | --- |
| Administrator | `admin@example.com` | `password123` |
| Doctor | `carlos.perez@hospital.com` | `password123` |
| Doctor | `maria.gonzalez@hospital.com` | `password123` |
| Doctor | `juan.rodriguez@hospital.com` | `password123` |

Test patients may be generated through factories and seeders. Check the database after running `php artisan db:seed` to review the generated patient accounts.

## Useful Commands

Run migrations:

```bash
php artisan migrate
```

Run seeders:

```bash
php artisan db:seed
```

Recreate the database with initial data:

```bash
php artisan migrate:fresh --seed
```

Start the local server:

```bash
php artisan serve
```

Run Vite:

```bash
npm run dev
```

Build assets for production:

```bash
npm run build
```

Run the complete development environment:

```bash
composer run dev
```

Run tests:

```bash
php artisan test
```

Run the Composer test script:

```bash
composer test
```

## Project Structure

```text
Gestion-Citas-Medicas/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Admin/
│   │   │   │   ├── AdminDashboardController.php
│   │   │   │   ├── AppointmentController.php
│   │   │   │   ├── DoctorController.php
│   │   │   │   ├── ScheduleController.php
│   │   │   │   └── UserController.php
│   │   │   ├── Auth/
│   │   │   │   ├── LoginController.php
│   │   │   │   └── RegisterController.php
│   │   │   ├── AppointmentController.php
│   │   │   ├── DashboardController.php
│   │   │   ├── DoctorDashboardController.php
│   │   │   └── PatientDashboardController.php
│   │   ├── Middleware/
│   │   │   └── CheckRole.php
│   │   └── Requests/
│   ├── Models/
│   │   ├── Appointment.php
│   │   ├── Doctor.php
│   │   ├── Schedule.php
│   │   └── User.php
│   ├── Observers/
│   └── Providers/
│
├── database/
│   ├── factories/
│   ├── migrations/
│   │   ├── create_users_table.php
│   │   ├── create_doctors_table.php
│   │   ├── create_appointments_table.php
│   │   ├── create_schedules_table.php
│   │   ├── add_soft_deletes_to_doctors_table.php
│   │   └── add_soft_deletes_to_users_table.php
│   └── seeders/
│       ├── AppointmentSeeder.php
│       ├── DatabaseSeeder.php
│       ├── DoctorSeeder.php
│       └── ScheduleSeeder.php
│
├── public/
├── resources/
│   ├── css/
│   ├── js/
│   └── views/
│
├── routes/
│   ├── console.php
│   └── web.php
│
├── storage/
├── tests/
├── .env.example
├── artisan
├── composer.json
├── package.json
├── phpunit.xml
├── TECHNICAL_DOCUMENTATION.md
└── vite.config.js
```

## Technical Documentation

The repository includes additional technical documentation in:

```text
TECHNICAL_DOCUMENTATION.md
```

This documentation describes in greater detail:

- MVC architecture.
- Models and relationships.
- Observers.
- Soft deletes.
- Authorization middleware.
- Business workflows.
- Status management.
- Technical implementation details.

## Author

Developed by **Cristofer Guillen**.

- GitHub: [@CristoferGuillen](https://github.com/CristoferGuillen)
- Repository: [Gestion-Citas-Medicas](https://github.com/CristoferGuillen/Gestion-Citas-Medicas)

## License

This project is available under the **MIT** license.
