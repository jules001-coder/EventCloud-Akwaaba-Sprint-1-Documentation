# EventCloud (Akwaaba) — Sprint 1 Documentation (Initial Dev Stage)

![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![AWS Lambda](https://img.shields.io/badge/AWS-Lambda-FF9900?logo=awslambda&logoColor=white)
![Amazon Cognito](https://img.shields.io/badge/Amazon-Cognito-FF9900?logo=amazon-aws&logoColor=white)
![CloudFormation](https://img.shields.io/badge/AWS-CloudFormation-FF9900?logo=amazon-aws&logoColor=white)

A cloud-native event management platform — **Akwaaba** — built on AWS. This document covers the first sprint: what was planned, what each team delivered, and what is coming next.

---

## Table of Contents

- [Getting Started](#getting-started)
- [Tools Required](#tools-required)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Folder Description](#folder-description)
- [Architecture](#architecture)
- [AWS Services](#aws-services)
- [What Was Delivered This Sprint](#what-was-delivered-this-sprint)
- [Screenshots](#screenshots)
- [Core Features (Planned)](#core-features-planned)
- [Development](#development)
- [Running the App](#running-the-app)
- [Roadmap](#roadmap)
- [Future Enhancements](#future-enhancements)
- [Authors](#authors)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Getting Started

The project has 6 active branches — one per team role or feature area — with all changes merged into `develop` before being released to `main`.

- `main` — stable release branch
- `develop` — active development branch
- Feature branches — one per team member or feature

---

## Tools Required

To work with this project locally you will need:

- Node.js and npm — for the React frontend
- Python 3.x — for Lambda functions
- AWS CLI — to interact with AWS services
- AWS SAM CLI — for deploying serverless infrastructure
- An AWS account with appropriate IAM permissions
- A code editor (VS Code recommended)
- Git — to clone and manage the repository

---

## Installation

Clone the repository:

```bash
git clone https://github.com/Wild-Technological-Services/eventcloud.git
```

Navigate into the project:

```bash
cd eventcloud
```

Install frontend dependencies:

```bash
cd Frontend
npm install
```

Set up your AWS credentials:

```bash
aws configure
```

---

## Project Structure

```
eventcloud/
│
├── Backend/               # Python Lambda functions (auth + mock events)
├── Docs/                  # Project documentation and wireframes
├── Frontend/              # React web application (Akwaaba)
├── Infrastructure/        # AWS CloudFormation templates
├── .gitignore             # Files excluded from version control
├── Devops.README.md       # DevOps-specific setup and deployment notes
└── README.md              # Main project documentation (this file)
```

---

## Folder Description

**Backend/**
Contains the initial Python-based AWS Lambda functions built this sprint:
- Auth Lambda — handles user registration and login via Amazon Cognito
- Mock Events Lambda — returns placeholder event data so the frontend team can build and test pages without waiting for a full database

**Frontend/**
Contains the React web application. This sprint covers the event manager portal pages and the attendee-facing event pages. UI is built with React 18, Vite, and Tailwind CSS.

**Infrastructure/**
Contains the AWS CloudFormation templates that provision the base cloud environment — started this sprint. Includes the Cognito User Pool configuration.

**Docs/**
Contains project documentation, wireframes, and planning materials used throughout development.

---

## Architecture

At this sprint stage, the active architecture is:

```
Organisers & Attendees
        |
        ▼
  React SPA (Akwaaba)
        |
        ▼
   API Gateway
        |
        ▼
  AWS Lambda Functions (Python 3.12)
  ┌──────────────────────┬──────────────────────┐
  │   Auth Lambda        │  Mock Events Lambda  │
  │   (Login/Register)   │  (Placeholder Data)  │
  └──────────┬───────────┴──────────────────────┘
             |
             ▼
      Amazon Cognito
   (User Auth & JWT Tokens)
```

The full planned architecture — including DynamoDB, S3, SES, SNS, and CloudFront — is being built in upcoming sprints.

---

## AWS Services

Services active and in use this sprint:

| Service | Purpose |
|---------|---------|
| AWS CloudFormation | Infrastructure as Code — provisioning the base cloud environment |
| Amazon Cognito | User authentication — login, registration, and JWT token management |
| AWS Lambda | Serverless backend functions — auth and mock event data |

---

## What Was Delivered This Sprint

### Cloud Team
- Initiated AWS CloudFormation templates for base infrastructure provisioning
- Configured Amazon Cognito User Pool with role groups (Admin, Organiser, Attendee)
- Set up IAM roles and base account configuration

### Backend Team
- **Auth Lambda** — user registration and login backed by Amazon Cognito
- **Mock Events Lambda** — returns placeholder event data so the frontend team can develop and test pages independently

### Frontend Team

Pages built and delivered this sprint:

| Page | Description |
|------|-------------|
| Login Page | Sign-in screen for event managers to access the portal |
| Event Manager Navigation | Side navigation covering Dashboard, Events, and Participants |
| Events — List | View all events created by the organiser |
| Events — Add | Form to create a new event |
| Events — Update | Form to edit an existing event |
| Events — Delete | Ability to remove an event |
| Participants — List | View registered participants for an event |
| Dummy Dashboard | Overview screen for event managers with placeholder data |
| Public Events Page | Attendees can browse available public events and register |
| Invitation-Only Events Page | Invited attendees confirm availability before a ticket is issued |

---

## Screenshots

The following screenshots show the pages designed and developed during Sprint 1.

### Login Page
Sign-in screen for event managers to access the Akwaaba portal.

![Login Page](https://raw.githubusercontent.com/jules001-coder/EventCloud-Akwaaba-Sprint-1-Documentation/main/images/login-page.png)

---

### Dashboard
Overview screen for event managers showing event activity, participant counts, and event status breakdown.

![Dashboard](https://raw.githubusercontent.com/jules001-coder/EventCloud-Akwaaba-Sprint-1-Documentation/main/images/dashboard.png)

---

### Events List
A table view of all events with submission counts, registration numbers, status badges, and type — with search and filter controls.

![Events List](https://raw.githubusercontent.com/jules001-coder/EventCloud-Akwaaba-Sprint-1-Documentation/main/images/events.png)

---

### Add Event
Form for creating a new event — covering event name, description, date, time, location, capacity, status, and event type.

![Add Event](https://raw.githubusercontent.com/jules001-coder/EventCloud-Akwaaba-Sprint-1-Documentation/main/images/add-event.png)

---

### Participants List
A list of all participants who have registered or been invited to events, showing their RSVP status and registration date.

![Participants](https://raw.githubusercontent.com/jules001-coder/EventCloud-Akwaaba-Sprint-1-Documentation/main/images/participants.png)

---

## Core Features (Planned)

### Authentication
- User registration and login
- Email verification
- Password recovery
- Multi-factor authentication (MFA)
- Role-based access: Admin, Organiser, Attendee

### Event Management
- Create, edit, delete, and publish events
- Event categories, access types, and cover images
- Capacity management and seat tracking

### Registration
- Register for events
- Cancel registration
- Waiting list support

### Ticketing
- QR code generation per registration
- Ticket validation at check-in
- Digital ticket download

### Notifications
- Email confirmation on registration
- Reminder emails before events
- Event update and cancellation notices

### Organiser Dashboard
- Live event statistics
- Registration, ticket, and attendance reports

---

## Development

### Team Roles

| Role | Responsibilities |
|------|----------------|
| Cloud Architect | AWS infrastructure, IAM, CI/CD pipeline, branch strategy, deployment |
| Backend Developer(s) | Lambda functions, API logic, DynamoDB integration |
| Frontend Developer(s) | React web app, UI wireframes, page components |
| QA Engineer | Testing and documentation |

### Workflow

The team follows a feature-branch Git workflow:

1. Create a feature branch from `develop`
2. Implement the feature
3. Commit changes with descriptive messages
4. Open a Pull Request
5. Team code review
6. Merge into `develop`
7. Release tested features to `main`

---

## Running the App

### Frontend (local development)

The frontend can run locally using mock data — no deployed backend required:

```bash
cd Frontend
npm run dev
```

The app will run at `http://localhost:3000`

> If `VITE_API_BASE_URL` is not set in your `.env` file, the app automatically uses built-in mock data for local development.

### Backend (local Lambda testing)

```bash
cd Infrastructure
sam local start-api
```

This runs a local version of API Gateway and your Lambda functions for testing.

---

## Roadmap

| Week | Focus |
|------|-------|
| **Week 1** ✅ | Project setup — repository, branches, AWS account, IAM, base CloudFormation, Cognito, auth Lambda, mock events, core frontend pages |
| Week 2 | Authentication (Cognito) and Event Management (Lambda + DynamoDB) |
| Week 3 | Registration system and Ticketing (QR codes, validation) |
| Week 4 | Notifications (SES, SNS) and Organiser Dashboard |
| Week 5 | Testing, bug fixes, and performance optimisation |
| Week 6 | Final deployment, demo, and documentation |

---

## Future Enhancements

- Online payments integration
- AI-powered event recommendations
- Google Calendar and iCal integration
- Live streaming support
- Mobile push notifications
- Multi-language support
- React Native mobile application

---

## Authors

| Role | Contribution |
|------|-------------|
| Cloud Architect | Infrastructure, IAM, and Cognito setup |
| Backend Developer(s) | Auth Lambda and Mock Events Lambda |
| Frontend Developer(s) | React UI, portal pages, and attendee event pages |
| QA Engineer | Testing and documentation |

---

## License

This project is licensed under the MIT License — see the LICENSE file for details.

---

## Acknowledgments

- AWS Documentation — official AWS service guides
- AWS SAM Documentation — serverless deployment reference
- All team members who contributed across cloud, backend, frontend, and QA
