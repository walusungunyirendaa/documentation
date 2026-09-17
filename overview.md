
# Bloom Platform Overview

## 1. Platform Overview

Bloom is a connected maternal health platform that brings together the mobile application, backend API, administrative dashboard, and informational website.

The platform follows a client-server architecture where client applications communicate with the backend API, while the backend manages application logic, authentication, data processing, and communication with the PostgreSQL database.

The main platform components are:

- **Bloom Mobile Application** - Flutter-based application used by mothers, caregivers, and Community Health Promoters (CHPs).
- **Bloom Backend API** - FastAPI-based backend responsible for application logic, data processing, authentication, and communication with the database.
- **Bloom Administrative Dashboard** - Web-based interface used by administrators to manage users, maternal health content, platform metrics, safety alerts, and account settings.
- **Bloom Informational Website** - Public website that provides information about Bloom, its purpose, features, and maternal health support services.

These components communicate through APIs to provide a connected maternal health ecosystem.

---

## 2. Platform Components

### Mobile Application

The Bloom mobile application provides role-specific functionality for:

- Mothers
- Caregivers
- Community Health Promoters (CHPs)

The mobile application provides functionality including:

- User authentication
- Maternal profile management
- Daily symptom logging
- Care scheduling
- Medication and appointment-related reminders
- Delivery date tracking
- Location functionality
- CHP interaction and location sharing
- Caregiver access to maternal information
- Maternal health tips
- Alerts and notifications

The mobile application communicates with the Bloom backend through the API layer.

---

### Backend API

The Bloom backend provides the central application services used by the mobile application and administrative dashboard.

The backend is implemented using **FastAPI** and provides functionality for:

- User management
- Authentication and authorization
- Maternal profiles
- Symptom management
- Symptom logging
- Care schedules
- Maternal health tips
- Location management
- Analytics
- Database access
- Email functionality
- Distance calculations
- API security and request handling

The backend communicates with the PostgreSQL database for persistent data storage.

---

### Administrative Dashboard

The Bloom administrative dashboard provides administrators with a centralized interface for managing and monitoring the platform.

The dashboard contains the following major areas:

- **Authentication**
- **Account Settings**
- **Content Management**
- **Metrics**
  - Growth and Engagement
  - Safety and Alerts
- **Users Management**

The dashboard communicates with the backend API to retrieve and update platform information.

---

### Informational Website

The Bloom informational website provides publicly accessible information about the Bloom platform, its purpose, features and maternal health support services.

The website serves as the public-facing information resource for Bloom and is separate from the authenticated administrative dashboard and mobile application.

**Informational Website:**  

[Visit the Bloom Informational Website →](https://bloom-rho-sand.vercel.app/)

---

## 3. User Roles

Bloom supports multiple user roles, each with a different interaction with the platform.

### Mother

The mother is the primary user of the Bloom platform.

The mother can:

- Maintain her maternal profile
- Log daily symptoms
- Manage care schedules
- View reminders
- Track pregnancy and delivery information
- Be linked to a Community Health Provider
- Receive maternal health tips

---

### Caregiver

Caregivers can access information associated with the mothers they support.

Caregiver functionality includes:

- Viewing maternal information made available to them
- Viewing maternal symptoms
- Receiving relevant alerts
- Monitoring the mother's health information through the application

---

### Community Health Promoter (CHP)

CHPs support mothers through the platform by monitoring relevant maternal information and responding to alerts.

CHP functionality includes:

- Viewing assigned mothers
- Monitoring maternal symptoms
- Receiving relevant alerts
- Viewing maternal information
- Using location information where required
- Accessing information needed to support maternal care

---

### Administrator

Administrators manage and monitor the Bloom platform through the administrative dashboard.

Administrator functionality includes:

- Managing users
- Managing maternal health content
- Viewing growth and engagement metrics
- Monitoring safety and alerts
- Managing administrator account settings

---

## 4. Core Platform Modules

The Bloom platform is organized around several functional modules.

| Module | Description |
|---|---|
| Authentication | Handles user authentication and access to platform functionality |
| User Management | Manages Bloom user information and roles |
| Maternal Profile | Stores and manages maternal health profile information |
| Symptom Management | Defines and manages maternal symptoms |
| Symptom Logging | Records symptoms submitted by mothers |
| Care Scheduling | Manages maternal care schedules and related reminders |
| Location | Handles relevant maternal and CHP location information |
| Maternal Tips | Provides maternal health information and recommendations |
| Analytics | Provides data used for platform metrics and monitoring |
| Notifications | Provides relevant reminders, alerts and notifications |

---

## 5. Client-to-API Communication

Both the mobile application and administrative dashboard communicate with the backend through HTTP API requests.

The general request flow is:

```text
Client Application

       │

       │ HTTP Request

   Backend API

       │

       ├── Authentication

       │

       ├── Validation

       │

       ├── Business Logic

       │

       └── Database Operation

              │

          PostgreSQL

              │

       Backend Response

              │

       Client Application
````

This architecture allows the client applications to access centralized application functionality without directly communicating with the database.

---

## 6. Data Persistence

Bloom uses PostgreSQL as its primary database.

Persistent application data includes information associated with:

* Users
* Maternal profiles
* Locations
* Symptoms
* Symptom logs
* Care schedules
* Maternal health tips
* Analytics-related information

The backend is responsible for interacting with the database and exposing the required information through API endpoints.

Client applications do not directly access the PostgreSQL database.

---

## 7. API Integration

The mobile application and administrative dashboard are integrated with the Bloom backend API.

API integration allows client applications to:

* Submit user information
* Retrieve user information
* Create and update maternal profiles
* Submit and retrieve symptom information
* Manage symptom logs
* Manage care schedules
* Retrieve maternal health tips
* Exchange relevant location information
* Retrieve analytics information
* Retrieve alerts and other platform information

The API therefore serves as the primary communication layer between the client applications and backend services.

---

## 8. Platform Architecture

At a high level, Bloom follows a client-server architecture consisting of:

1. **Presentation Layer**

   * Bloom Mobile Application
   * Bloom Administrative Dashboard

2. **Application Layer**

   * Bloom FastAPI Backend
   * API routers
   * Services
   * Repositories
   * Application configuration and security

3. **Data Layer**

   * PostgreSQL database

The separation of these layers allows the different parts of the platform to be developed and maintained independently while communicating through defined APIs.

---
