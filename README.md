# Plant Disease AI Assistant

An AI-powered, browser-based application for preliminary screening of
plant diseases from leaf images.

## Project Overview

Plant Disease AI Assistant allows a registered user to upload a
plant-leaf photograph and submit it for image classification. The
backend sends the image to a configured Hugging Face Inference API using
the `linkanjarad/mobilenet_v2_1.0_224-plant-disease-identification`
model. The application displays the predicted class and confidence score
returned by the model and saves successful detections so the user can
review or delete their own history.

> **Important:** Results are preliminary model-generated indications,
> not confirmed diagnoses or a substitute for advice from a qualified
> agricultural specialist.

## Problem Statement

Plant disease symptoms can be difficult for non-specialists to identify
visually, and timely expert assessment may not always be available. This
project provides a simple image-based screening workflow that returns a
model-generated class and score.

## Objectives

-   Allow users to create accounts and sign in securely.
-   Allow authenticated users to upload supported plant-leaf images for
    classification.
-   Use a pre-trained image-classification model through the Hugging
    Face Inference API.
-   Display the predicted class and confidence score returned by the
    model.
-   Provide brief, cautious general guidance based on the returned
    label.
-   Save successful detections and allow users to view and delete their
    own history.
-   Protect user records and application secrets from unauthorized
    access.

## Key Features

-   Email-and-password registration and login.
-   Password hashing and JWT-protected API access.
-   Single plant-leaf image upload per detection request.
-   JPEG, PNG, and WEBP image support (maximum file size: 5 MB).
-   AI-based image classification through the configured Hugging Face
    model.
-   Prediction label and confidence-score display.
-   Brief rule-based general guidance based on the predicted label.
-   User-specific detection history, newest first (up to the latest 100
    records).
-   Ability for users to delete their own detection records and
    associated uploaded images.
-   Clear validation and error messages when input, authentication,
    upload, or inference fails.

## User Roles

### Visitor (Unauthenticated)

-   Open publicly accessible pages.
-   View registration and login interfaces.
-   Register an account or sign in.

### Registered User (Authenticated)

-   Upload a supported plant-leaf image for classification.
-   View the prediction, confidence score, and general guidance.
-   View their own detection history.
-   Delete their own detection records and associated uploaded images.

The current SRS does not define administrator or moderator
functionality; these roles are not included in the initial version.

## Technology Stack

  -----------------------------------------------------------------------------------------------------
  Component                           Technology
  ----------------------------------- -----------------------------------------------------------------
  Frontend                            React 18, Vite, JavaScript/JSX, HTML, CSS

  Routing                             React Router

  HTTP Client                         Axios

  Backend                             Node.js 20+, Express REST API

  Database                            MongoDB, Mongoose

  AI Service                          Hugging Face Inference API

  AI Model                            `linkanjarad/mobilenet_v2_1.0_224-plant-disease-identification`
                                      (MobileNetV2-based)

  Authentication                      JSON Web Tokens (JWT)

  Password Hashing                    bcryptjs

  Image Upload                        Multer
  -----------------------------------------------------------------------------------------------------

## System Workflow

1.  A visitor registers or signs in.
2.  The authenticated user uploads one supported plant-leaf image.
3.  The backend validates the image format and 5 MB size limit.
4.  The backend sends the image to the configured Hugging Face inference
    endpoint using server-side credentials.
5.  The application displays the predicted class and confidence score
    returned by the model.
6.  Brief general guidance is displayed based on the predicted label.
7.  Successful detection metadata is saved in MongoDB and appears in the
    user's detection history.

If inference fails or returns unusable data, the application displays an
error and does not invent a classification.

## Data Management

### User Data

The user record contains a name, unique email address, password hash,
and timestamps.

### Detection Data

A detection record contains the user reference, stored image path,
original filename, predicted label, confidence score, guidance text, and
timestamps.

Users can access and delete only their own detection records. The
initial history operation returns up to the latest 100 records.

## Security, Privacy, and Performance

-   Passwords are stored as bcrypt hashes, not plaintext.
-   Protected API operations require a valid JWT.
-   Hugging Face tokens, JWT secrets, and database credentials are kept
    in backend environment configuration and must not be exposed in
    frontend code or public repositories.
-   The backend validates image formats and file size before forwarding
    images to the inference service.
-   The backend uses security middleware, allowed-origin configuration,
    and request-rate limiting.
-   Ordinary pages and non-inference API operations should respond
    within 3 seconds under normal test conditions. AI inference time is
    measured separately.
-   Users can access only their own detection records.

## Scope and Limitations

### Included in the Initial Version

-   React/Vite frontend and Node.js/Express backend.
-   Registration, login, and JWT-protected operations.
-   Single-image upload in JPEG, PNG, or WEBP format, up to 5 MB.
-   Hugging Face-based image classification.
-   Prediction display, brief rule-based guidance, and user-specific
    detection history.
-   MongoDB storage for user and detection metadata.

### Not Included in the Initial Version

-   Training or fine-tuning a new machine-learning model.
-   A chatbot or generative-AI agricultural adviser.
-   Automatic pesticide selection, dosage calculation, or guaranteed
    treatment prescriptions.
-   Offline image inference.
-   Guaranteed identification of all plant species, diseases, pests, or
    nutrient deficiencies.
-   Administrator/moderator dashboard or management features.

Image quality, lighting, background, crop variety, and field conditions
may affect results. The model's supported class labels also limit what
it can identify. Important crop-management decisions should be confirmed
by a qualified agricultural specialist.

## Project Information

-   **University:** Northern University of Business and Technology
    Khulna
-   **Department:** Computer Science and Engineering (CSE)
-   **Course:** Software Development III
-   **Course Code:** CSE4104
-   **Section:** 7G
-   **Team ID:** CSE4104-7G-T07
-   **Submission:** Week 3

## Team Information

  Name        Role          Student ID
  ----------- ------------- -------------
  Asha Moni   Team Leader   11230321329

*Add the names, roles, and student IDs of the other team members before
submitting the final README.*

## Repository Structure

The repository has the required top-level folders for the initial project
setup. The `.gitkeep` files keep empty folders visible in GitHub. Add
implementation files to the relevant folders as development progresses.

```text
Plant-Disease-AI-Assistant/
├── frontend/
│   ├── .gitkeep
│   └── backend/
│       └── .gitkeep
├── backend/
│   ├── .gitkeep
│   └── ai-model/
│       ├── .gitkeep
│       └── database/
│           └── docs/
│               └── .gitkeep
├── database/
│   └── README.md
├── documentation/
│   └── .gitkeep
├── diagrams/
│   ├── diagram 1.jpeg
│   ├── diagram 2.jpeg
│   ├── diagram 4.jpeg
│   └── diagrqam 3.jpeg
└── README.md
```

The original root-level `database` placeholder text has been preserved
in `database/README.md`. Existing nested placeholder folders have been
retained.
## Configuration

The SRS identifies the following configuration variables:

**Backend:** `MONGODB_URI`, `JWT_SECRET`, `HF_TOKEN`, `HF_API_URL`,
`PORT`, `CLIENT_ORIGIN`

**Frontend:** `VITE_API_URL`

Keep real credentials and secret values in environment files that are
excluded from version control. Do not commit API tokens, passwords, or
database credentials to GitHub.

## Project Status

Requirements specification and initial design phase (Week 3). Update
this status as development progresses.

## Academic Use

This project is being developed as part of the CSE4104 Software
Development III course.
