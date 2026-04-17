<div align="center">

# ACI-React-Pet-Shelter-Client

### Building a Serverless Pet Shelter Application with React and AWS

<p align="center">
  <img src="https://img.shields.io/badge/status-in_progress-2ea44f?style=flat-square" alt="Status Badge" />
  <img src="https://img.shields.io/badge/course-developer_intermediate_2_q2_2026-1f6feb?style=flat-square" alt="Course Badge" />
  <img src="https://img.shields.io/badge/frontend-react-61dafb?style=flat-square&logo=react&logoColor=black" alt="React Badge" />
  <img src="https://img.shields.io/badge/cloud-AWS-232f3e?style=flat-square&logo=amazonaws&logoColor=white" alt="AWS Badge" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/build-vite-646cff?style=flat-square&logo=vite&logoColor=white" alt="Vite Badge" />
  <img src="https://img.shields.io/badge/api-API_Gateway-f59e0b?style=flat-square" alt="API Gateway Badge" />
  <img src="https://img.shields.io/badge/compute-Lambda-f59e0b?style=flat-square&logo=awslambda&logoColor=white" alt="Lambda Badge" />
  <img src="https://img.shields.io/badge/database-DynamoDB-4053d6?style=flat-square&logo=amazondynamodb&logoColor=white" alt="DynamoDB Badge" />
</p>

<p align="center">
  <b>Current Phase:</b> Week 2 complete, with Week 1 and Week 2 pet shelter deliverables refreshed, retested, and documented while later course weeks are still pending
</p>

</div>

---

## Overview

This repository documents the **AnyCompany Pet Shelter** project work for **Developer Intermediate 2 Q2 2026** and captures the currently completed build scope through the published Week 1 and Week 2 deliverables.

The progress preserved here starts with a standalone React + Vite frontend that uses local pet data, reusable UI components, client-side routing, and starter tests, then advances into a serverless pets microservice backed by **Amazon API Gateway, AWS Lambda, Amazon DynamoDB, and Amazon S3**.

The project is ultimately aiming to become a cloud-native pet shelter web application where users can browse adoptable pets through a static React frontend, retrieve live shelter inventory from AWS-backed microservices, and continue expanding into broader adoption-related workflows as later project work is completed. At the current stage, this repository functions as the **documentation and packaged-deliverable record** for that build progress. The Week 1 and Week 2 application snapshots are preserved as archived zip packages and have not yet been expanded into the repository as live source code.

---

## Repository Description

Developer Intermediate 2 Q2 2026 repository for documenting the AnyCompany Pet Shelter build, storing architecture assets, and preserving the packaged Week 1 frontend and Week 2 pets microservice snapshots that move the project toward a full AWS serverless application.

---

## Client Scenario

**AnyCompany Pet Shelter** is a newly formed non-profit that needs a web application where customers can browse pets available for adoption and begin the adoption process, while the development team follows AWS serverless and microservices best practices introduced in the course.

The initial archived version of the project uses a React frontend with hardcoded pet and application data. The Week 2 archived deliverable moves the project toward a live AWS-backed workflow by retrieving pet data through API Gateway and Lambda, storing pet records in DynamoDB, and preparing pet images and static site hosting for Amazon S3.

---

## Current Status

| Category | Current State |
|----------|---------------|
| Project Status | In Progress |
| Course Track | Developer Intermediate 2 Q2 2026 |
| Archive Coverage | Week 1 and Week 2 preserved |
| Repository Type | Documentation and packaged phase artifacts |
| Deployment Target | AWS serverless environment |
| Application Type | React web application with serverless backend integration |
| Current Focus | Week 1 and Week 2 archives refreshed, retested, and aligned |

---

## Architecture Diagram

This project follows the pet shelter MVP direction introduced in the course: a React single-page application hosted as a static site and a serverless pets microservice backed by API Gateway, Lambda, DynamoDB, and S3-hosted images.

<p align="center">
  <img src="docs/images/pet-shelter-architecture.png" alt="Pet Shelter App AWS Architecture Diagram" width="100%" />
</p>

**Architecture flow**  
`Browser → Amazon S3 static website hosting → React (Vite SPA) → React Router → Axios → Amazon API Gateway → AWS Lambda → Amazon DynamoDB`  
`Pet images → Amazon S3 → VITE_PET_IMAGES_BUCKET_URL → Pets page`

> This architecture represents the current Week 2 target state preserved in the archived package. The broader course later introduces additional AWS services, but those later weeks are not yet documented in this repository.

---

## Platform and Tooling

<table>
  <tr>
    <td valign="top" width="50%">

### AWS Services in Scope

| Service | Purpose |
|---------|---------|
| Amazon S3 | Hosts the static frontend and the pet image objects used by the Pets page |
| Amazon API Gateway | Exposes the `GET /pets` endpoint |
| AWS Lambda | Runs the backend logic that returns pet data |
| Amazon DynamoDB | Stores pet records for the pets listing |
| AWS SAM / CloudFormation | Defines and deploys the backend infrastructure |
| IAM | Supports Lambda execution permissions |

  </td>
  <td valign="top" width="50%">

### Tech Stack

| Layer | Tools / Services |
|-------|------------------|
| Languages | JavaScript / JSX, Python 3.12 |
| Frontend | React 18, Vite |
| Routing | React Router |
| Data Fetching | Axios |
| Testing | Vitest, Testing Library, Python `unittest` |
| Infrastructure as Code | AWS SAM, CloudFormation |
| Storage / Data | Amazon S3, Amazon DynamoDB |
| Tooling | ESLint, npm, pip |

  </td>
  </tr>
</table>

Later course modules mention additional AWS services such as Amazon Cognito, AWS Step Functions, Amazon SNS, Amazon CloudWatch, AWS X-Ray, AWS CodeBuild, AWS CodePipeline, Amazon ECR, Amazon EKS, and Amazon RDS, but those services are not yet represented in the archived Week 1 and Week 2 deliverables.

---

## Project Scope and What This Project Demonstrates

This project is designed to move a pet shelter application from a local mock-data frontend toward an AWS-integrated microservices architecture while building practical experience across React foundations, API integration, serverless infrastructure, testing, and packaged project documentation.

Through the work currently preserved in this repository, the project demonstrates:

- building a multi-page React client for a pet shelter use case
- analyzing a React application structure in the context of a microservices design course
- displaying and filtering adoptable pets by species
- calculating time in shelter from intake dates
- creating adoption-related UI flows and supporting pages
- writing starter frontend tests for rendering and utility logic
- preparing a static frontend for Amazon S3 website hosting
- replacing hardcoded pet data with live API retrieval
- defining serverless backend resources with AWS SAM
- seeding DynamoDB data and preparing S3-hosted image delivery
- packaging tested migration guides and local setup workflows for handoff use
- preserving milestone snapshots as packaged deliverables

---

## Phase Guide and Package Notes

This repository currently serves as the documentation and packaging layer for the project rather than the live application source itself.

At this stage, the repository contains:

- project documentation
- architecture image assets used in the README
- packaged **Week 1** and **Week 2** application snapshots stored as zip archives under `docs/phase-zips/`
- refreshed migration guides, setup files, and validation support inside the archived packages
- documentation aligned to the current pet shelter project scope rather than the unrelated appointments example

The live project files for both archived weeks are preserved inside the zip packages and are not yet extracted into the root repository as active source code.

This approach keeps the repository clean while still preserving the project deliverables, architecture assets, and the current state of work completed so far.

Each zip package acts as a point-in-time snapshot of the application and can be used for reference, backup, migration, or later extraction into a live working codebase.

---

## Repository Structure

```bash
.
├── docs/                                      # Project documentation and supporting assets
│   ├── images/                                # Images used in documentation and README
│   │   └── pet-shelter-architecture.png       # Architecture diagram for the project
│   └── phase-zips/                            # Archived project deliverables
│       ├── week-1-pet-shelter-client.zip      # Week 1 packaged React frontend snapshot
│       └── week-2-pet-shelter-client.zip      # Week 2 packaged frontend + backend snapshot
└── README.md                                  # Project overview, architecture, and status tracking
```

---

## Phase Package Contents

<details>
<summary><b>Week 1 Package Contents</b></summary>

The archived Week 1 application package contains the standalone React client source, the initial frontend test files, and a refreshed migration guide for local setup and course-aligned Amazon S3 website hosting.

```bash
week-1-pet-shelter-client.zip
└── pet-shelter-client/
    ├── .eslintrc.cjs                    # ESLint configuration for local validation
    ├── .gitignore                       # Excludes dependencies and build output
    ├── src/                              # Frontend source
    │   ├── components/                   # Routed page components and layout pieces
    │   │   ├── Header.jsx                # Navigation and branding
    │   │   ├── Home.jsx                  # Shelter landing page
    │   │   ├── AboutUs.jsx               # Shelter information page
    │   │   ├── Pets.jsx                  # Pet cards, species filter, days-in-shelter display
    │   │   ├── AdoptionForm.jsx          # Adoption form shell
    │   │   ├── ApplicationInfo.jsx       # Application details page
    │   │   ├── Applications.jsx          # Mock application list page
    │   │   └── Footer.jsx                # Footer and copyright
    │   ├── __test__/                     # Vitest test files
    │   │   ├── App.test.jsx              # Main page rendering checks
    │   │   └── utils.test.js             # Utility tests for shelter-day calculations
    │   ├── assets/                       # Local pet, shelter, and branding images
    │   ├── App.jsx                       # Route setup and local pets data
    │   ├── main.jsx                      # App bootstrap
    │   ├── utils.js                      # daysInShelter helper
    │   ├── styles.css                    # Main UI styling
    │   └── index.css                     # Global styles
    ├── public/
    │   └── logo.png                      # Public logo asset
    ├── index.html
    ├── package-lock.json                 # Locked npm dependency tree for repeatable installs
    ├── package.json                      # React, Vite, Vitest, Testing Library scripts and deps
    ├── phase-1-aws-migration-guide.md    # Step-by-step guide for local setup and S3 website hosting
    ├── setup.sh                          # One-command setup for local development
    ├── vite.config.js                    # Vite config
```

### Structure Notes

- **`week-1-pet-shelter-client.zip`** contains the standalone Week 1 React frontend snapshot.
- Pet data in this archive is stored directly in `src/App.jsx` as local mock data.
- The package includes `App.test.jsx` and `utils.test.js` for the frontend validation workflow.
- `phase-1-aws-migration-guide.md` and `setup.sh` were added so the archive can be used directly outside the lab environment.
- The Week 1 guide now follows the course-aligned Amazon S3 website hosting path for the static frontend.
- All pet and shelter imagery is served from bundled local assets in this archived version.

</details>

<details>
<summary><b>Week 2 Package Contents</b></summary>

The archived Week 2 application package contains the updated React client, the serverless AWS backend files used to retrieve live pet data, and refreshed setup files for local validation, SAM deployment, S3 image hosting, and S3 static website hosting in a personal AWS account.

```bash
week-2-pet-shelter-client.zip
├── backend/
│   ├── handlers/
│   │   └── get_pets/
│   │       └── getPets.py               # Lambda handler for GET /pets
│   ├── scripts/
│   │   ├── create_images_bucket.py      # Creates and configures the S3 images bucket
│   │   └── populate_pets_table.py       # Seeds DynamoDB with sample pets
│   ├── tests/
│   │   └── test_get_pets.py             # Backend unit tests for successful and failed handler responses
│   ├── template.yaml                    # AWS SAM template for API Gateway, Lambda, and DynamoDB
│   └── .gitignore                       # Excludes SAM build artifacts and Python cache files
├── pet-shelter-client/
│   ├── .env.example                     # Frontend environment template for API and S3 settings
│   ├── src/
│   │   ├── components/                  # Updated frontend views
│   │   ├── __test__/                    # Frontend test files
│   │   ├── data/fallbackPets.js         # Packaged sample data used when no API URL is configured
│   │   ├── test/setup.js                # Vitest Testing Library setup
│   │   ├── assets/                      # Local assets still used by some static pages
│   │   ├── App.jsx                      # API-driven pet retrieval with packaged fallback data
│   │   ├── styles.css                   # Main styling
│   │   ├── main.jsx                     # App bootstrap
│   │   └── index.css                    # Global styles
│   ├── public/
│   ├── .eslintrc.cjs                    # ESLint configuration
│   ├── .gitignore                       # Excludes node_modules, build artifacts, and .env
│   ├── index.html
│   ├── package.json                     # Frontend dependencies including Axios, Vitest, and PropTypes
│   ├── package-lock.json
│   ├── vite.config.js
├── phase-2-aws-migration-guide.md       # Step-by-step guide for local setup, SAM deployment, and S3 website hosting
├── requirements-dev.txt                 # Python dev dependencies for backend validation
├── requirements.txt                     # Python runtime dependencies for local backend scripts
└── setup.sh                             # One-command setup for frontend and backend validation
```

### Structure Notes

- **`week-2-pet-shelter-client.zip`** contains the Week 2 archived snapshot with both frontend and backend files.
- `backend/template.yaml` now defaults to a personal-account-friendly SAM deployment with SAM-managed IAM permissions and on-demand DynamoDB billing.
- The frontend can run with packaged sample data when `VITE_API_GATEWAY_URL` is not configured, making local verification easier before AWS resources are deployed.
- `phase-2-aws-migration-guide.md`, `setup.sh`, `requirements.txt`, and `requirements-dev.txt` were added so the archive can be used directly outside the lab environment.
- The Week 2 guide now documents the packaged backend deployment flow, stack-output lookup, DynamoDB seeding, S3 image hosting, and S3 static website deployment path used by the pet shelter project.
- Adoption submission and applications retrieval remain scaffolded in the frontend, but the archived package does not yet include fully deployed backend flows for those features.

</details>

---

## Weekly Status Log

<details>
<summary><b>Week 1 / Module 1</b> - Developing on AWS</summary>

### Lab Focus
- Review the pet shelter MVP use case and React project structure
- Create, validate, and test a basic React application
- Build routed pages and reusable components
- Display local pet data and add species filtering

### Status
**Completed**

### Outcome
The Week 1 snapshot contains a working React client with Home, About Us, Pets, Adopt, Application Info, and Applications views. The Pets page renders nine sample pets, supports dog and cat filtering, and calculates how long each pet has been in the shelter using a shared utility function.

### What Was Added
- `src/App.jsx` — route-based application shell with local pet data
- `src/components/Pets.jsx` — pet cards, species filter, and days-in-shelter display
- `src/components/AdoptionForm.jsx` — initial adoption form UI
- `src/components/ApplicationInfo.jsx` and `src/components/Applications.jsx` — starter adoption workflow views
- `src/utils.js` — `daysInShelter` helper used by the pets listing

### What Was Tested

| Test File | Tests | What It Covers |
|---|---|---|
| `App.test.jsx` | 2 | Main page heading and footer rendering |
| `utils.test.js` | 3 | `daysInShelter` behavior for same-day, 5-day, and 100-day cases |

### Summary
Week 1 established the client-side foundation for the project in the context of the Developer Intermediate 2 pet shelter scenario. The application was structured with React Router, reusable components, bundled local assets, and starter tests, creating a usable baseline for later AWS integration. The packaged archive has now also been refreshed with a tested local setup script, locked dependencies, and a phase-specific Amazon S3 website hosting guide.

</details>

<details open>
<summary><b>Week 2</b> - Serverless Pets Service Integration</summary>

### Lab Focus
- Create a serverless backend with AWS SAM
- Expose `GET /pets` through API Gateway and Lambda
- Store pet records in DynamoDB and seed sample data
- Move the pets listing from hardcoded data to live API-driven data

### Status
**Completed**

### Outcome
The Week 2 snapshot expands the project into a serverless full-stack application. A SAM template, Lambda handler, DynamoDB table setup, and S3 helper scripts were added, while the frontend was updated to fetch pet data from an API Gateway endpoint and build pet image URLs from an S3 bucket base URL.

### What Was Added
- `backend/template.yaml` — defines API Gateway, Lambda, DynamoDB, CORS settings, and stack output for the pets endpoint
- `backend/handlers/get_pets/getPets.py` — scans DynamoDB and returns pet data with CORS headers
- `backend/scripts/populate_pets_table.py` — seeds `PetsTable` with sample pets
- `backend/scripts/create_images_bucket.py` — creates a public-read S3 bucket for pet images
- `backend/tests/test_get_pets.py` — backend unit tests for the Lambda handler
- `pet-shelter-client/src/App.jsx` — supports API-driven pet retrieval with packaged fallback data when no API URL is configured
- `pet-shelter-client/src/components/Pets.jsx` — builds pet image URLs from `VITE_PET_IMAGES_BUCKET_URL` and falls back to local assets when needed
- `pet-shelter-client/src/__test__/` — frontend tests for the app shell and pets filtering
- `phase-2-aws-migration-guide.md`, `requirements*.txt`, and `setup.sh` — packaged local setup and personal-account deployment support

### What Was Verified
- Frontend validation passed with `npm run lint`, `npm run test`, and `npm run build`
- Backend validation passed with `python -m unittest discover backend/tests -v` and `python -m compileall backend`
- The archived backend includes helper scripts for DynamoDB seeding and S3 bucket creation
- The archived frontend includes `.env.example` and packaged fallback data so the UI can still be verified before AWS resources are deployed

### Summary
Week 2 transitions the project from a static React client into an AWS-backed application. The main completed feature is live pet retrieval through API Gateway, Lambda, and DynamoDB, supported by S3-hosted pet images and a static frontend deployment path that matches the pet shelter course documentation. The packaged archive has also been refreshed with tested setup files, migration guidance, and validation coverage for use outside the original lab environment.

</details>

Additional weekly logs will be added as the remaining project work is completed and documented.

---

## Milestones

- ✅ Developer Intermediate 2 pet shelter scenario reviewed
- ✅ Repository reorganized into a docs-based archive structure
- ✅ Architecture asset directory prepared
- ✅ Architecture diagram added to `docs/images/`
- ✅ Week 1 archive refreshed with a tested migration guide and setup workflow
- ✅ Week 2 archive refreshed with tested migration guides, setup files, validation support, and course-aligned AWS deployment steps
- [ ] Additional weekly logs added
- [ ] Later-stage backend and deployment work documented
