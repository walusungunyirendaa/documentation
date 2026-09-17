# Informational Website

#**1. Overview**

The Bloom informational website provides public information about the Bloom platform and its services.

The website is intended for visitors who want to learn about Bloom before using the mobile application or administrative dashboard.

[Bloom Informational Website:](https://bloom-rho-sand.vercel.app/)

The informational website is separate from the authenticated administrative dashboard.

```text
Visitor

       |

       |

Informational Website

       |

       |

Bloom Platform Information
```

The website can provide information about Bloom, its purpose, features, services, and other public-facing content.

---

## **2. Purpose of the Informational Website**

The informational website provides a public entry point to the Bloom platform.

Its main purposes are:

* Introduce the Bloom platform
* Explain the purpose of Bloom
* Provide information about the platform's features
* Explain the services available to mothers, caregivers, and CHPs
* Provide general information about maternal health support
* Provide links to the Bloom application and other relevant resources

The informational website does not provide direct access to the PostgreSQL database.

---

## **3. Website Structure**

The informational website contains public-facing pages and content.

A typical structure is:

```text
Informational Website

|

|-- Home

|

|-- About Bloom

|

|-- Features

|

|-- Services

|

|-- How Bloom Works

|

|-- Contact / Information

|

`-- Links to Bloom Services
```

The exact pages depend on the implemented website structure.

---

## **4. Navigation Bar**

The informational website should be accessible from the main navigation bar.

The navigation should provide a clear link to the informational website so users can easily access public information about Bloom.

Example navigation structure:

```text
Navigation Bar

Home

Informational Website

About

Features

Contact

Login
```

The **Informational Website** item should link to the public informational website.

If the informational website is a separate route, the navigation link should point to that route.

Example:

```text
Informational Website

        |

        v

/informational
```

If it is hosted separately, the navigation item should point to the deployed website URL.

---

## **5. Placement in the Project**

The informational website should be placed in the frontend project alongside the other public-facing pages.

For example:

```text
frontend/

|

`-- app/

    |

    |-- informational/

    |   |

    |   `-- page.jsx

    |

    |-- admin/

    |

    |-- layout.jsx

    |

    `-- other frontend pages
```

The `informational` directory contains the page responsible for displaying the public informational website.

---

## **6. User Access**

The informational website is intended to be publicly accessible.

Unlike the administrative dashboard, visitors do not need an administrator account to view the public information.

```text
Visitor

       |

       v

Informational Website

       |

       v

Public Information
```

Administrative functionality remains protected separately.

```text
Administrator

       |

       v

Admin Login

       |

       v

Administrative Dashboard
```

---

## **7. Informational Website and Bloom Backend**

Public informational content may be displayed directly by the frontend when the content is static.

If information needs to be retrieved dynamically, the website can communicate with the Bloom backend through the API.

```text
Informational Website

       |

       | API Request (when required)

       v

Bloom Backend

       |

       v

Backend Services

       |

       v

PostgreSQL
```

The informational website does not connect directly to PostgreSQL.

---

## **8. Styling**

The informational website uses frontend styling to provide a consistent and user-friendly interface.

Styling can be used for:

* Navigation
* Headers
* Sections
* Buttons
* Cards
* Images
* Typography
* Spacing
* Responsive layouts
* Footer

The informational website should maintain the same general visual identity as the Bloom platform.

Example:

```css
.heroTitle {
  font-size: 42px;
  font-weight: 700;
}

.section {
  padding: 40px 20px;
}
```

---

## **9. Responsive Design**

The informational website should support different screen sizes.

The layout should work on:

* Desktop computers
* Tablets
* Mobile devices

Responsive CSS allows the website content and navigation to adapt to different screen widths.

Example:

```css
@media (max-width: 768px) {
  .heroTitle {
    font-size: 32px;
  }
}
```

---

## **10. Relationship with the Bloom Applications**

The informational website is one part of the Bloom platform.

```text
                         Bloom Platform

                              |

             +----------------+----------------+

             |                |                |

             v                v                v

      Informational       Mobile App      Admin Dashboard

        Website

             |                |                |

             |                |                |

             +----------------+----------------+

                              |

                              v

                       Bloom Backend

                              |

                              v

                         PostgreSQL
```

The informational website provides public information, while the mobile application provides functionality for users and the administrative dashboard provides management functionality for authorized administrators.

---

## **11. Informational Website and Mobile Application**

The informational website can provide information about the mobile application and explain the features available to users.

For example, it can explain that mothers can:

* Manage their maternal profile
* Log symptoms
* Set reminders
* Receive reminder notifications
* Access maternal health tips

Caregivers and CHPs can access the functionality and information provided to them according to their roles.

---

## **12. Informational Website and Administrative Dashboard**

The informational website is separate from the administrative dashboard.

The informational website is public-facing, while the administrative dashboard is restricted to authorized administrators.

```text
Public User

     |

     v

Informational Website

     |

     v

Public Information


Administrator

     |

     v

Admin Login

     |

     v

Administrative Dashboard

     |

     v

Protected Administrative Functions
```

This separation prevents public visitors from accessing administrative functionality.

---

## **13. Deployment**

The informational website should be deployed using the hosting platform configured for the frontend application.

The production deployment follows the general flow:

```text
Website Source Code

       |

       v

Git Repository

       |

       v

Hosting Platform

       |

       v

Hosted Informational Website
```

The production URL should be documented below:

```text
Bloom Informational Website:

[ADD THE HOSTED INFORMATIONAL WEBSITE LINK HERE]
```

Replace the placeholder with the actual deployed Bloom informational website URL.

---

## **14. Navigation Link**

The informational website should also be included in the project's navigation configuration.

For a Next.js application, the navigation can contain a link similar to:

```jsx
<Link href="/informational">
  Informational Website
</Link>
```

If the website is deployed separately, the link can instead point to the hosted website:

```jsx
<a href="https://bloom-rho-sand.vercel.app/">
  Informational Website
</a>
```

---

## **15. Access Flow**

The overall access flow is:

```text
Visitor

       |

       v

Navigation Bar

       |

       v

Informational Website

       |

       v

Bloom Information
```

For users who need the Bloom application:

```text
Visitor

       |

       v

Informational Website

       |

       v

Bloom Application
```

For administrators:

```text
Administrator

       |

       v

Admin Login

       |

       v

Admin Dashboard

       |

       v

Bloom Backend
```

---

## **16. Summary**

The Bloom informational website provides the public-facing introduction to the Bloom platform.

It is separate from the administrative dashboard and does not provide direct access to the database.

The informational website:

* Provides public information about Bloom
* Explains Bloom's features and services
* Provides information about the mobile application
* Provides navigation to relevant Bloom services
* Uses responsive frontend styling
* Can communicate with the Bloom backend when dynamic information is required
* Is deployed as a public-facing website
* Is accessible from the main navigation bar
* Has its deployed URL documented at the beginning of this page
