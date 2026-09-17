# Administrative Dashboard

## 1. Overview

The Bloom administrative dashboard is the web interface used by Bloom administrators.

It provides administrators with access to platform management, user management, content management, account settings, and platform metrics.

The dashboard is built using **Next.js** and communicates with the Bloom backend through the API.

The dashboard does not connect directly to the PostgreSQL database. All database operations are handled by the Bloom backend.

```text
Administrator

       |

       |

Admin Dashboard

       |

       | API requests

       |

   Bloom Backend

       |

       | Database operations

       |

   PostgreSQL
```

The dashboard is hosted using **Vercel**.

```text
Administrator

       |

       |

Hosted Bloom Dashboard

       |

       | HTTPS / API requests

       |

   Bloom Backend

       |

       |

   PostgreSQL
```

---

## 2. Technologies Used

The administrative dashboard uses the following technologies:

| Technology            | Purpose                                                 |
| --------------------- | ------------------------------------------------------- |
| Next.js               | Frontend web application framework                      |
| React                 | Building the dashboard user interface                   |
| JavaScript / JSX      | Application logic and UI components                     |
| CSS                   | Styling dashboard pages and components                  |
| Vercel                | Hosting and deployment of the dashboard                 |
| Bloom Backend API     | Communication with backend services                     |
| Environment Variables | Configuration of the backend API URL and other settings |

Next.js provides the application structure and routing for the administrative dashboard.

---

## 3. Dashboard Hosting

The Bloom administrative dashboard is deployed and hosted using **Vercel**.

Vercel provides the deployment environment for the Next.js application.

```text
Next.js Dashboard

       |

       | Build and Deployment

       v

     Vercel

       |

       | HTTPS

       v

Administrator
```

The hosted dashboard can be accessed through the following URL:


[Hosted Dashboard:](https://spyhive-dashboard.vercel.app)


The Vercel URL should be added here after deployment, for example:

```text
https://your-dashboard-name.vercel.app
```

The dashboard is deployed from the frontend project and is made available to authorized administrators through the hosted Vercel application.

---

## 4. Dashboard Project Structure

The dashboard is organized under the `admin` area of the Next.js application.

```text
frontend/
|
|-- app/
|   |
|   |-- admin/
|       |
|       |-- account-settings/
|       |
|       |-- auth/
|       |   |
|       |   `-- login/
|       |
|       |-- content-management/
|       |
|       |-- metrics/
|       |   |
|       |   |-- growth-and-engagement/
|       |   `-- safety-alerts/
|       |
|       `-- users-management/
|
|-- api/
|
|-- layout.jsx
|
`-- other frontend files
```

The dashboard pages are separated into different folders according to their functionality.

This makes the administrative features easier to maintain and organize.

---

## 5. Next.js Application

The administrative dashboard is implemented using **Next.js**.

Next.js provides the application structure, page routing, rendering, and frontend functionality required by the dashboard.

The dashboard uses the Next.js `app` directory to organize its pages.

For example:

```text
app/
|
`-- admin/
    |
    |-- auth/
    |   `-- login/
    |       `-- page.jsx
    |
    |-- users-management/
    |   `-- page.jsx
    |
    |-- content-management/
    |
    |-- account-settings/
    |
    `-- metrics/
```

Each `page.jsx` file represents a page or route within the dashboard.

---

## 6. Dashboard Layout

The dashboard uses a shared layout for the administrative area.

The layout is located in:

```text
app/
|
`-- admin/
    |
    `-- layout.jsx
```

The layout provides the common structure used by administrative pages.

```text
Admin Layout

      |

      |-- Navigation

      |-- Dashboard Content

      |-- Common UI Elements

      `-- Administrative Pages
```

Using a shared layout allows the different dashboard pages to maintain a consistent structure and styling.

---

## 7. Environment Configuration

The dashboard uses environment variables to configure the backend API connection.

The local development environment uses:

```text
.env.local
```

The project contains environment variables such as:

```text
NEXT_PUBLIC_API_URL="https://bloom-8db38d59208f.herokuapp.com"
```

This variable contains the URL of the Bloom backend API.

The dashboard uses this value when making API requests.

```text
Next.js Dashboard

       |

       | NEXT_PUBLIC_API_URL

       v

Bloom Backend API

       |

       v

PostgreSQL
```

Environment variables prevent the backend URL and other configuration values from being hard-coded throughout the application.

The `.env.local` file should not be committed if it contains sensitive or environment-specific configuration.

For Vercel deployment, the required environment variables should be configured in the Vercel project settings.

---

## 8. API Connection

The dashboard communicates with the Bloom backend through HTTP API requests.

The backend API URL is provided through the environment configuration.

For example:

```javascript
const API_URL = process.env.NEXT_PUBLIC_API_URL;
```

The dashboard can then use the API URL when sending requests to the backend.

Example:

```javascript
const response = await fetch(`${API_URL}/users`);
const data = await response.json();
```

The dashboard does not communicate directly with PostgreSQL.

```text
Admin Dashboard
       |
       | HTTP API Request
       v
Bloom Backend
       |
       | Database Operation
       v
PostgreSQL
```

---

## 9. Authentication

Administrator authentication is located under:

```text
admin/
|
`-- auth/
    |
    `-- login/
        |
        `-- page.jsx
```

The login page provides the entry point for administrators to authenticate.

```text
Administrator

       |

       |

    Login Page

       |

       | Authentication Request

       v

Bloom Backend

       |

       |

Authentication

       |

       v

Authenticated Administrator

       |

       v

Admin Dashboard
```

Only authenticated and authorized administrators should be able to access protected administrative functionality.

---

## 10. Account Settings

Administrator account settings are located under:

```text
admin/
|
`-- account-settings/
    |
    `-- page.jsx
```

This section provides functionality related to administrator account settings.

Account-related requests are handled through the dashboard and communicated to the Bloom backend API.

```text
Administrator

       |

       |

Account Settings

       |

       | API Request

       v

Bloom Backend

       |

       v

Administrator Account Data
```

---

## 11. User Management

User management is located under:

```text
admin/
|
`-- users-management/
    |
    `-- page.jsx
```

This section allows authorized administrators to manage users within the Bloom platform.

Administrators can perform user-management operations provided by the backend API.

```text
Administrator

       |

       |

Users Management

       |

       | API Request

       v

Bloom Backend

       |

       v

User Data
```

User management may include viewing and managing user accounts according to the permissions provided to the administrator.

---

## 12. Content Management

Content management is located under:

```text
admin/
|
`-- content-management/
```

This section provides administrators with functionality for managing platform content.

For example, administrators can manage maternal health tips and other content made available through the Bloom platform.

```text
Administrator

       |

       |

Content Management

       |

       | API Request

       v

Bloom Backend

       |

       v

Platform Content
```

Content changes are handled through the backend API rather than directly through the database.

---

## 13. Metrics

The dashboard contains a metrics section.

```text
admin/
|
`-- metrics/
    |
    |-- growth-and-engagement/
    |
    `-- safety-alerts/
```

The metrics section provides administrators with information used to monitor the Bloom platform.

The dashboard retrieves the relevant information through the Bloom backend API.

---

## 14. Growth and Engagement

The growth and engagement section is located under:

```text
admin/
|
`-- metrics/
    |
    `-- growth-and-engagement/
```

This section provides information related to platform growth and user engagement.

The dashboard communicates with the backend analytics functionality.

```text
Administrator

       |

       |

Growth and Engagement

       |

       | API Request

       v

Bloom Backend

       |

       |

Analytics Service

       |

       v

Analytics Data
```

The dashboard displays the information returned by the backend.

---

## 15. Safety Alerts

The safety alerts section is located under:

```text
admin/
|
`-- metrics/
    |
    `-- safety-alerts/
```

This section provides administrators with safety-related information available through the platform.

```text
Administrator

       |

       |

Safety Alerts

       |

       | API Request

       v

Bloom Backend

       |

       v

Safety-Related Data
```

The dashboard does not retrieve this information directly from PostgreSQL.

---

## 16. React and JSX Components

The dashboard uses React components written using JSX.

For example, a simple dashboard page can be structured as:

```jsx
export default function UsersManagement() {
  return (
    <div>
      <h1>Users Management</h1>
      <p>Manage Bloom users.</p>
    </div>
  );
}
```

React allows the dashboard interface to be divided into reusable components.

For example:

```text
Dashboard

   |

   |-- Navigation Component

   |-- Header Component

   |-- User Management Component

   |-- Content Management Component

   `-- Metrics Components
```

This helps keep the frontend organized and makes individual parts of the interface easier to maintain.

---

## 17. Fetching Data from the Backend

The dashboard retrieves data from the Bloom API using JavaScript.

A simplified example is:

```javascript
async function getUsers() {
  const response = await fetch(
    `${process.env.NEXT_PUBLIC_API_URL}/users`
  );

  return await response.json();
}
```

The returned data can then be displayed by a React component.

```text
Dashboard Page

       |

       | fetch()

       v

Bloom API

       |

       v

Backend Service

       |

       v

Database

       |

       v

API Response

       |

       v

React Component

       |

       v

Dashboard UI
```

---

## 18. Styling

The administrative dashboard uses CSS to style the interface.

Dashboard-specific CSS files are located alongside their related pages.

For example:

```text
admin/
|
|-- account-settings/
|   |-- page.jsx
|   `-- account.module.css
|
|-- auth/
|   `-- login/
|       |-- page.jsx
|       `-- login.module.css
|
|-- metrics/
|   `-- safety-alerts/
|       |-- page.jsx
|       `-- safety.module.css
|
`-- users-management/
    |-- page.jsx
    `-- users-management.css
```

CSS is used to control the visual appearance and layout of the dashboard.

This includes elements such as:

* Page layout
* Navigation
* Buttons
* Forms
* Tables
* Cards
* Metrics displays
* Spacing
* Typography
* Responsive layouts

Example:

```css
.dashboardTitle {
  font-size: 24px;
  font-weight: 600;
  margin-bottom: 20px;
}
```

The styling is separated from the application logic so that the appearance of the dashboard can be maintained independently.

---

## 19. Dashboard and Backend Communication

The general communication flow is:

```text
Administrative Dashboard

       |

       | API Request

       v

Bloom Backend

       |

       | Application Processing

       v

Backend Services

       |

       | Database Operations

       v

PostgreSQL

       |

       | API Response

       v

Administrative Dashboard
```

The backend is responsible for application logic, authentication, authorization, analytics, and database operations.

The dashboard is responsible for presenting the administrative interface and sending requests to the backend.

---

## 20. Database Access

The administrative dashboard does not communicate directly with PostgreSQL.

All database operations are performed by the Bloom backend.

```text
Admin Dashboard

       |

       |

Bloom API

       |

       |

Bloom Backend

       |

       |

PostgreSQL
```

This separation prevents the database from being directly exposed to the frontend application.

It also allows the backend to control authentication, authorization, validation, business logic, and database operations.

---

## 21. Dashboard Security

The administrative dashboard is protected through the security mechanisms implemented by the Bloom backend.

Administrative access uses authentication and role-based authorization.

```text
Administrator

       |

       v

Login

       |

       v

Authentication

       |

       v

Authorization

       |

       v

Admin Dashboard

       |

       v

Protected API Endpoints
```

The backend verifies that the authenticated user has the required administrator role before allowing access to protected administrative functionality.

This helps prevent ordinary users from accessing administrator functionality.

---

## 22. Dashboard Areas and Backend Functionality

The relationship between dashboard sections and backend functionality can be summarized as follows:

| Dashboard Area        | Related Functionality                 |
| --------------------- | ------------------------------------- |
| Authentication        | Administrator authentication          |
| Account Settings      | Administrator account functionality   |
| User Management       | User-related operations               |
| Content Management    | Platform content operations           |
| Growth and Engagement | Analytics and engagement information  |
| Safety Alerts         | Safety-related information and alerts |

The dashboard acts as the administrative interface, while the Bloom backend provides the API and application services behind these features.

---

## 23. Local Development

During development, the Next.js dashboard can be run locally.

The project uses the environment configuration to connect the local dashboard to the Bloom backend API.

```text
Local Next.js Dashboard

       |

       | API URL from .env.local

       v

Bloom Backend API

       |

       v

PostgreSQL
```

The environment configuration contains values such as:

```text
NEXT_PUBLIC_API_URL="https://bloom-8db38d59208f.herokuapp.com"
```

The local development environment allows the dashboard to be tested before deployment to Vercel.

---

## 24. Vercel Deployment

The administrative dashboard is deployed using Vercel.

The general deployment process is:

```text
Next.js Source Code

       |

       v

Git Repository

       |

       v

Vercel

       |

       | Build

       v

Next.js Production Application

       |

       v

Hosted Dashboard
```

During deployment, Vercel builds the Next.js application and hosts the resulting production application.

The required environment variables should be configured in the Vercel project settings.

For example:

```text
NEXT_PUBLIC_API_URL
```

should point to the deployed Bloom backend API.

---

## 25. Hosted Dashboard

The production Bloom administrative dashboard is hosted on Vercel.

The production URL should be documented here:

```text
Bloom Administrative Dashboard:

[ADD YOUR VERCEL HOSTED DASHBOARD LINK HERE]
```

For example:

```text
https://bloom-dashboard.vercel.app
```

The exact URL should be replaced with the actual Vercel deployment URL.

The hosted dashboard communicates with the deployed Bloom backend through the configured API URL.

```text
Administrator

       |

       |

Vercel Hosted Dashboard

       |

       | HTTPS API Requests

       v

Bloom Backend API

       |

       | Database Operations

       v

PostgreSQL
```

---

## 26. Deployment and Configuration Summary

The Bloom administrative dashboard uses Next.js and React for the frontend application.

The dashboard is connected to the Bloom backend through the API using the configured environment variables.

The production application is deployed and hosted using Vercel.

```text
Next.js / React

       |

       | Environment Configuration

       v

Vercel

       |

       | HTTPS

       v

Bloom Backend API

       |

       v

PostgreSQL
```

This architecture keeps the frontend, backend, and database separated while allowing the dashboard to securely communicate with the Bloom platform services.

---
