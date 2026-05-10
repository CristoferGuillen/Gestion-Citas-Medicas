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
    <img src="https://skillicons.dev/icons?i=php,laravel,mysql,tailwind,vite,js,git&theme=light" alt="Tecnologías utilizadas en MediConnect" />
  </a>
</p>

**MediConnect** es una aplicación web para la gestión de citas médicas. El sistema permite administrar pacientes, doctores, horarios de disponibilidad y reservas de citas desde una plataforma construida con **Laravel**, **Blade**, **MySQL** y control de acceso basado en roles.

El proyecto está diseñado para centralizar el flujo de atención entre pacientes, doctores y administradores, permitiendo que cada tipo de usuario acceda únicamente a las funcionalidades necesarias según su rol dentro del sistema.

> Nota: La interfaz de la aplicación está actualmente en español, ya que el proyecto está orientado a entornos médicos hispanohablantes.

## Tabla de Contenidos

- [Tecnologías](#tecnologías)
- [Descripción General](#descripción-general)
- [Características Principales](#características-principales)
- [Roles del Sistema](#roles-del-sistema)
- [Modelo de Dominio](#modelo-de-dominio)
- [Requisitos Previos](#requisitos-previos)
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Base de Datos](#base-de-datos)
- [Ejecución Local](#ejecución-local)
- [Credenciales de Prueba](#credenciales-de-prueba)
- [Comandos Útiles](#comandos-útiles)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Documentación Técnica](#documentación-técnica)
- [Autor](#autor)
- [Licencia](#licencia)

## Tecnologías

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

## Descripción General

MediConnect fue desarrollado como una solución web para organizar la gestión de citas médicas entre pacientes y profesionales de salud. Su objetivo es reemplazar procesos manuales o desorganizados por una plataforma centralizada, trazable y accesible desde el navegador.

La aplicación implementa autenticación, autorización por roles, dashboards personalizados, administración de doctores, gestión de horarios, creación de citas, actualización de estados y control de usuarios activos e inactivos.

El sistema se apoya en el patrón **MVC** de Laravel, separando la lógica de negocio en controladores, la persistencia de datos en modelos Eloquent y la presentación en vistas Blade.

## Características Principales

### Autenticación y autorización

- Registro de nuevos usuarios.
- Inicio y cierre de sesión.
- Autenticación basada en sesiones de Laravel.
- Protección de rutas mediante middleware.
- Control de acceso basado en roles.
- Middleware personalizado `CheckRole`.
- Redirección de usuarios según su rol.
- Validación de usuarios activos antes de permitir acceso al sistema.

### Gestión de usuarios

- Administración de usuarios del sistema.
- Roles disponibles:
  - Paciente.
  - Doctor.
  - Administrador.
- Activación y desactivación de cuentas.
- Relación entre usuarios y perfiles médicos.
- Control de acceso según estado activo o inactivo.
- Soporte para soft deletes en usuarios.
- Gestión administrativa de cuentas desde el panel de administrador.

### Gestión de doctores

- Registro de doctores con datos profesionales.
- Asociación entre doctor y usuario.
- Número de licencia médica.
- Especialidad médica.
- Biografía profesional.
- Foto o URL de imagen de perfil.
- Estado activo o inactivo.
- Soft delete para desactivar doctores sin eliminar definitivamente la información.
- Restauración de doctores desactivados.
- Sincronización automática entre el perfil del doctor y su usuario asociado.

### Horarios de disponibilidad

- Registro de horarios por doctor.
- Configuración por día de la semana.
- Hora de inicio y hora de finalización.
- Intervalos de atención.
- Activación o desactivación de horarios.
- Relación directa entre horarios y doctores.
- Base para validar disponibilidad al momento de reservar citas.

### Sistema de citas médicas

- Reserva de citas por pacientes.
- Asociación entre cita, paciente y doctor.
- Fecha y hora de la cita.
- Motivo de consulta.
- Notas adicionales.
- Estados de cita:
  - Pendiente.
  - Confirmada.
  - Atendida.
  - Cancelada.
- Cancelación de citas.
- Confirmación o actualización del estado por parte del doctor.
- Historial de citas por paciente.
- Visualización de citas próximas y anteriores.

### Dashboard de paciente

- Vista personalizada para pacientes.
- Resumen de citas del día.
- Conteo de citas pendientes.
- Conteo de citas confirmadas.
- Listado de próximas citas.
- Historial de citas.
- Información del doctor asociado a cada cita.
- Acceso a la reserva y gestión de citas propias.

### Dashboard de doctor

- Vista personalizada para doctores.
- Listado de citas asignadas.
- Citas pendientes de confirmación.
- Citas confirmadas.
- Citas atendidas.
- Agenda diaria.
- Agenda semanal.
- Actualización del estado de citas.
- Visualización de pacientes asociados a las citas.
- Generación de bloques horarios para la jornada médica.

### Panel administrativo

- Dashboard general para administradores.
- Gestión de doctores.
- Gestión de usuarios.
- Gestión de horarios.
- Visualización de citas del sistema.
- Administración de doctores activos e inactivos.
- Acciones administrativas para activar, desactivar, editar o eliminar registros.
- Estadísticas generales del sistema.

### Observers y sincronización automática

- Uso de observers para automatizar lógica relacionada con doctores y usuarios.
- Sincronización del rol de usuario cuando se crea, desactiva o restaura un doctor.
- Al desactivar un doctor, el usuario asociado puede pasar a estado inactivo.
- Al restaurar un doctor, el usuario asociado puede recuperar su rol y estado activo.
- Registro de cambios importantes mediante logs.
- Separación de lógica automática fuera de los controladores.

### Seguridad y validaciones

- Protección CSRF en formularios.
- Hashing de contraseñas.
- Protección contra SQL Injection mediante Eloquent ORM.
- Escapado automático de datos en vistas Blade.
- Validaciones de formularios.
- Restricción de rutas según rol.
- Validación de citas futuras.
- Validación de estados permitidos para citas.
- Prevención de operaciones no autorizadas.

## Roles del Sistema

MediConnect utiliza roles para separar responsabilidades y permisos dentro de la aplicación.

| Rol | Descripción |
| --- | --- |
| `admin` | Tiene acceso al panel administrativo, gestión de usuarios, doctores, horarios y citas. |
| `doctor` | Puede revisar sus citas, gestionar estados de atención y visualizar su agenda médica. |
| `patient` | Puede reservar citas, consultar sus próximas citas y revisar su historial. |

## Modelo de Dominio

El sistema está organizado alrededor de las principales entidades de una plataforma de citas médicas.

| Entidad | Propósito |
| --- | --- |
| `User` | Representa a los usuarios del sistema y almacena datos de autenticación, rol y estado. |
| `Doctor` | Representa el perfil profesional de un doctor asociado a un usuario. |
| `Schedule` | Define los horarios de disponibilidad de cada doctor. |
| `Appointment` | Representa una cita médica entre un paciente y un doctor. |

### Relaciones principales

- Un `User` puede tener un perfil de `Doctor`.
- Un `User` con rol de paciente puede tener muchas `Appointment`.
- Un `Doctor` pertenece a un `User`.
- Un `Doctor` puede tener muchas `Appointment`.
- Un `Doctor` puede tener muchos `Schedule`.
- Una `Appointment` pertenece a un paciente y a un doctor.
- Un `Schedule` pertenece a un doctor.

## Requisitos Previos

Antes de instalar el proyecto, asegúrate de tener instalado:

- PHP 8.2 o superior.
- Composer.
- MySQL 8.0 o superior.
- Node.js.
- npm.
- Git.

Extensiones PHP recomendadas para ejecutar Laravel con MySQL:

```ini
extension=curl
extension=fileinfo
extension=mbstring
extension=openssl
extension=pdo_mysql
extension=mysqli
extension=zip
```

## Instalación

Clona el repositorio:

```bash
git clone https://github.com/CristoferGuillen/Gestion-Citas-Medicas.git
```

Entra a la carpeta del proyecto:

```bash
cd Gestion-Citas-Medicas
```

Instala las dependencias de PHP:

```bash
composer install
```

Instala las dependencias de JavaScript:

```bash
npm install
```

Copia el archivo de entorno:

```bash
cp .env.example .env
```

En Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Genera la clave de la aplicación:

```bash
php artisan key:generate
```

## Configuración

Edita el archivo `.env` y configura los valores principales de la aplicación:

```env
APP_NAME=MediConnect
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:8000
```

Configura la conexión a MySQL:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=mediconnect
DB_USERNAME=root
DB_PASSWORD=your_password
```

Crea una base de datos llamada `mediconnect` antes de ejecutar las migraciones.

Puedes crearla desde MySQL con:

```sql
CREATE DATABASE mediconnect CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

## Base de Datos

Ejecuta las migraciones:

```bash
php artisan migrate
```

Carga los datos iniciales:

```bash
php artisan db:seed
```

También puedes recrear la base de datos y cargar los seeders en un solo comando:

```bash
php artisan migrate:fresh --seed
```

> Advertencia: `migrate:fresh --seed` elimina las tablas existentes, vuelve a ejecutar las migraciones y carga nuevamente los datos de prueba.

### Seeders disponibles

El proyecto incluye seeders para crear datos iniciales de desarrollo:

| Seeder | Descripción |
| --- | --- |
| `DatabaseSeeder` | Seeder principal que ejecuta la carga general de datos. |
| `DoctorSeeder` | Crea doctores de prueba con usuarios asociados. |
| `ScheduleSeeder` | Crea horarios de disponibilidad para los doctores. |
| `AppointmentSeeder` | Crea citas médicas de ejemplo con distintos estados. |

## Ejecución Local

Puedes ejecutar el entorno de desarrollo completo con:

```bash
composer run dev
```

También puedes ejecutar Laravel y Vite por separado.

Terminal 1:

```bash
php artisan serve
```

Terminal 2:

```bash
npm run dev
```

Luego abre la aplicación en:

```text
http://localhost:8000
```

Rutas principales:

```text
http://localhost:8000/login
http://localhost:8000/register
http://localhost:8000/dashboard
http://localhost:8000/admin/dashboard
http://localhost:8000/doctor/dashboard
http://localhost:8000/paciente/dashboard
```

## Credenciales de Prueba

Al ejecutar los seeders, el proyecto crea usuarios iniciales para probar los roles principales del sistema.

| Rol | Email | Contraseña |
| --- | --- | --- |
| Administrador | `admin@example.com` | `password123` |
| Doctor | `carlos.perez@hospital.com` | `password123` |
| Doctor | `maria.gonzalez@hospital.com` | `password123` |
| Doctor | `juan.rodriguez@hospital.com` | `password123` |

Los pacientes de prueba pueden generarse mediante factories y seeders. Revisa la base de datos después de ejecutar `php artisan db:seed` para consultar los correos creados.

## Comandos Útiles

Ejecutar migraciones:

```bash
php artisan migrate
```

Ejecutar seeders:

```bash
php artisan db:seed
```

Recrear la base de datos con datos iniciales:

```bash
php artisan migrate:fresh --seed
```

Iniciar el servidor local:

```bash
php artisan serve
```

Ejecutar Vite:

```bash
npm run dev
```

Compilar assets para producción:

```bash
npm run build
```

Ejecutar el entorno completo de desarrollo:

```bash
composer run dev
```

Ejecutar tests:

```bash
php artisan test
```

Ejecutar el script de pruebas definido en Composer:

```bash
composer test
```

## Estructura del Proyecto

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

## Documentación Técnica

El repositorio incluye documentación técnica adicional en:

```text
TECHNICAL_DOCUMENTATION.md
```

Esta documentación describe con mayor detalle:

- Arquitectura MVC.
- Modelos y relaciones.
- Observers.
- Soft deletes.
- Middleware de autorización.
- Flujos de negocio.
- Gestión de estados.
- Implementación técnica del proyecto.

## Autor

Desarrollado por **Cristofer Guillen**.

- GitHub: [@CristoferGuillen](https://github.com/CristoferGuillen)
- Repositorio: [Gestion-Citas-Medicas](https://github.com/CristoferGuillen/Gestion-Citas-Medicas)

## Licencia

Este proyecto está disponible bajo la licencia **MIT**.
