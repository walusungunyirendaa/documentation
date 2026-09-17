
## 1. Overview

The Bloom backend is the central application layer that connects the Bloom client applications to the database and provides the API used by the platform.

The backend is responsible for:

- Exposing REST API endpoints.
- Receiving requests from the mobile application and administrative dashboard.
- Validating incoming request data.
- Applying application and business logic.
- Authenticating and authorizing users.
- Managing user roles and permissions.
- Creating, reading, updating, and deleting application data.
- Communicating with the PostgreSQL database.
- Managing maternal profiles and pregnancy information.
- Managing symptoms and symptom logs.
- Managing care schedules and reminders.
- Providing maternal health information.
- Providing location-related functionality.
- Providing analytics functionality.
- Handling integrations and background operations where implemented.
- Returning structured API responses to client applications.

The backend acts as the single access point between the client applications and PostgreSQL.

```text
Bloom Mobile Application
        |
        | HTTP / REST API requests
        |
        v
   Bloom Backend
        |
        | SQLAlchemy
        |
        v
   PostgreSQL Database
````

The administrative dashboard follows the same architecture:

```text
Administrative Dashboard
        |
        | HTTP / REST API requests
        |
        v
   Bloom Backend
        |
        | SQLAlchemy
        |
        v
   PostgreSQL Database
```

Client applications do not connect directly to PostgreSQL.

---

## 2. Technology Stack

The backend is built using Python and a set of Python libraries and frameworks that provide the API, database access, validation, authentication, and supporting functionality.

### Main Technologies

| Technology     | Purpose                                                      |
| -------------- | ------------------------------------------------------------ |
| **Python**     | Primary backend programming language                         |
| **FastAPI**    | Web framework used to create the REST API                    |
| **Pydantic**   | Request and response data validation                         |
| **SQLAlchemy** | Object-relational mapper used to communicate with PostgreSQL |
| **PostgreSQL** | Primary relational database                                  |
| **UUID**       | Identifier type used for database records                    |
| **Postman**    | API testing and regression testing                           |
| **Swagger UI** | Interactive API documentation provided by FastAPI            |

The backend is therefore structured around the following flow:

```text
Client Application
       |
       v
    FastAPI
       |
       v
    Router
       |
       v
    Service
       |
       v
   SQLAlchemy
       |
       v
 PostgreSQL
```

---

## 3. Python Configuration

Python is the primary programming language used to implement the Bloom backend.

Python is used for:

* API endpoints.
* Application logic.
* Database models.
* Services.
* Authentication.
* Validation.
* Utility functions.
* Analytics processing.
* Integrations.

### Python Installation

Python should be installed on the development machine before setting up the backend.

Verify the installation:

```bash
python --version
```

or:

```bash
python3 --version
```

A virtual environment should be used to isolate backend dependencies from other Python projects.

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Linux/macOS:

```bash
source venv/bin/activate
```

On Windows:

```bash
venv\Scripts\activate
```

After activation, install the backend dependencies:

```bash
pip install -r requirements.txt
```

---

## 4. FastAPI

FastAPI is the web framework used to expose the Bloom backend as an HTTP API.

FastAPI handles:

* Routing.
* HTTP requests.
* HTTP responses.
* Request validation.
* Dependency injection.
* API documentation.
* Error responses.
* Integration with Pydantic schemas.

The main application entry point is:

```text
main.py
```

The application starts FastAPI and registers the backend routers.

A simplified structure is:

```text
Client
   |
   v
HTTP Request
   |
   v
FastAPI
   |
   v
Router
   |
   v
Service
   |
   v
Database
```

### Running FastAPI Locally

The FastAPI development server can be started using Uvicorn.

A typical command is:

```bash
uvicorn main:app --reload
```

The `--reload` option automatically reloads the development server when source files change.

Once the server is running, FastAPI provides interactive API documentation through Swagger UI.

```text
http://localhost:8000/docs
```

FastAPI also provides an alternative OpenAPI interface:

```text
http://localhost:8000/redoc
```

The actual host and port should follow the project's environment configuration.

---

## 5. API Architecture

The backend follows a layered architecture.

The major layers are:

```text
Client Application
        |
        v
     Router
        |
        v
     Schema
        |
        v
     Service
        |
        v
   Repository / Data Access
        |
        v
    SQLAlchemy
        |
        v
    PostgreSQL
```

### Router Layer

Routers define the API endpoints.

They are responsible for:

* Receiving HTTP requests.
* Selecting the appropriate endpoint.
* Reading path and query parameters.
* Calling the appropriate service.
* Returning API responses.

Examples of router areas in the backend include:

```text
routers/
├── users
├── locations
├── maternal profiles
├── symptoms
├── symptom logs
├── care schedules
├── maternal health tips
└── analytics
```

### Service Layer

The service layer contains application and business logic.

A router should not contain all of the application's business logic.

Instead:

```text
API Request
     |
     v
  Router
     |
     v
  Service
     |
     v
 Database
```

Services are responsible for processing the request and applying the rules required by the application.

### Database Layer

The database layer manages communication with PostgreSQL.

SQLAlchemy models represent database tables as Python classes.

---

## 6. API Communication

The Bloom clients communicate with the backend using HTTP requests.

The backend exposes REST-style API resources.

A request generally contains:

```text
HTTP Method
Endpoint
Headers
Authentication information
Request body
```

The backend processes the request and returns a structured response.

For example:

```text
Mobile Application
       |
       | POST /...
       | JSON body
       |
       v
     FastAPI
       |
       v
     Router
       |
       v
     Service
       |
       v
   PostgreSQL
       |
       v
   JSON Response
```

The exact endpoint paths are defined by the registered FastAPI routers.

---

## 7. API HTTP Methods

The backend can use standard HTTP methods depending on the operation exposed by each router.

| Method   | General Purpose              |
| -------- | ---------------------------- |
| `GET`    | Retrieve information         |
| `POST`   | Create a new resource        |
| `PUT`    | Replace or update a resource |
| `PATCH`  | Partially update a resource  |
| `DELETE` | Delete a resource            |

For example, a resource may follow this pattern:

```text
GET     /resource
GET     /resource/{id}
POST    /resource
PUT     /resource/{id}
DELETE  /resource/{id}
```

The exact routes available in Bloom should be taken from the FastAPI router definitions and Swagger documentation.

---

## 8. API Endpoint Groups

The backend provides functionality around the following application areas.

### User API

Responsible for operations related to platform users.

User functionality includes:

* User creation.
* User retrieval.
* User updates.
* User status.
* User roles.
* Authentication-related information.
* User location association.

The user model is defined in:

```text
models/user.py
```

The corresponding API functionality is handled through the user router and service.

---

### Location API

The location functionality manages geographic information associated with users and other platform functionality.

The location model is:

```text
models/location.py
```

Location information includes:

* Location identifier.
* Location name.
* Latitude.
* Longitude.
* Creation timestamp.

The backend also contains distance calculation functionality through:

```text
distance.py
```

---

### Maternal Profile API

The maternal profile API manages information associated with a mother.

The model is:

```text
models/maternal_profile.py
```

It stores information such as:

* User association.
* CHP code.
* Caregiver information.
* Caregiver phone number.
* Caregiver device token.
* Last menstrual period.
* Expected due date.
* Delivery date.
* Pregnancy status.
* Caregiver sharing code.
* Sharing-code expiration.
* Caregiver waiting status.
* Profile linking information.

---

### Symptom API

The symptom API manages the predefined maternal conditions and their descriptions.

The model is:

```text
models/symptom.py
```

Symptoms are associated with supported maternal conditions.

The current model defines conditions including:

```text
postpartum hemorrhage
pre-eclampsia/eclampsia
sepsis
```

Each symptom contains:

* A UUID identifier.
* A condition name.
* A symptom description.

---

### Symptom Log API

The symptom log functionality records symptoms associated with a maternal profile.

The model is:

```text
models/symptom_log_item.py
```

A symptom log contains information such as:

* Logged symptoms.
* Maternal profile.
* Log date.
* Duration.
* Severity.
* Risk status.
* Trigger time.

The system supports alert states including:

```text
Severity:
- Low
- Medium
- Critical
```

Risk statuses include:

```text
- Triggered
- CHP called
- Resolved
```

---

### Care Schedule API

Care schedules are represented by:

```text
models/care_schedule.py
```

The care schedule functionality supports reminders related to maternal care.

A schedule contains:

* Schedule identifier.
* Maternal profile.
* Reminder type.
* Scheduled times.
* Frequency.
* Status.

Reminder types currently represented by the model include:

```text
Medication
Anti-natal Care Visit
```

Supported frequencies include:

```text
Daily
Weekly
Monthly
```

Supported statuses include:

```text
Scheduled
sent
Completed
```

The scheduled time is represented as an array of datetime values.

---

### Maternal Health Tips API

Maternal health information is represented by:

```text
models/maternal_tip.py
```

A maternal health tip contains:

* Tip identifier.
* Title.
* Content.
* Pregnancy week.
* Creation timestamp.

Pregnancy week is indexed to support efficient retrieval based on pregnancy stage.

---

### Analytics API

Analytics functionality is handled by the backend.

The backend contains analytics functionality under:

```text
routers/
    analytics.py

services/
    analytics_service.py
```

The dashboard communicates with the backend API to retrieve analytics rather than accessing PostgreSQL directly.

---

## 9. Request and Response Validation

FastAPI works with Pydantic schemas to validate incoming and outgoing API data.

Validation ensures that API requests contain the expected:

* Fields.
* Data types.
* Required values.
* Optional values.
* Formats.

A simplified request flow is:

```text
HTTP Request
      |
      v
FastAPI
      |
      v
Pydantic Validation
      |
      v
Router
      |
      v
Service
      |
      v
Database
```

Invalid requests should be rejected before invalid data reaches the database layer.

FastAPI can return validation errors using HTTP `422`.

---

## 10. PostgreSQL Database

PostgreSQL is the primary relational database used by Bloom.

The database stores information required by:

* The mobile application.
* The administrative dashboard.
* Backend services.

Client applications do not connect directly to PostgreSQL.

All database operations pass through the backend.

```text
Mobile Application
        |
        v
     Bloom API
        |
        v
     Backend
        |
        v
   PostgreSQL
```

---

## 11. SQLAlchemy

SQLAlchemy is the Object-Relational Mapper (ORM) used by the backend.

Instead of writing SQL queries for every database operation, SQLAlchemy allows database tables to be represented as Python classes.

For example:

```python
class User(Base):
    __tablename__ = "users"
```

The class represents the `users` database table.

SQLAlchemy provides:

* Table mapping.
* Column definitions.
* Relationships.
* Foreign keys.
* Database queries.
* Transactions.
* Database sessions.

The models inherit from the project's SQLAlchemy `Base`:

```python
from database import Base
```

---

## 12. SQLAlchemy Data Types

The backend uses SQLAlchemy data types to define the structure of PostgreSQL columns.

### UUID

UUIDs are used as primary identifiers for many entities.

Example:

```python
user_id = Column(
    UUID(as_uuid=True),
    primary_key=True,
    default=uuid4
)
```

UUIDs provide unique identifiers without relying on sequential integer IDs.

---

### String

Strings are used for text fields with defined maximum lengths.

Example:

```python
first_name = Column(String(100), nullable=False)
```

Examples of fields using strings include:

* First name.
* Last name.
* Email.
* Phone number.
* Location name.
* CHP code.

---

### Text

`Text` is used for longer text content.

The maternal health tip model uses:

```python
content = Column(Text, nullable=False)
```

This allows longer health information to be stored than a short fixed-length string field.

---

### Integer

Integers are used for whole-number values.

For example:

```python
pregnancy_week = Column(Integer, nullable=False)
```

The symptom log also uses an integer for duration.

---

### Float

Floating-point numbers are used for geographic coordinates.

The location model uses:

```python
latitude = Column(Float, nullable=False)
longitude = Column(Float, nullable=False)
```

---

### Boolean

Boolean fields represent true/false states.

For example:

```python
caregiver_waiting = Column(Boolean, default=False, nullable=False)
```

Another example is:

```python
is_deleted = Column(
    Boolean,
    nullable=False,
    default=False,
    server_default="false"
)
```

---

### Date

`Date` is used when only a calendar date is required.

Maternal profiles use dates for:

```text
lmp_date
due_date
delivery_date
```

---

### DateTime

`DateTime` is used when both date and time are required.

Examples include:

```text
created_at
scheduled_time
log_date
triggered_at
linked_at
unlinked_at
share_code_expires_at
```

---

### Enum

Enums restrict a database field to a predefined set of values.

For example, the user role is represented using:

```python
class UserRole(str, PyEnum):
    ADMIN = "admin"
    CHP = "chp"
    MOTHER = "mother"
```

The database column then uses:

```python
role = Column(
    Enum(UserRole, name="user_role_enum", create_type=True),
    nullable=False
)
```

This prevents arbitrary role values from being stored.

---

### ARRAY

PostgreSQL array types are supported through SQLAlchemy.

The care schedule uses:

```python
scheduled_time = Column(
    ARRAY(DateTime),
    nullable=False
)
```

The symptom log uses:

```python
symptoms_logged = Column(
    ARRAY(UUID(as_uuid=True)),
    nullable=False,
    default=list
)
```

This allows multiple datetime values or multiple symptom UUIDs to be stored in a single field.

---

## 13. Database Relationships

SQLAlchemy relationships and foreign keys connect related entities.

For example, a maternal profile references a user:

```python
user_id = Column(
    UUID(as_uuid=True),
    ForeignKey(
        "users.user_id",
        ondelete="CASCADE"
    ),
    nullable=False,
    unique=True,
    index=True
)
```

This creates a relationship between:

```text
User
 |
 | user_id
 v
Maternal Profile
```

A symptom log item references a maternal profile:

```text
Maternal Profile
       |
       | profile_id
       v
Symptom Log Item
```

A care schedule also references the maternal profile:

```text
Maternal Profile
       |
       | profile_id
       v
Care Schedule
```

Locations are associated with users:

```text
Location
    |
    | location_id
    v
User
```

---

## 14. Cascade and Referential Integrity

Foreign keys are used to maintain relationships between database records.

Some relationships use:

```python
ondelete="CASCADE"
```

For example, the maternal profile references the user with cascade deletion.

This means that when the parent record is deleted, dependent records can also be removed according to the database relationship.

The user location relationship uses:

```python
ondelete="RESTRICT"
```

This prevents deletion of a referenced location when dependent user records still exist.

These rules help maintain database integrity.

---

## 15. Database Models

The main models currently documented for the Bloom backend are:

```text
models/
├── user.py
├── location.py
├── maternal_profile.py
├── symptom.py
├── symptom_log_item.py
├── care_schedule.py
└── maternal_tip.py
```

Each model represents a database entity.

### User

Table:

```text
users
```

Main fields include:

```text
user_id
location_id
first_name
last_name
role
chp_code
device_token
phone_number
email
hashed_password
user_status
created_at
is_deleted
```

---

### Location

Table:

```text
locations
```

Main fields:

```text
location_id
location_name
latitude
longitude
created_at
```

---

### Maternal Profile

Table:

```text
maternal_profiles
```

Main fields:

```text
profile_id
user_id
chp_code
caregiver_name
caregiver_phone
caregiver_device_token
lmp_date
due_date
delivery_date
status
share_code
share_code_expires_at
caregiver_waiting
linked_at
unlinked_at
```

---

### Symptom

Table:

```text
symptoms
```

Main fields:

```text
symptom_id
condition_name
symptom_description
```

---

### Symptom Log Item

Table:

```text
symptom_log_items
```

Main fields:

```text
log_item_id
symptoms_logged
profile_id
log_date
duration
severity
risk_status
triggered_at
```

---

### Care Schedule

Table:

```text
care_schedules
```

Main fields:

```text
care_schedule_id
profile_id
type
scheduled_time
frequency
status
```

---

### Maternal Health Tip

Table:

```text
maternal_health_tips
```

Main fields:

```text
tip_id
title
content
pregnancy_week
created_at
```

---

## 16. Authentication and User Roles

The backend supports different user roles.

The current user role enum contains:

```text
admin
chp
mother
```

The role is stored in the `users` table.

```python
class UserRole(str, PyEnum):
    ADMIN = "admin"
    CHP = "chp"
    MOTHER = "mother"
```

Roles allow the backend to determine what functionality a particular user can access.

Authentication and authorization are handled by the backend rather than by the client applications alone.

The client provides authentication information with API requests, and the backend verifies the request before allowing protected operations.

---

## 17. User Account Status

Users also have an account status.

The supported values are:

```text
Active
Inactive
```

The model defines:

```python
user_status = Column(
    Enum(
        "Active",
        "Inactive",
        name="user_status_enum"
    ),
    nullable=False,
    default="Active"
)
```

The model also contains:

```python
is_deleted = Column(
    Boolean,
    nullable=False,
    default=False,
    server_default="false"
)
```

This allows the application to distinguish between active records and records that have been marked as deleted.

---

## 18. Maternal Profile Status

Maternal profiles contain a pregnancy status.

The model currently defines:

```text
Pregnant
Postpartum
Pending Chart Initiation
```

The status is stored using a PostgreSQL enum.

This allows the application to determine the current state of a maternal profile.

---

## 19. Symptom Risk and Alert States

Symptom log records contain severity and risk status.

Severity values are:

```text
Low
Medium
Critical
```

Risk status values are:

```text
Triggered
CHP called
Resolved
```

This allows the backend to track the lifecycle of a symptom-related alert.

The general process can be represented as:

```text
Symptom Recorded
       |
       v
Risk Evaluated
       |
       v
Alert Triggered
       |
       v
CHP Called
       |
       v
Resolved
```

The exact transition rules are implemented by the application services.

---

## 20. Care Schedule and Reminders

Care schedules allow the backend to store scheduled maternal-care activities.

The supported reminder types include:

```text
Medication
Anti-natal Care Visit
```

The supported frequencies include:

```text
Daily
Weekly
Monthly
```

The reminder lifecycle includes:

```text
Scheduled
sent
Completed
```

A schedule can contain multiple scheduled datetime values because `scheduled_time` is represented as a PostgreSQL array of `DateTime` values.

---

## 21. Environment Configuration

Backend configuration should be stored through environment variables rather than hard-coded credentials.

The backend provides an example configuration file:

```text
.env.example
```

Developers should create the appropriate local environment file based on the example.

Sensitive values should not be committed to Git.

Typical configuration areas may include:

```text
Database connection
Application configuration
Authentication configuration
External service configuration
```

The exact environment variables used by the current backend should be taken from `.env.example` and the backend configuration module.

---

## 22. Database Configuration

Database functionality is provided through:

```text
database.py
```

The application imports the SQLAlchemy `Base` from the database module:

```python
from database import Base
```

Models then inherit from this base:

```python
class User(Base):
```

This connects the model definitions to the SQLAlchemy database configuration.

The general relationship is:

```text
database.py
     |
     v
SQLAlchemy Base
     |
     v
Models
     |
     v
Database Session
     |
     v
PostgreSQL
```

---

## 23. API Documentation

FastAPI automatically generates API documentation from the registered routes, request schemas, response schemas, and endpoint definitions.

The main interactive documentation interface is Swagger UI.

```text
/docs
```

The alternative documentation interface is:

```text
/redoc
```

Swagger UI can be used to:

* View available endpoints.
* View HTTP methods.
* Inspect request parameters.
* Inspect request bodies.
* Inspect response schemas.
* Test API requests.
* Verify validation behaviour.
* Test authenticated endpoints where authentication is configured.

The Swagger documentation should be treated as the authoritative list of currently registered API endpoints.

---

## 24. API Testing

The backend API is tested using Postman and FastAPI's Swagger UI.

### Postman

Postman is used for:

* API request testing.
* CRUD testing.
* Authentication testing.
* Validation testing.
* Error response testing.
* Regression testing.

A typical test flow is:

```text
Postman
   |
   v
Bloom API
   |
   v
Router
   |
   v
Service
   |
   v
Database
```

### Swagger UI

Swagger UI is useful during development because it allows developers to test API endpoints directly from the generated API documentation.

---

## 25. API Error Handling

The API should return appropriate HTTP status codes based on the result of a request.

Common status codes include:

| Status Code | Meaning                                 |
| ----------- | --------------------------------------- |
| `200`       | Request completed successfully          |
| `201`       | Resource successfully created           |
| `204`       | Request completed with no response body |
| `400`       | Invalid request                         |
| `401`       | Authentication required or failed       |
| `403`       | Request is not authorized               |
| `404`       | Requested resource was not found        |
| `422`       | Request validation failed               |
| `500`       | Unexpected server-side error            |

FastAPI handles validation errors and allows application code to return appropriate HTTP exceptions.

---

## 26. API Data Flow

A typical request follows this architecture:

```text
Client
  |
  | HTTP Request
  v
FastAPI
  |
  v
Router
  |
  v
Pydantic Validation
  |
  v
Service Layer
  |
  v
SQLAlchemy
  |
  v
PostgreSQL
  |
  v
SQLAlchemy
  |
  v
Service Layer
  |
  v
API Response
  |
  v
Client
```

This separation makes it possible to keep:

* HTTP handling in routers.
* Validation in schemas.
* Business logic in services.
* Database mapping in models.
* Database communication in the database layer.

---

## 27. Backend Project Structure

The backend follows a modular structure.

A typical structure is:

```text
backend/
│
├── main.py
├── database.py
├── requirements.txt
├── .env.example
│
├── routers/
│   ├── users
│   ├── locations
│   ├── maternal_profiles
│   ├── symptoms
│   ├── symptom_log_items
│   ├── care_schedules
│   ├── maternal_tips
│   └── analytics.py
│
├── services/
│   ├── user_service
│   ├── location_service
│   ├── maternal_profile_service
│   ├── symptom_service
│   ├── symptom_log_item_service
│   ├── care_schedule_service
│   ├── maternal_tip_service
│   └── analytics_service.py
│
├── models/
│   ├── user.py
│   ├── location.py
│   ├── maternal_profile.py
│   ├── symptom.py
│   ├── symptom_log_item.py
│   ├── care_schedule.py
│   └── maternal_tip.py
│
└── utils/
    └── distance.py
```

The exact filenames and directories should follow the current repository structure.

---

## 28. Backend and Client Separation

The Bloom architecture separates client applications from backend and database operations.

```text
                 ┌─────────────────────┐
                 │   Mobile Application│
                 └──────────┬──────────┘
                            |
                            |
                       HTTP API
                            |
                            v
                 ┌─────────────────────┐
                 │    Bloom Backend    │
                 │      FastAPI        │
                 └──────────┬──────────┘
                            |
                       SQLAlchemy
                            |
                            v
                 ┌─────────────────────┐
                 │     PostgreSQL      │
                 └─────────────────────┘

                 ┌─────────────────────┐
                 │ Administrative      │
                 │ Dashboard            │
                 └──────────┬──────────┘
                            |
                       HTTP API
                            |
                            v
                       Bloom Backend
```

Neither the mobile application nor the dashboard needs direct database credentials.

---

## 29. Backend Deployment

The backend is deployed separately from the mobile application, dashboard, and informational website.

The backend deployment environment must provide:

* Python runtime.
* Backend dependencies.
* Environment variables.
* Database connectivity.
* API server process.

### Heroku Deployment

The Bloom backend is deployed using **Heroku**.

The deployment process requires the backend application and its dependencies to be available to the Heroku environment.

The backend dependency file is:

```text
requirements.txt
```

Dependencies can be installed locally with:

```bash
pip install -r requirements.txt
```

The backend also requires its environment configuration to be available in the deployment environment.

Sensitive configuration values should be stored as Heroku environment/configuration variables rather than committed to the repository.

---

## 30. Local Backend Setup

A developer setting up the backend locally should follow these general steps.

### Step 1 — Clone the repository

```bash
git clone <repository-url>
```

Enter the backend directory:

```bash
cd backend
```

### Step 2 — Create a virtual environment

```bash
python -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

### Step 3 — Install dependencies

```bash
pip install -r requirements.txt
```

### Step 4 — Configure environment variables

Create the environment file using the project's example configuration:

```text
.env.example
```

### Step 5 — Configure PostgreSQL

Ensure PostgreSQL is available and the required database configuration is provided to the backend.

### Step 6 — Start FastAPI

```bash
uvicorn main:app --reload
```

### Step 7 — Open API documentation

Open:

```text
http://localhost:8000/docs
```

The Swagger interface can then be used to inspect and test the registered endpoints.

---

## 31. Database Development Workflow

When working with database functionality, developers should follow the application architecture instead of accessing PostgreSQL directly from the client applications.

The workflow is:

```text
Define / update model
        |
        v
Database schema
        |
        v
Service logic
        |
        v
Router
        |
        v
API endpoint
        |
        v
Client application
```

Changes to database models should be handled carefully because they affect the PostgreSQL schema and any API functionality that depends on the model.

---

## 32. API Endpoint Reference

The backend endpoint reference should be generated from the registered FastAPI routers.

The main endpoint groups correspond to:

```text
Users
Locations
Maternal Profiles
Symptoms
Symptom Logs
Care Schedules
Maternal Health Tips
Analytics
```

For the exact:

* HTTP method.
* URL path.
* Path parameters.
* Query parameters.
* Request body.
* Authentication requirement.
* Response schema.
* Status codes.

developers should use the current Swagger documentation:

```text
/docs
```

This prevents the technical documentation from becoming inconsistent with the actual registered API routes.

---

## 33. Development Practices

Backend development should follow a separation of responsibilities.

### Routers

Routers handle API communication.

```text
Request
  |
  v
Router
```

### Services

Services handle business logic.

```text
Router
  |
  v
Service
```

### Models

Models represent database entities.

```text
Service
  |
  v
Model
```

### Database

The database layer handles database connectivity.

```text
Model
  |
  v
SQLAlchemy
  |
  v
PostgreSQL
```

This separation makes the application easier to maintain and test.

---

## 34. Security Considerations

The backend is responsible for protecting application data and controlling access to protected resources.

Important security responsibilities include:

* Authentication.
* Authorization.
* User role enforcement.
* Password protection.
* Database access control.
* Environment variable protection.
* Input validation.
* API error handling.
* Protection of sensitive user information.

Passwords should not be stored as plain text.

The user model stores:

```text
hashed_password
```

rather than a plaintext password.

Sensitive environment values should also never be committed to the source repository.

---

## 35. Backend Testing Checklist

Before considering a backend change complete, verify:

* API endpoint responds correctly.
* Request validation works.
* Required fields are enforced.
* Invalid data is rejected.
* Authentication is enforced where required.
* Authorization rules are respected.
* Database records are created correctly.
* Database relationships remain valid.
* Updates modify the expected records.
* Deletes follow the configured foreign-key rules.
* Correct HTTP status codes are returned.
* API responses match the expected schema.
* Swagger documentation reflects the endpoint.
* Postman tests pass.

---

## 36. Troubleshooting

### FastAPI does not start

Check:

```bash
python --version
```

Then verify dependencies:

```bash
pip install -r requirements.txt
```

Also verify that the FastAPI application entry point is correct.

---

### Database connection fails

Check:

* PostgreSQL is running.
* Database credentials are configured.
* Environment variables are loaded.
* Database name is correct.
* Host and port are correct.
* The backend has access to the database.

---

### API validation error

Check the request against the schema shown in Swagger UI.

A `422` response generally indicates that the request data does not satisfy the expected validation rules.

---

### Endpoint not visible in Swagger

Check that:

* The router exists.
* The router is imported.
* The router is registered with the FastAPI application.
* The endpoint is defined correctly.

---

## 37. Related Documentation

* [Architecture](architecture.md)
* [Database](database.md)
* [Security](security.md)
* [Testing and QA](qa.md)



---
