
Bloom applies cybersecurity measures to protect user accounts, sensitive maternal health information, API endpoints, and administrative functionality.

### JWT Authentication

Bloom uses **JSON Web Tokens (JWT)** to authenticate users.

After successful login, a JWT is used to identify the authenticated user when accessing protected API endpoints.

**Meaning:** JWT helps the system verify that a request is coming from an authenticated user.

---

### Role-Based Access Control

Bloom uses **role-based access control (RBAC)** to ensure that users can only access functionality appropriate to their role.

- **Mother:** Can manage her maternal profile, log symptoms, set reminders, receive reminder notifications, and access maternal health tips.
- **Caregiver:** Can access information made available to them about the mothers they support.
- **Community Health Promoter (CHP):** Can access information required to support assigned mothers.
- **Administrator:** Can manage users, maternal health content, platform metrics, safety alerts, and administrator account settings.

**Meaning:** RBAC prevents users from accessing functions or information that belong to other roles.

---

### API Security

Protected API endpoints require authentication and authorization before allowing access to protected resources.

**Meaning:** API security prevents unauthorized users from accessing or modifying protected backend functionality.

---

### Rate Limiting

Bloom applies **rate limiting within a 15-minute window** to control excessive API requests.

**Meaning:** Rate limiting helps protect the API against excessive requests, brute-force attempts, and automated abuse.

---

### OTP Verification

Bloom uses **One-Time Password (OTP)** verification as an additional identity verification mechanism.

**Meaning:** OTP provides an additional verification step to confirm the user's identity.

---

### IDOR Protection

Bloom protects against **Insecure Direct Object Reference (IDOR)** vulnerabilities by checking whether the authenticated user is authorized to access the requested resource.

**Meaning:** A user cannot simply change an ID in an API request to access another user's private information.

---

### Password Hashing

User passwords are **hashed before being stored** and are not stored as plain text.

**Meaning:** Password hashing protects user credentials if the database is compromised.

---

### Least Privilege

Bloom follows the **principle of least privilege**, giving users and system components only the permissions required for their intended tasks.

**Meaning:** Users and system components do not receive unnecessary access to sensitive information or functionality.

---

### Sensitive Data Protection and Encryption

Bloom protects sensitive information such as **maternal health information, user credentials, authentication information, and other private user data**.

Sensitive information is protected using appropriate security controls, including encryption.

- **Encryption in transit** protects information while it is being transferred between the client, API, and backend.
- **Encryption at rest** protects sensitive information while it is stored.
- Passwords are protected using **hashing**, rather than reversible encryption.
- Sensitive credentials and secrets are stored in environment configuration and should not be committed to the repository.

**Meaning:** Encryption helps prevent unauthorized people from reading sensitive information during transmission or from stored data.

---

### Administrative Access

Administrative functionality is restricted to authorized administrator accounts.

Administrators can:

- Manage users
- Manage maternal health content and tips
- View platform growth and engagement metrics
- Monitor safety alerts
- Manage administrator account settings

**Meaning:** Restricting administrative access helps prevent unauthorized changes to users, content, platform information, and system settings.

---
### Security Summary

```text
Authentication
     |
     |-- JWT
     |-- OTP Verification
     |
     v
Authorization
     |
     |-- Role-Based Access Control
     |-- Least Privilege
     |-- IDOR Protection
     |
     v
API Protection
     |
     |-- Rate Limiting (15 minutes)
     |-- Protected Endpoints
     |
     v
Data Protection
     |
     |-- Sensitive Data Protection
     |-- Encryption
     |-- Password Hashing
     |
     v
Bloom Backend
     |
     v
PostgreSQL
```