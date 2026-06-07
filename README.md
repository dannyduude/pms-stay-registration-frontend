pms-stay-registration-frontend

Objective

pms-stay-registration-frontend is the React frontend for the PMS Stay Registration module.

It provides one frontend application with two route groups:

* admin reservation management
* guest intake form for guests

The frontend calls only pms-stay-registration-view-service.

Service Type

Frontend React application.

Tech Stack

* React
* TypeScript
* Vite
* Docker

Template

This frontend is based on:

gravity-react-ts-standalone-template

The implementation should preserve the conventions of the template.

Responsibilities

This frontend is responsible for:

* rendering admin reservation screens
* rendering guest intake screens
* allowing admin to create and view reservations
* allowing admin to view and manage persons attached to reservations
* allowing admin to upload documents for OCR
* allowing admin to generate guest intake links
* allowing guests to open tokenized intake URLs
* allowing guests to enter person data manually
* allowing guests to upload DNI, NIE or passport images
* showing OCR parsed fields in an editable form
* submitting confirmed person data through the view-service

Non-Responsibilities

This frontend must not:

* connect to MongoDB
* call pms-stay-registration-service directly
* implement OCR itself
* parse DNI, NIE or passport data itself
* contain backend business logic
* generate final police TXT files

API Dependency

The frontend calls:

pms-stay-registration-view-service

Environment variable:

VITE_STAY_REGISTRATION_VIEW_API_BASE_URL=http://localhost:8080

Routes

Admin routes:

* /admin/reservations
* /admin/reservations/:reservationId
* /admin/reservations/:reservationId/persons/new
* /admin/exports

Guest intake routes:

* /guest-intake/:token
* /guest-intake/:token/persons/new
* /guest-intake/:token/confirmation

Main Screens

Admin:

* reservations list
* reservation detail
* create/edit reservation form
* persons table
* manual person form
* document upload/OCR flow
* parse text flow
* guest intake link generation
* export TXT placeholder

Guest:

* guest intake landing page
* basic stay information
* person creation form
* document upload
* OCR review form
* confirmation page

OCR User Flow

1. User uploads a document image or submits raw text.
2. Frontend sends the request to the view-service.
3. View-service forwards it to the domain backend.
4. Domain backend returns parsed fields.
5. Frontend displays parsed fields in an editable form.
6. User corrects or completes the form.
7. Frontend submits the final person data to the view-service.

Local Development

Install dependencies:

npm install

Run locally:

npm run dev

Default local URL:

http://localhost:5173

The frontend expects the view-service at:

http://localhost:8080

Architecture Rule

This frontend renders screens only. It does not own business logic and does not access databases directly.
