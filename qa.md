# Testing

## 1. Overview

Testing is used to verify that the different parts of Bloom work as expected.

Testing covers the backend API, mobile application, administrative dashboard, and the integration between these components.

---

## 2. Backend Testing

Backend tests are organized separately from the application code.

The main areas to test include:

- API endpoints
- Authentication
- User management
- Maternal profiles
- Symptoms and symptom logs
- Care schedules
- Maternal health tips
- Location functionality
- Analytics

Backend tests should also verify that API requests return the expected responses and handle invalid input correctly.

---

## 3. Mobile Testing

The Flutter application contains tests under:

```text
test/
|
|-- unit/
|-- widget/
\-- integration/
```

### Unit Tests

Used to test individual pieces of application logic.

### Widget Tests

Used to test individual Flutter widgets and user interface behaviour.

### Integration Tests

Used to test functionality involving multiple parts of the mobile application.

---

## 4. Dashboard Testing

Dashboard functionality should be tested across its main areas:

```text
admin/
|
|-- account-settings/
|-- auth/
|   \-- login/
|-- content-management/
|-- metrics/
|   |-- growth-and-engagement/
|   \-- safety-and-alerts/
\-- users-management/
```

Testing should cover authentication, user management, content management, metrics, safety alerts, and account settings.

---

## 5. API Integration Testing

Integration testing verifies communication between the client applications and the backend.

```text
Mobile / Dashboard
       |
       | API request
       |
Bloom Backend
       |
       | Database operation
       |
PostgreSQL
```

These tests help verify that requests, responses, authentication, and stored data work correctly across the connected components.

---

## 6. QA Testing

The project also contains a dedicated QA area for organizing broader test cases and regression testing.

```text
qa/
|
|-- test-cases/
|-- api/
|-- mobile/
|-- dashboard/
|-- integration/
\-- regression/
```

The QA structure allows testing to be organized by feature and platform.

---

## 7. Regression Testing

Regression testing is performed after changes to make sure existing functionality continues to work.

The regression checklist is maintained under:

```text
qa/
|
\-- regression/
    |
    \-- regression-checklist.md
```

---

## 8. Before Submitting Changes

Before creating a pull request:

- Run the relevant tests.
- Check the affected application manually where necessary.
- Verify API integrations if the change involves the backend.
- Check that existing functionality has not been broken.
- Include relevant testing information in the pull request.

---
