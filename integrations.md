# Integrations

## 1. Overview

Bloom consists of several connected components that work together through the backend API.

```text
Bloom Mobile
      |
      | API
      |
Bloom Backend
      |
      | Database
      |
PostgreSQL

Bloom Dashboard
      |
      | API
      |
Bloom Backend
```

The informational website is separate from the authenticated applications.

---

## 2. Mobile and Backend

The Bloom mobile application communicates with the backend through API services.

The integration supports functionality such as:

- Authentication
- User information
- Maternal profiles
- Symptom logging
- Care schedules
- Maternal health tips
- Location functionality
- Alerts and notifications

The mobile application does not communicate directly with PostgreSQL.

---

## 3. Dashboard and Backend

The administrative dashboard also communicates with the backend API.

The integration supports:

- Administrator authentication
- User management
- Content management
- Growth and engagement metrics
- Safety and alerts
- Account settings

The dashboard does not directly access the database.

---

## 4. Backend and PostgreSQL

The backend communicates with PostgreSQL for persistent application data.

```text
Client Application
       |
       | API request
       |
Bloom Backend
       |
       | Database operation
       |
PostgreSQL
```

The backend is responsible for processing requests before data is stored or retrieved.

---

## 5. Location Integration

Location-related functionality is handled through the backend.

The backend includes location functionality and a distance calculation module:

```text
backend/
|
|-- distance.py
|
\-- bloom/
    |
    \-- routers/
        |
        \-- location.py
```

Location information is exchanged through the API rather than through direct database access from the mobile application.

---

## 6. Email Integration

The backend contains email functionality in:

```text
backend/
|
\-- email.py
```

Email-related operations are handled by the backend as part of the platform's server-side functionality.

---

## 7. Notifications

Notification functionality is included in the mobile application under:

```text
mobile/
|
\-- lib/
    |
    \-- services/
        |
        \-- notifications/
```

Notifications support the reminder and alert functionality available within the application.

---

## 8. Informational Website

Bloom also has a public informational website.

**Informational Website:**

[Visit the Bloom Informational Website →](https://bloom-rho-sand.vercel.app/)

The website is separate from the mobile application and administrative dashboard.

---

## 9. Integration Flow

The main integration between Bloom components can be summarized as:

```text
Mobile Application
       |
       | API
       |
       +----------------+
                        |
                        |
                  Bloom Backend
                        |
                        | Database
                        |
                   PostgreSQL
                        |
                        |
       +----------------+
       |
       | API
       |
Administrative Dashboard
```

This allows the mobile application and dashboard to use the same backend and centralized data storage.

---

## 10. Related Documentation

- [System Architecture](architecture.md)
- [Backend API](backend-api.md)
- [Database](database.md)
- [Mobile Application](mobile.md)
- [Administrative Dashboard](frontend-web.md)