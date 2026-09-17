# Mobile Application

## 1. Overview

The Bloom mobile application is the main client application for mothers, caregivers, and Community Health Promoters (CHPs).

The application is built using **Flutter**, which allows Bloom to develop the mobile interface using a single codebase for supported mobile platforms.

The mobile application communicates with the Bloom backend through HTTP API requests. It does not connect directly to the PostgreSQL database.

```text
Mother / Caregiver / CHP
          |
          |
    Bloom Mobile
          |
          | HTTP API requests
          |
    Bloom Backend
          |
          | Database operations
          |
      PostgreSQL
```

The Flutter application is responsible mainly for the **user interface, user interaction, local application state, API communication, and presentation of data returned by the backend**.

---

## 2. Technologies Used

The Bloom mobile application uses the following main technologies:

| Technology    | Purpose                                                |
| ------------- | ------------------------------------------------------ |
| Flutter       | Mobile application framework                           |
| Dart          | Programming language used by Flutter                   |
| HTTP/REST API | Communication with the Bloom backend                   |
| Provider      | Application state management                           |
| Android       | Android application platform                           |
| iOS           | iOS application platform                               |
| Appetize.io   | Browser-based mobile application demonstration/testing |

Flutter uses **Dart** to build screens, widgets, services, models, and application logic.

For example, a simple Flutter widget can be written as:

```dart
import 'package:flutter/material.dart';

class WelcomeScreen extends StatelessWidget {
  const WelcomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Bloom'),
      ),
      body: const Center(
        child: Text('Welcome to Bloom'),
      ),
    );
  }
}
```

This creates a Flutter screen containing an application bar and a welcome message.

---

## 3. User Flow

The Bloom mobile application follows different user flows depending on the user's role and the features they access.

The main flow generally follows:

```text
Open Application
       |
       v
Authentication
       |
       v
User Verification
       |
       v
Role Identification
       |
       v
Role-Specific Home Screen
       |
       v
Bloom Features
```

The user flow covers the main steps users take when interacting with the application, from authentication and profile setup to accessing maternal health features and services.

[View Bloom Mobile User Flow](https://www.figma.com/design/xOG6fkIbWP1ZtLjHvgaTqJ/SpyHIve-User-Flows?node-id=0-1&p=f&t=YI9sriyGLWtHGNX0-0)

---

## 4. User Roles

The mobile application supports three main user roles:

```text
Bloom Mobile
     |
     |-- Mother
     |
     |-- Caregiver
     |
     `-- Community Health Promoter (CHP)
```

Each role has functionality relevant to its responsibilities within the Bloom platform.

The administrator role is managed through the separate administrative dashboard.

---

## 5. Mobile Application Structure

The Flutter application is organized under the `mobile` directory.

The main application code is located in `lib`.

```text
mobile/
|
|-- lib/
|   |
|   |-- main.dart
|   |
|   |-- models/
|   |
|   |-- services/
|   |   |
|   |   |-- api/
|   |   |
|   |   |-- authentication/
|   |   |
|   |   `-- notifications/
|   |
|   |-- screens/
|   |   |
|   |   |-- auth_screens/
|   |   |
|   |   |-- mothers_screens/
|   |   |
|   |   |-- caregiver_screens/
|   |   |
|   |   `-- chp_screens/
|   |
|   |-- widgets/
|   |
|   |-- providers/
|   |
|   |-- constants/
|   |
|   `-- utils/
|
|-- assets/
|   |
|   |-- images/
|   |-- icons/
|   `-- fonts/
|
|-- test/
|   |
|   |-- unit/
|   |-- widget/
|   `-- integration/
|
|-- android/
|-- ios/
|
|-- pubspec.yaml
`-- .env.example
```

The application separates screens, services, models, reusable widgets, providers, constants, and utility functionality.

---

## 6. Main Application Entry Point

The main application entry point is:

```text
lib/
|
`-- main.dart
```

`main.dart` starts the Flutter application and provides the entry point from which the application is initialized.

A simplified Flutter entry point looks like:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const BloomApp());
}

class BloomApp extends StatelessWidget {
  const BloomApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Bloom',
      home: const WelcomeScreen(),
    );
  }
}
```

The actual application can initialize additional services, providers, configuration, and application settings before displaying the main interface.

---

## 7. Models

The `models` directory contains the data models used by the mobile application.

```text
lib/
|
`-- models/
```

Models provide a representation of the data used by the application when communicating with the backend and displaying information within the mobile interface.

For example, a model can represent information returned by the backend:

```dart
class UserModel {
  final int id;
  final String email;
  final String role;

  UserModel({
    required this.id,
    required this.email,
    required this.role,
  });
}
```

Models help keep application data structured and make it easier for screens and services to work with API responses.

---

## 8. Services

The `services` directory contains functionality used by the application to communicate with external services and handle shared application operations.

```text
services/
|
|-- api/
|
|-- authentication/
|
`-- notifications/
```

Services keep communication and shared operations separate from the user interface.

---

## 8.1 API Services

The `api` directory contains the services used for communication between the Flutter application and the Bloom backend.

```text
Bloom Mobile
     |
     | HTTP request
     v
API Service
     |
     v
Bloom Backend
```

API communication is used for functionality such as:

* Authentication
* User information
* Maternal profile information
* Symptom logging
* Care schedules
* Maternal health tips
* Location-related functionality
* Other information provided through the Bloom API

A simplified example of an API request in Dart is:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<void> getMaternalProfile(String token) async {
  final response = await http.get(
    Uri.parse('https://api.example.com/maternal-profile'),
    headers: {
      'Authorization': 'Bearer $token',
      'Content-Type': 'application/json',
    },
  );

  if (response.statusCode == 200) {
    final data = jsonDecode(response.body);
    print(data);
  }
}
```

The actual Bloom API URL and authentication configuration are provided by the project's environment configuration.

---

## 8.2 Authentication Services

Authentication-related functionality is organized under:

```text
services/
|
`-- authentication/
```

These services support authentication within the mobile application.

The authentication process communicates with the Bloom backend rather than handling authentication only within the local application.

```text
User
 |
 v
Mobile Application
 |
 | Authentication request
 v
Bloom Backend
 |
 v
Authentication
 |
 v
JWT / Authentication Response
```

After successful authentication, the mobile application can use the returned authentication information when communicating with protected backend endpoints.

---

## 8.3 Notification Services

Notification-related functionality is organized under:

```text
services/
|
`-- notifications/
```

These services support notification functionality within the mobile application.

Bloom uses notifications primarily for **reminders**, such as reminders associated with care schedules or other activities configured by the user.

For example:

```text
Mother sets reminder
        |
        v
Reminder information
        |
        v
Bloom Backend / Application
        |
        v
Mobile Notification
```

The notification service allows the application to display relevant reminder notifications to the user.

---

## 9. Screens

The mobile screens are organized according to the user roles and authentication functionality.

```text
screens/
|
|-- auth_screens/
|
|-- mothers_screens/
|
|-- caregiver_screens/
|
`-- chp_screens/
```

This organization keeps the interfaces for the different user roles separate.

---

## 9.1 Authentication Screens

Authentication screens are located under:

```text
screens/
|
`-- auth_screens/
```

These screens provide the user-facing authentication flow for the mobile application.

They can include interfaces for login, registration, verification, and other authentication-related steps.

---

## 9.2 Mother Screens

Mother-specific screens are located under:

```text
screens/
|
`-- mothers_screens/
```

The mother experience includes functionality such as:

* Maternal profile management
* Daily symptom logging
* Care scheduling
* Setting reminders
* Receiving reminder notifications
* Delivery date tracking
* Location functionality
* Maternal health tips

For example, a mother can enter a symptom through a Flutter form and submit it to the backend:

```dart
ElevatedButton(
  onPressed: () {
    // Submit symptom to the Bloom API
  },
  child: const Text('Log Symptom'),
)
```

The screen handles the user's interaction while the API service handles communication with the backend.

---

## 9.3 Caregiver Screens

Caregiver-specific screens are located under:

```text
screens/
|
`-- caregiver_screens/
```

These screens provide functionality intended for caregivers.

The caregiver experience allows relevant maternal information to be accessed through the functionality provided by the Bloom platform.

Access to information is handled through the application's backend API.

---

## 9.4 CHP Screens

Community Health Promoter functionality is organized under:

```text
screens/
|
`-- chp_screens/
```

These screens provide functionality intended for Community Health Promoters.

The CHP experience includes functionality related to interaction with assigned mothers and location-related information available through the Bloom platform.

---

## 10. Widgets

Reusable Flutter widgets are organized under:

```text
lib/
|
`-- widgets/
```

Widgets are used to provide reusable interface components across the application.

For example:

```dart
class BloomButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;

  const BloomButton({
    super.key,
    required this.text,
    required this.onPressed,
  });

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPressed,
      child: Text(text),
    );
  }
}
```

A reusable widget can then be used by multiple screens instead of recreating the same interface component.

---

## 11. Providers and State Management

Application providers are located under:

```text
lib/
|
`-- providers/
```

Providers are used by the mobile application to manage and provide application state to the relevant parts of the interface.

State management allows the application to update the interface when information changes.

For example, when user information is loaded from the API, application state can be updated and the relevant screen can display the new information.

A simplified provider example is:

```dart
class UserProvider {
  String? role;

  void setRole(String userRole) {
    role = userRole;
  }
}
```

The actual application providers can contain the state and operations required by the different Bloom features.

---

## 12. Constants

Application constants are organized under:

```text
lib/
|
`-- constants/
```

This directory contains values that are shared across different parts of the mobile application.

Keeping shared constants in one location avoids repeatedly defining the same values throughout the application.

Examples can include API configuration values, application labels, and other shared constants.

---

## 13. Utilities

Utility functionality is organized under:

```text
lib/
|
`-- utils/
```

This directory contains reusable supporting functionality used by the mobile application.

Utilities can be used for common operations that are required by more than one part of the application.

---

## 14. Application Styling and User Interface

Flutter provides the styling system used to create the Bloom mobile interface.

The application uses Flutter widgets together with themes, text styles, spacing, icons, images, and reusable components to maintain a consistent interface.

A Flutter theme can be configured using:

```dart
MaterialApp(
  theme: ThemeData(
    useMaterial3: true,
    textTheme: const TextTheme(
      bodyMedium: TextStyle(
        fontSize: 16,
      ),
    ),
  ),
  home: const WelcomeScreen(),
)
```

This allows common visual properties to be defined centrally rather than individually on every screen.

Reusable widgets under `widgets/` can also help maintain consistent buttons, cards, forms, and other interface components.

---

## 15. Assets

The mobile application contains assets under the `assets` directory.

```text
assets/
|
|-- images/
|-- icons/
`-- fonts/
```

### `images/`

Contains image assets used by the mobile application.

### `icons/`

Contains icon resources used by the application.

### `fonts/`

Contains font resources used by the application.

Assets are referenced by Flutter through the project configuration in `pubspec.yaml`.

For example:

```yaml
flutter:
  assets:
    - assets/images/
    - assets/icons/
```

---

## 16. API Integration

The mobile application communicates with the Bloom backend through the API services.

The general flow is:

```text
Mobile Screen
       |
       | User action
       v
API Service
       |
       | HTTP request
       v
Bloom Backend
       |
       | Application processing
       v
PostgreSQL
       |
       | Response
       v
Bloom Backend
       |
       v
API Service
       |
       v
Mobile Screen
```

For example, when a mother logs a symptom:

```text
Mother enters symptom
        |
        v
Flutter Symptom Screen
        |
        v
Symptom API Service
        |
        v
Bloom Backend API
        |
        v
Symptom Service
        |
        v
PostgreSQL
```

The response is then returned to the mobile application and displayed to the user.

This keeps database operations within the backend and prevents the Flutter application from directly accessing PostgreSQL.

---

## 17. Role-Based Mobile Functionality

The mobile application displays functionality according to the authenticated user's role.

```text
Authenticated User
        |
        v
      Role
        |
   +----+----+
   |    |    |
   v    v    v
Mother Caregiver CHP
```

For example:

**Mother**

* Manage maternal profile
* Log symptoms
* Set reminders
* Receive reminder notifications
* View maternal health tips
* Manage care schedules

**Caregiver**

* View maternal information made available to them
* Access relevant maternal information through the application

**CHP**

* View assigned mothers
* Access relevant maternal information
* Support mothers using available platform information
* Use relevant location functionality

The backend remains responsible for enforcing authorization; the mobile application should not be treated as the final security boundary.

---

## 18. Environment Configuration

The mobile project contains an `.env.example` file.

```text
mobile/
|
`-- .env.example
```

The example file provides the expected environment configuration for the application.

Environment-specific values should be configured locally rather than committing sensitive values to the repository.

For example, an API base URL can be configured through environment configuration rather than being repeated throughout the application.

```text
API_BASE_URL=https://api.example.com
```

The actual configuration values used by Bloom should match the deployed Bloom backend.

---

## 19. Flutter Dependencies

Flutter dependencies are defined in:

```text
mobile/
|
`-- pubspec.yaml
```

The `pubspec.yaml` file contains the packages and other project configuration required by the Flutter application.

Dependencies can be installed through Flutter's package management process.

From the mobile project directory:

```bash
flutter pub get
```

Packages used by the project can provide functionality such as HTTP communication, state management, notifications, location services, and other mobile capabilities.

---

## 20. Running the Mobile Application

To work with the mobile application locally, Flutter must be installed and configured on the development machine.

From the `mobile` directory:

```bash
flutter pub get
```

The application can then be launched on a configured emulator, simulator, or physical device.

```bash
flutter run
```

A specific device can also be selected using Flutter's normal device management commands.

The required environment configuration should be available before running features that depend on the Bloom backend API.

---

## 21. Building the Application

Flutter can create release builds for supported platforms.

For Android, a release APK can be generated using:

```bash
flutter build apk --release
```

For an Android App Bundle suitable for Google Play distribution:

```bash
flutter build appbundle --release
```

For iOS, the application can be built using:

```bash
flutter build ios --release
```

The final release process also requires the appropriate Android or iOS signing and platform configuration.

---

## 22. Appetize Deployment

Bloom can use **Appetize.io** to provide a browser-based demonstration of the mobile application.

Appetize allows a mobile application build to be uploaded and opened in a browser-based mobile device simulator. This is useful for demonstrations, testing user flows, and allowing others to interact with the application without installing the application directly on a physical device.

The general deployment process is:

```text
Flutter Project
      |
      v
Flutter Release Build
      |
      v
Android APK / Compatible Build
      |
      v
Appetize.io
      |
      v
Browser-Based Mobile Simulator
```

For example, an Android release APK can first be generated:

```bash
flutter build apk --release
```

The generated APK can then be uploaded to Appetize according to the deployment configuration used by the project.

After deployment, Appetize provides a browser-based interface through which the Bloom mobile application can be demonstrated.

The Appetize deployment is intended for **demonstration and testing** and is separate from distributing the application through the Google Play Store or Apple App Store.

---

## 23. Testing

Mobile tests are organized under the `test` directory.

```text
test/
|
|-- unit/
|-- widget/
`-- integration/
```

### Unit Tests

The `unit` directory contains tests for individual pieces of application logic.

### Widget Tests

The `widget` directory contains tests for Flutter widgets and interface components.

### Integration Tests

The `integration` directory contains tests that verify functionality across multiple parts of the application.

Testing helps verify that Flutter screens, application logic, API integration, and user flows work as expected before deployment.

---

## 24. Mobile Application and Backend Relationship

The Flutter application is the presentation and client layer of Bloom.

The backend remains responsible for application logic, authentication, authorization, validation, and database operations.

```text
Bloom Mobile
     |
     | HTTP / REST API
     v
Bloom FastAPI Backend
     |
     | Database operations
     v
PostgreSQL
```

This separation allows the mobile application and backend to be developed independently while communicating through defined API endpoints.

---
