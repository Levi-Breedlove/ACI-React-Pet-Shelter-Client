<div align="center">

# ACI-React-Pet-Shelter-Client

### Building and Deploying the AnyCompany Pet Shelter Application

<p align="center">
  <img src="https://img.shields.io/badge/status-production_near_final-2ea44f?style=flat-square" alt="" />
  <img src="https://img.shields.io/badge/course-Developer_Intermediate_2_Q2_2026-1f6feb?style=flat-square" alt="" />
  <img src="https://img.shields.io/badge/phase-Week_7_X--Ray_Observability-0f766e?style=flat-square" alt="" />
  <img src="https://img.shields.io/badge/archive-Week_1--7_packages-334155?style=flat-square" alt="" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/frontend-react-61dafb?style=flat-square&logo=react&logoColor=black" alt="" />
  <img src="https://img.shields.io/badge/build-vite-646cff?style=flat-square&logo=vite&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/runtime-Python_3.12-3776ab?style=flat-square&logo=python&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/IaC-AWS_SAM-f59e0b?style=flat-square&logo=amazonaws&logoColor=white" alt="" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/api-API_Gateway-f59e0b?style=flat-square&logo=amazonaws&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/compute-Lambda-f59e0b?style=flat-square&logo=awslambda&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/database-DynamoDB-4053d6?style=flat-square&logo=amazondynamodb&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/storage-S3-569a31?style=flat-square&logo=amazons3&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/auth-Cognito-dd6b20?style=flat-square&logo=amazonaws&logoColor=white" alt="" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/workflow-Step_Functions-7c3aed?style=flat-square&logo=amazonaws&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/messaging-SNS-c2410c?style=flat-square&logo=amazonaws&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/logs-CloudWatch-2f855a?style=flat-square&logo=amazoncloudwatch&logoColor=white" alt="" />
  <img src="https://img.shields.io/badge/tracing-X--Ray-0f766e?style=flat-square&logo=amazonaws&logoColor=white" alt="" />
</p>

<p align="center">
  <b>Current Phase:</b> Week 7 complete - production-near archive with X-Ray observability, Step Functions reporting, and target-account validation pending
</p>

</div>

---

## Overview

This repository documents the **AnyCompany Pet Shelter** project for **ACI Developer Intermediate 2 Q2 2026**. It preserves the completed Week 1 through Week 7 course deliverables as packaged archives, along with the architecture notes, setup guidance, and sprint history needed to understand the project at each phase.

The application starts as a standalone **React + Vite** frontend and progresses into a serverless AWS application backed by **Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon S3, Amazon Cognito, AWS Step Functions, Amazon SNS, Amazon CloudWatch, and AWS X-Ray**. Public users can browse adoptable pets and submit adoption applications, while signed-in employees can review application records through Cognito-protected routes and trigger reporting workflows.

Weeks 6 and 7 extend the Week 5 authentication baseline with a reporting microservice, Step Functions orchestration, SNS email notification, report storage in S3, and IaC-managed tracing across API Gateway, Lambda, and the reporting state machine.

At this stage, the root repository is the documentation and deliverable index. The runnable application source remains inside the weekly zip packages under `docs/phase-zips/`.

---

## Client Scenario

**AnyCompany Pet Shelter** is a newly formed non-profit that needs a web application where customers can browse pets available for adoption and begin the adoption process, while the development team follows AWS serverless and microservices best practices introduced in the course.

The archived deliverables show that evolution step by step: Week 1 establishes the React client, Week 2 adds the pets service, Week 3 adds adoption reads, Week 4 adds adoption submissions, Week 5 secures employee application review with Amazon Cognito, Week 6 adds a reporting microservice, and Week 7 adds observability and tracing through CloudWatch and AWS X-Ray.

---

## Current Status

| Category | Current State |
|----------|---------------|
| Project Status | Production-near final archive; target-account validation pending |
| Course Track | ACI Developer Intermediate 2 Q2 2026 |
| Archive Coverage | Week 1 through Week 7 |
| Repository Type | Documentation and packaged phase artifacts |
| Current Package | `docs/phase-zips/week-7-pet-shelter-client.zip` |
| Current Focus | X-Ray tracing, CloudWatch-friendly logging, Step Functions retry behavior, and production-near archive cleanup |
| Live Source Location | Inside the weekly zip archives, not expanded at the repository root |
| Next Planned Phase | Target-account validation, production hardening, monitoring alarms, and deployment refinements |

---

## Architecture

<p align="center">
  <img src="docs/images/DI2-PetShelter-Lab7-Architecture-After.png" alt="Week 7 X-Ray Observability Architecture After" width="100%" />
</p>

**Architecture flow**<br>
`User → Amazon S3-hosted React web application → Amazon API Gateway`<br>
`Amazon API Gateway → Pets and Adoptions microservices → AWS Lambda functions → Amazon DynamoDB tables`<br>
`Employee authentication → Amazon Cognito hosted UI → protected adoption read routes`<br>
`Reporting workflow → POST /create-report → AWS Step Functions → report Lambdas → Amazon S3 report.html → Amazon SNS email notification`<br>
`Observability flow → API Gateway, Lambda, and Step Functions active tracing → AWS X-Ray service map and CloudWatch Logs`<br>
`Core flows → list pets, submit adoption applications, review adoption records after employee sign-in, and generate adoption-interest reports`

---

## Platform and Tooling

### AWS Services in Scope

| Service | Purpose |
|---------|---------|
| Amazon S3 | Hosts the static frontend and the pet image objects used by the Pets and Applications pages |
| Amazon API Gateway | Exposes the `GET /pets`, `GET /adoptions`, `GET /adoptions/{id}`, `POST /adoptions`, and `POST /create-report` routes, with Cognito authorization applied to employee adoption reads |
| AWS Lambda | Runs the pets/adoptions read handlers and the create-adoption handler |
| Amazon DynamoDB | Stores pet records and adoption application records in separate tables |
| Amazon Cognito | Provides employee hosted UI sign-in, token issuance, and sign-out support for protected application review pages |
| AWS Step Functions | Orchestrates the adoption-interest reporting workflow across report data, HTML generation, presigned URL, and notification steps |
| Amazon SNS | Sends report-availability email notifications after the reporting workflow completes |
| AWS X-Ray | Traces API Gateway, Lambda, and Step Functions requests for the Week 7 observability lab |
| AWS SAM / CloudFormation | Defines and deploys the backend infrastructure |
| IAM | Supports Lambda execution, DynamoDB read/write, API Gateway authorization setup, and role pass-through during deployment |
| Amazon CloudWatch Logs | Captures Lambda runtime logs, custom trace-context messages, and deployment/permission troubleshooting details |

### Tech Stack

| Layer | Tools / Services |
|-------|------------------|
| Languages | JavaScript / JSX, Python 3.12 |
| Frontend | React 18, Vite |
| Routing | React Router |
| Data Fetching | Axios |
| Testing | Vitest, Testing Library, Python `unittest`, ESLint, Vite production builds, packaged frontend smoke checks |
| Infrastructure as Code | AWS SAM, CloudFormation |
| Storage / Data | Amazon S3, Amazon DynamoDB |
| Observability | AWS X-Ray active tracing, CloudWatch Logs, trace-context logging, Step Functions execution history |
| Tooling | ESLint, npm, pip, AWS CLI, AWS SAM CLI |

---

## What This Capstone Demonstrates

The archived work demonstrates a staged move from a local React app to a serverless AWS application:

- React routing, reusable UI components, pet filtering, adoption forms, and application review pages
- API Gateway and Lambda integrations for pets, adoptions, adoption details, and adoption creation
- DynamoDB table usage for pet and adoption records, plus seed scripts for reusable setup
- S3-backed static hosting and image delivery considerations
- Cognito hosted UI authentication for employee-only application review workflows
- Step Functions orchestration for asynchronous report generation
- SNS notification and S3 report delivery patterns
- X-Ray tracing and CloudWatch log correlation for serverless observability
- AWS SAM deployment packaging, migration guides, validation scripts, and IAM/service audit notes

---

## Repository Layout

```bash
.
├── docs/                                      # Project documentation and supporting assets
│   ├── images/                                # Images used by documentation and README
│   │   └── DI2-PetShelter-Lab7-Architecture-After.png
│   └── phase-zips/                            # Archived project deliverables
│       ├── week-1-pet-shelter-client.zip      # Week 1 packaged React frontend snapshot
│       ├── week-2-pet-shelter-client.zip      # Week 2 packaged frontend + pets backend snapshot
│       ├── week-3-pet-shelter-client.zip      # Week 3 packaged frontend + pets/adoptions backend snapshot
│       ├── week-4-pet-shelter-client.zip      # Week 4 packaged POST request handling snapshot
│       ├── week-5-pet-shelter-client.zip      # Week 5 packaged Cognito authentication snapshot
│       ├── week-6-pet-shelter-client.zip      # Week 6 packaged reporting microservice snapshot
│       └── week-7-pet-shelter-client.zip      # Week 7 packaged X-Ray observability snapshot
└── README.md                                  # Project overview, architecture, and status tracking
```

---

## Phase Snapshot Summary

| Week | Package | Focus | Status |
|------|---------|-------|--------|
| Week 1 | `week-1-pet-shelter-client.zip` | React frontend baseline with local data and starter tests | Complete |
| Week 2 | `week-2-pet-shelter-client.zip` | Serverless pets API with API Gateway, Lambda, DynamoDB, and S3 image support | Complete |
| Week 3 | `week-3-pet-shelter-client.zip` | Adoptions read APIs and frontend application list/detail integration | Complete |
| Week 4 | `week-4-pet-shelter-client.zip` | Adoption application submission through `POST /adoptions` | Complete |
| Week 5 | `week-5-pet-shelter-client.zip` | Cognito employee authentication and protected adoption review routes | Complete |
| Week 6 | `week-6-pet-shelter-client.zip` | Reporting microservice with Step Functions, report-generation Lambdas, S3 report output, and SNS email notification | Complete |
| Week 7 | `week-7-pet-shelter-client.zip` | X-Ray tracing, CloudWatch-friendly logging, Step Functions retry behavior, IaC-managed observability, and cleaned final archive | Complete |

---

## Week 7 Final Package

Week 7 is the current final archive for this repository. It preserves the lab-complete X-Ray observability implementation while cleaning the package tree for reuse outside the temporary lab workspace.

| Package | Intended Use | What It Preserves or Changes |
|---------|--------------|-------------------------------|
| `docs/phase-zips/week-7-pet-shelter-client.zip` | Production-near final review and own-account migration starting point | Preserves the Week 6 reporting workflow, adds SAM-managed X-Ray tracing for API Gateway, Lambda, and Step Functions, adds CloudWatch-friendly logging, includes `phase-7-aws-migration-guide.md`, replaces session `.env` with `.env.example`, and excludes generated `node_modules` and `.aws-sam` artifacts |

The Week 6 archive remains available as the reporting lab snapshot, but Week 7 is the README reference point for final architecture, observability, and migration guidance.

---

## Phase Package Notes

The package trees below are intentionally collapsed so the README stays readable while still preserving the exact contents of each weekly deliverable.

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

<details>
<summary><b>Week 3 Package Contents</b></summary>

The archived Week 3 application package contains the React client, the expanded serverless backend for pets and adoptions read flows, and a full set of setup and AWS deployment support files for validating and deploying the package in a personal AWS account.

```bash
week-3-pet-shelter-client.zip
├── backend/
│   ├── handlers/
│   │   ├── get_pets/
│   │   │   └── getPets.py               # Lambda handler for GET /pets
│   │   ├── get_adoptions/
│   │   │   └── getAdoptions.py          # Lambda handler for GET /adoptions
│   │   └── get_adoption/
│   │       └── getAdoption.py           # Lambda handler for GET /adoptions/{id}
│   ├── scripts/
│   │   ├── populate_pets_table.py       # Seeds the deployed pets table
│   │   ├── populate_adoptions_table.py  # Seeds the deployed adoptions table
│   │   ├── adoptions.json               # Sample adoptions data used by the seed script
│   │   └── create_images_bucket.py      # Creates and configures the public-read images bucket
│   ├── tests/
│   │   ├── test_get_pets.py             # Backend tests for the pets Lambda handler
│   │   ├── test_get_adoptions.py        # Backend tests for the adoptions list handler
│   │   └── test_get_adoption.py         # Backend tests for the adoption detail handler
│   ├── template.yaml                    # AWS SAM template for the Week 3 backend resources
│   ├── samconfig.toml                   # Saved SAM deploy defaults for the Week 3 stack
│   └── .gitignore                       # Excludes SAM build artifacts and Python cache files
├── pet-shelter-client/
│   ├── .env.example                     # Frontend environment template for API and image settings
│   ├── src/
│   │   ├── components/                  # Updated frontend views and routed pages
│   │   ├── data/fallbackPets.js         # Packaged sample pets data for local fallback mode
│   │   ├── data/fallbackAdoptions.js    # Packaged sample adoptions data for local fallback mode
│   │   ├── assets/                      # Local imagery bundled with the archive
│   │   ├── App.jsx                      # Pets API integration and route setup
│   │   ├── styles.css                   # Main styling
│   │   ├── main.jsx                     # App bootstrap
│   │   └── index.css                    # Global styles
│   ├── public/
│   ├── .eslintrc.cjs                    # ESLint configuration
│   ├── .gitignore                       # Excludes node_modules, build artifacts, and .env
│   ├── README.md                        # Frontend-specific package notes and environment guidance
│   ├── index.html
│   ├── package.json                     # Frontend dependencies including Axios and React Router
│   ├── package-lock.json
│   └── vite.config.js
├── phase-3-aws-migration-guide.md       # Step-by-step guide for local setup, SAM deployment, and S3 website hosting
├── requirements-dev.txt                 # Python dev dependencies for backend validation
├── requirements.txt                     # Python runtime dependencies for local backend scripts
└── setup.sh                             # One-command setup for frontend and backend validation
```

### Structure Notes

- **`week-3-pet-shelter-client.zip`** contains the Week 3 archived full-stack snapshot for the adoptions read flow.
- `backend/template.yaml` defines two DynamoDB tables, three Lambda handlers, and API Gateway routes for `GET /pets`, `GET /adoptions`, and `GET /adoptions/{id}`.
- The Week 3 backend mirrors the lab's core architecture pattern with separate read-focused Lambda functions, distinct pets and adoptions DynamoDB tables, and AWS SAM as the deployment entry point.
- `backend/samconfig.toml` now defaults to a Week 3 stack name and saved SAM deployment settings that match the packaged migration guide.
- The packaged infrastructure intentionally improves a few lab defaults for reuse in personal AWS accounts, including SAM-managed `DynamoDBReadPolicy` permissions and DynamoDB `PAY_PER_REQUEST` billing.
- `phase-3-aws-migration-guide.md`, `requirements.txt`, `requirements-dev.txt`, and `setup.sh` were added so the archive can be used directly outside the lab environment.
- The frontend can run with packaged sample pets and adoptions data when `VITE_API_GATEWAY_URL` is not configured, which makes local verification possible before AWS resources exist.
- The archived UI still includes the adoption submission form shell, but the packaged backend remains read-only for adoptions at this stage.

</details>

<details>
<summary><b>Week 4 Package Contents</b></summary>

The archived Week 4 application package contains the React client, the expanded serverless backend for pets and adoptions read/create flows, and a Week 4 migration guide with explicit lab-to-personal-AWS deployment guidance plus an IAM/service setup audit.

```bash
week-4-pet-shelter-client.zip
├── backend/
│   ├── handlers/
│   │   ├── get_pets/
│   │   │   └── getPets.py               # Lambda handler for GET /pets
│   │   ├── get_adoptions/
│   │   │   └── getAdoptions.py          # Lambda handler for GET /adoptions
│   │   ├── get_adoption/
│   │   │   └── getAdoption.py           # Lambda handler for GET /adoptions/{id}
│   │   └── create_adoption/
│   │       └── createAdoption.py        # Lambda handler for POST /adoptions
│   ├── scripts/
│   │   ├── populate_pets_table.py       # Seeds the deployed pets table
│   │   ├── populate_adoptions_table.py  # Seeds the deployed adoptions table
│   │   ├── adoptions.json               # Sample adoptions data used by the seed script
│   │   ├── postDataTestPayload.json     # Sample payload for POST /adoptions smoke tests
│   │   └── create_images_bucket.py      # Creates and configures the public-read images bucket
│   ├── tests/
│   │   ├── test_get_pets.py             # Backend tests for the pets Lambda handler
│   │   ├── test_get_adoptions.py        # Backend tests for the adoptions list handler
│   │   ├── test_get_adoption.py         # Backend tests for the adoption detail handler
│   │   └── test_create_adoption.py      # Backend tests for adoption create validation and writes
│   ├── template.yaml                    # AWS SAM template for Week 4 backend resources
│   ├── samconfig.example.toml           # Example SAM deploy defaults without account-specific values
│   └── .gitignore                       # Excludes SAM build artifacts, local config, and Python cache files
├── pet-shelter-client/
│   ├── .env.example                     # Frontend environment template for API and image settings
│   ├── src/
│   │   ├── components/                  # Updated frontend views and routed pages
│   │   ├── data/fallbackPets.js         # Packaged sample pets data for local fallback mode
│   │   ├── data/fallbackAdoptions.js    # Packaged sample adoptions data for local fallback mode
│   │   ├── assets/                      # Local imagery bundled with the archive
│   │   ├── App.jsx                      # Pets API integration and route setup
│   │   ├── styles.css                   # Main styling
│   │   ├── main.jsx                     # App bootstrap
│   │   └── index.css                    # Global styles
│   ├── public/
│   ├── .eslintrc.cjs                    # ESLint configuration
│   ├── .gitignore                       # Excludes node_modules, build artifacts, and .env
│   ├── README.md                        # Frontend-specific package notes and environment guidance
│   ├── index.html
│   ├── package.json                     # Frontend dependencies including Axios and React Router
│   ├── package-lock.json
│   └── vite.config.js                   # Vite config with configurable base path
├── phase-4-aws-migration-guide.md       # Week 4 setup, deployment, validation, and IAM/service audit guide
├── requirements-dev.txt                 # Python dev dependencies for backend validation
├── requirements.txt                     # Python runtime dependencies for local backend scripts
└── setup.sh                             # One-command setup for frontend and backend validation
```

### Structure Notes

- **`week-4-pet-shelter-client.zip`** contains the Week 4 archived full-stack snapshot for adoption application creation.
- `backend/template.yaml` defines two DynamoDB tables, four Lambda handlers, and API Gateway routes for `GET /pets`, `GET /adoptions`, `GET /adoptions/{id}`, and `POST /adoptions`.
- `CreateAdoptionLambda` validates `applicant_name`, `email`, `phone`, and a non-empty `pets` array, generates an application `id`, adds `submitted_at`, writes to `AdoptionsTable`, and returns `201` with the created item.
- The SAM template uses `DynamoDBReadPolicy` for read handlers and `DynamoDBWritePolicy` scoped to `AdoptionsTable` for the create handler.
- `backend/samconfig.example.toml` replaces saved lab-specific deploy defaults so personal AWS account deployments can create their own local `samconfig.toml`.
- The frontend keeps packaged fallback data for read-only local verification and uses `VITE_API_GATEWAY_URL` for live API reads and adoption submissions.
- The frontend submit flow requires a deployed Week 4 API because `POST /adoptions` writes to DynamoDB.
- `phase-4-aws-migration-guide.md` documents local setup, SAM deployment, stack output lookup, frontend `.env` connection steps, API smoke tests, teardown, troubleshooting, known limitations, and an IAM/service setup audit.
- The cleaned archive excludes `.env`, `node_modules`, `dist`, `.aws-sam`, `.venv`, Python cache files, logs, credentials, and private keys.

</details>

<details>
<summary><b>Week 5 Package Contents</b></summary>

The archived Week 5 application package contains the React client with Cognito employee sign-in support, the existing serverless backend for pets and adoptions, and a Week 5 migration guide covering Cognito setup, API Gateway authorizers, protected route validation, and IAM/service audit steps for a personal AWS account.

```bash
week-5-pet-shelter-client.zip
├── backend/
│   ├── handlers/
│   │   ├── get_pets/
│   │   │   └── getPets.py               # Lambda handler for GET /pets
│   │   ├── get_adoptions/
│   │   │   └── getAdoptions.py          # Lambda handler for GET /adoptions
│   │   ├── get_adoption/
│   │   │   └── getAdoption.py           # Lambda handler for GET /adoptions/{id}
│   │   └── create_adoption/
│   │       └── createAdoption.py        # Lambda handler for POST /adoptions
│   ├── scripts/
│   │   ├── populate_pets_table.py       # Seeds the deployed pets table
│   │   ├── populate_adoptions_table.py  # Seeds the deployed adoptions table
│   │   ├── adoptions.json               # Sample adoptions data used by the seed script
│   │   ├── postDataTestPayload.json     # Sample payload for POST /adoptions smoke tests
│   │   └── create_images_bucket.py      # Creates and configures the public-read images bucket
│   ├── template.yaml                    # AWS SAM template for API Gateway, Lambda, DynamoDB, and CORS
│   └── samconfig.toml                   # SAM deploy defaults for the packaged lab/session stack
├── pet-shelter-client/
│   ├── .env                             # Session-specific API, S3 image, Cognito, client, and redirect settings
│   ├── src/
│   │   ├── components/
│   │   │   ├── Header.jsx               # Conditional employee Applications navigation
│   │   │   ├── Applications.jsx         # Sends bearer token to GET /adoptions
│   │   │   ├── ApplicationDetail.jsx    # Sends bearer token to GET /adoptions/{id}
│   │   │   ├── AdoptionForm.jsx         # Public POST /adoptions submission flow
│   │   │   ├── AboutUs.jsx
│   │   │   ├── Home.jsx
│   │   │   ├── Pets.jsx
│   │   │   └── Footer.jsx
│   │   ├── assets/                      # Local image assets bundled with the archive
│   │   ├── App.jsx                      # Cognito hosted UI sign-in/sign-out, token handling, and route setup
│   │   ├── styles.css                   # Main styling
│   │   ├── main.jsx                     # App bootstrap
│   │   └── index.css                    # Global styles
│   ├── public/
│   │   ├── logo.png
│   │   └── vite.svg
│   ├── .eslintrc.cjs                    # ESLint configuration
│   ├── .gitignore                       # Excludes node_modules and build artifacts
│   ├── README.md                        # Frontend-specific package notes
│   ├── index.html
│   ├── package.json                     # Frontend dependencies including Axios and React Router
│   ├── package-lock.json
│   └── vite.config.js                   # Vite config using the lab preview base path
├── phase-5-aws-migration-guide.md       # Week 5 setup, Cognito, authorizer, validation, and audit guide
├── requirements-dev.txt                 # Python validation dependencies including cfn-lint support
├── requirements.txt                     # Python runtime dependencies for backend scripts
└── setup.sh                             # One-command local setup and validation workflow
```

### Structure Notes

- **`week-5-pet-shelter-client.zip`** contains the current archived sprint package for Cognito authentication.
- Week 5 builds on the existing Week 4 pets and adoptions backend rather than adding new Lambda routes.
- The React client uses `VITE_COGNITO_AUTH_URL`, `VITE_CLIENT_ID`, and `VITE_REDIRECT_URI` to build Cognito hosted UI login/logout URLs.
- `App.jsx` captures the returned Cognito token from the URL hash, stores it in `localStorage`, tracks signed-in state, and shows employee sign-in/sign-out controls.
- `Header.jsx` only shows the `Applications` navigation link when an employee is signed in.
- `Applications.jsx` and `ApplicationDetail.jsx` send `Authorization: Bearer <token>` headers to the adoption read endpoints.
- `GET /pets` and `POST /adoptions` remain public flows so visitors can browse pets and submit adoption applications.
- The Week 5 guide documents the manual Cognito user pool, hosted UI domain, app client, callback/logout URL, employee user, and API Gateway authorizer setup needed outside the AWS Training lab.
- The API Gateway Cognito authorizer is documented as a post-deployment setup step for `GET /adoptions` and `GET /adoptions/{id}`; it is not currently defined inside `backend/template.yaml`.
- `backend/template.yaml` still references the fixed Lambda execution role `LambdaApplicationRoleSam`, so the guide explains either creating that role or updating the template before deployment.
- `pet-shelter-client/.env` is packaged with session-specific endpoint and Cognito values. Replace those values before reusing the archive in another AWS account and keep private data out of frontend source and environment files.

</details>

<details>
<summary><b>Week 6 Package Contents</b></summary>

The archived Week 6 application package captures the reporting microservice lab for the pet shelter application. It starts from the Cognito-secured Week 5 baseline and adds an adoption-interest reporting workflow with API Gateway, Lambda, Step Functions, S3 report output, and SNS email notification.

```bash
week-6-pet-shelter-client.zip
├── backend/
│   ├── handlers/
│   │   ├── get_pets/
│   │   │   └── getPets.py                    # Lambda handler for GET /pets
│   │   ├── get_adoptions/
│   │   │   └── getAdoptions.py               # Lambda handler for GET /adoptions
│   │   ├── get_adoption/
│   │   │   └── getAdoption.py                # Lambda handler for GET /adoptions/{id}
│   │   ├── create_adoption/
│   │   │   └── createAdoption.py             # Lambda handler for POST /adoptions
│   │   ├── create_report/
│   │   │   └── createReport.py               # Starts the Step Functions reporting workflow
│   │   ├── generate_report_data/
│   │   │   └── generateReportData.py         # Builds adoption-interest report data
│   │   ├── generate_html/
│   │   │   └── generateHtml.py               # Writes report.html to the report bucket
│   │   └── generate_presigned_url/
│   │       └── generatePresignedUrl.py       # Creates a temporary report URL
│   ├── scripts/
│   │   ├── populate_pets_table.py
│   │   ├── populate_adoptions_table.py
│   │   ├── populate_pets_interest_table.py
│   │   ├── create_images_bucket.py
│   │   ├── create_report_bucket.py
│   │   ├── pets_interest_data.json
│   │   ├── adoptions.json
│   │   └── postDataTestPayload.json
│   ├── statemachine/
│   │   └── report_generation.asl.json        # Step Functions workflow definition
│   ├── template.yaml                         # SAM template for API, Lambda, DynamoDB, Cognito, Step Functions, SNS, and S3 report access
│   ├── samconfig.toml                        # Lab/session SAM deploy defaults
│   └── .aws-sam/                             # Generated build artifacts preserved in the lab snapshot
└── pet-shelter-client/
    ├── .env                                  # Session-specific frontend/API/Cognito/report configuration
    ├── node_modules/                         # Generated dependencies preserved in the lab snapshot
    ├── src/
    ├── public/
    ├── package.json
    ├── package-lock.json
    ├── README.md
    ├── index.html
    └── vite.config.js
```

### Structure Notes

- **`week-6-pet-shelter-client.zip`** contains the reporting microservice snapshot for the Step Functions lab context.
- The archive adds `POST /create-report`, `CreateReportLambda`, `ReportGenerationStateMachine`, report-generation Lambda tasks, a `PetsInterestTable`, S3 report output support, and an SNS email notification topic/subscription.
- The state machine runs report data generation, HTML report creation, presigned URL generation, and SNS publishing as an orchestrated workflow.
- The package preserves the working lab tree, including generated `.aws-sam`, `node_modules`, and session-specific `.env` files. Treat it as a lab-complete snapshot rather than the production-clean archive.
- No separate `phase-6-aws-migration-guide.md` is present in this zip, so the README and lab context should be used with the package tree when reviewing Week 6.

</details>

<details>
<summary><b>Week 7 Package Contents</b></summary>

The archived Week 7 application package captures the final observability lab state for the pet shelter application. It starts from the Week 6 reporting workflow and adds CloudWatch/X-Ray observability changes in infrastructure as code, Step Functions retry behavior, trace-friendly logging, and a cleaner reusable package tree.

```bash
week-7-pet-shelter-client.zip
├── backend/
│   ├── handlers/
│   │   ├── get_pets/
│   │   │   └── getPets.py                    # Optimized read handler with custom trace-context logging
│   │   ├── get_adoptions/
│   │   │   └── getAdoptions.py
│   │   ├── get_adoption/
│   │   │   └── getAdoption.py
│   │   ├── create_adoption/
│   │   │   └── createAdoption.py
│   │   ├── create_report/
│   │   │   └── createReport.py
│   │   ├── generate_report_data/
│   │   │   └── generateReportData.py
│   │   ├── generate_html/
│   │   │   └── generateHtml.py               # Uses REPORT_BUCKET_NAME from SAM parameters
│   │   └── generate_presigned_url/
│   │       └── generatePresignedUrl.py       # Uses REPORT_BUCKET_NAME from SAM parameters
│   ├── scripts/
│   │   ├── populate_pets_table.py
│   │   ├── populate_adoptions_table.py
│   │   ├── populate_pets_interest_table.py
│   │   ├── create_images_bucket.py
│   │   ├── create_report_bucket.py
│   │   ├── pets_interest_data.json
│   │   ├── adoptions.json
│   │   └── postDataTestPayload.json
│   ├── statemachine/
│   │   └── report_generation.asl.json        # Reporting workflow with retry on GenerateHTML
│   ├── template.yaml                         # SAM template with Lambda, API Gateway, Step Functions, SNS, Cognito, and X-Ray tracing
│   └── samconfig.toml
├── pet-shelter-client/
│   ├── .env.example                          # Reusable frontend environment template
│   ├── src/
│   ├── public/
│   ├── package.json
│   ├── package-lock.json
│   ├── README.md
│   ├── index.html
│   └── vite.config.js
└── phase-7-aws-migration-guide.md            # Observability setup, deployment, and validation guide
```

### Structure Notes

- **`week-7-pet-shelter-client.zip`** is the current production-near final archive for this repository.
- `backend/template.yaml` enables active Lambda tracing through SAM `Globals.Function.Tracing`, API Gateway stage tracing with `TracingEnabled: true`, and Step Functions tracing with `Tracing.Enabled: true`.
- The template adds IaC-managed X-Ray permissions for `LambdaApplicationRoleSam` and IaC-managed report object access for the generated `report.html` object.
- `backend/statemachine/report_generation.asl.json` adds retry behavior around `GenerateHTML` with `States.ALL`, `IntervalSeconds: 5`, `MaxAttempts: 3`, and `BackoffRate: 2.0`.
- `GenerateHTMLLambda` is configured with a 5-second timeout, while temporary lab-only timeout/failure simulation snippets are intentionally left out of the final archive.
- The cleaned archive excludes generated `node_modules`, `.aws-sam`, and session `.env` artifacts, and replaces the frontend environment file with `.env.example`.

</details>

---

## Working With Phase Archives

This repository intentionally keeps the weekly deliverables packaged instead of expanding every app snapshot into the root directory. Each zip is a point-in-time course milestone that can be extracted, validated, deployed, or used as a backup reference.

Use the migration guide inside each archive for setup and deployment details. For the current sprint, start with `phase-7-aws-migration-guide.md` inside `week-7-pet-shelter-client.zip`, and refer back to `phase-5-aws-migration-guide.md` when validating the Cognito baseline that Week 7 builds on.

Inspect the current package:

```bash
unzip -l docs/phase-zips/week-7-pet-shelter-client.zip
```

Preview the Week 7 migration guide:

```bash
unzip -p docs/phase-zips/week-7-pet-shelter-client.zip phase-7-aws-migration-guide.md
```

Extract a package for local review:

```bash
mkdir -p /tmp/pet-shelter-week-7
unzip docs/phase-zips/week-7-pet-shelter-client.zip -d /tmp/pet-shelter-week-7
```

Package workflow:

1. Extract the week package you want to inspect or run.
2. Read that package's `phase-*-aws-migration-guide.md`.
3. Run the package's `setup.sh` when available.
4. Configure AWS, Cognito, S3, Step Functions, SNS, X-Ray, and frontend `.env` values for your own target account before deployment.

Do not commit `.env` files, AWS credentials, PEM keys, personal endpoint values, local dependency folders, generated build artifacts, or private account identifiers.

---

## Weekly Sprint Log

<details>
<summary><b>Week 1</b> - Establish the Pet Shelter React Baseline</summary>

### Sprint Focus
- Establish the standalone React application structure for the pet shelter scenario
- Build routed pages and reusable UI components for browsing pets and adoption-related views
- Display bundled local pet data with species filtering and shelter-day calculations
- Package the baseline with starter tests, local setup support, and S3 website hosting guidance

### Status
**Completed**

### Outcome
The Week 1 snapshot establishes the archived React baseline for the project. It includes Home, About Us, Pets, Adopt, Application Info, and Applications views, plus local pet data, species filtering, shelter-day calculations, starter tests, and packaged setup guidance.

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
Week 1 established the client-side foundation for the pet shelter project. The archived package captures a routed React app with reusable components, bundled local assets, starter tests, locked dependencies, a tested setup script, and a phase-specific Amazon S3 website hosting guide that prepares the project for later AWS integration.

</details>

<details>
<summary><b>Week 2</b> - Integrate the Serverless Pets Service</summary>

### Sprint Focus
- Add the serverless pets backend with AWS SAM, API Gateway, Lambda, and DynamoDB
- Seed pet records and prepare public S3 image hosting for the pets experience
- Move the pets listing from hardcoded data to live API-driven data with packaged fallback support
- Package validation and deployment guidance so the archive can be reused in a personal AWS account

### Status
**Completed**

### Outcome
The Week 2 snapshot integrates the archived React client with a serverless pets service. It adds the SAM-defined backend, DynamoDB pet storage and seeding, S3 image bucket support, and frontend API-driven pet retrieval with fallback data for local verification.

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
Week 2 transitions the project from a static React client into an AWS-backed application. The archived package now supports live pet retrieval through API Gateway, Lambda, and DynamoDB, uses S3-hosted pet images, and includes the setup files, tests, fallback data, and migration guidance needed to validate and deploy the snapshot outside the original course lab environment.

</details>

<details>
<summary><b>Week 3</b> - Add the Adoptions Read Flow</summary>

### Sprint Focus
- Add read-only adoptions routes with AWS SAM, API Gateway, Lambda, and DynamoDB
- Seed adoption records and expose list and detail endpoints for archived package testing
- Connect the Applications and Application Detail views to deployed APIs with fallback sample data
- Package updated setup, validation, and deployment support for the expanded full-stack snapshot

### Status
**Completed**

### Outcome
The Week 3 snapshot expands the serverless backend beyond pets-only retrieval and adds the adoptions read flow. The packaged frontend can now load pets, adoption lists, and individual adoption details from deployed AWS APIs while still falling back to bundled sample data when those resources are not configured.

### What Was Added
- `backend/template.yaml` — defines the Week 3 API Gateway routes, two DynamoDB tables, three Lambda functions, and CloudFormation outputs for the backend
- `backend/handlers/get_adoptions/getAdoptions.py` — returns the adoptions list from DynamoDB
- `backend/handlers/get_adoption/getAdoption.py` — returns a single adoption record by id
- `backend/scripts/populate_adoptions_table.py` and `backend/scripts/adoptions.json` — seed the adoptions table with sample records
- `backend/tests/test_get_adoptions.py` and `backend/tests/test_get_adoption.py` — backend tests for the new read handlers
- `pet-shelter-client/src/components/Applications.jsx` — loads adoption list data from the deployed API or fallback sample data
- `pet-shelter-client/src/components/ApplicationDetail.jsx` — loads adoption detail data from the deployed API or fallback sample data
- `phase-3-aws-migration-guide.md`, `requirements*.txt`, `setup.sh`, and the package README — packaged local setup and AWS deployment support aligned to the Week 3 scope

### What Was Verified
- Frontend validation passed with `npm ci`, `npm run lint`, and `npm run build`
- Backend validation passed with `python -m unittest discover backend/tests -v` and `python -m compileall backend`
- The archived package includes `phase-3-aws-migration-guide.md`, `requirements.txt`, `requirements-dev.txt`, and `setup.sh`
- The archived package excludes `node_modules`, `.aws-sam`, `.venv`, `.env`, and Python cache artifacts
- The packaged frontend still runs in fallback mode before AWS environment variables are configured

### Summary
Week 3 moves the project closer to the course target architecture by extending the archive with adoptions list and detail reads, matching frontend integrations, and reusable backend validation support. The package preserves the same core API Gateway, Lambda, and DynamoDB pattern used in the course while also keeping the personal-account-friendly SAM defaults, deployment guidance, and fallback-friendly frontend workflow introduced in the refreshed archive.

</details>

<details>
<summary><b>Week 4</b> - Implement POST Request Handling for Adoption Applications</summary>

### Sprint Focus
- Add POST request handling for adoption application submissions
- Extend the Week 3 SAM backend with a create-adoption Lambda handler and `POST /adoptions`
- Connect the React adoption form to the deployed API while preserving local fallback behavior for read-only pages
- Package Week 4 with validation support, migration guidance, and an IAM/service setup audit for personal AWS accounts

### Status
**Completed**

### Outcome
The Week 4 snapshot completes the adoption application create flow for the archived pet shelter app. The frontend can submit a selected-pet application to `POST /adoptions`, the backend validates and stores the record in DynamoDB, and the API returns the created application so the UI can navigate to the application detail route.

### What Was Added
- `backend/handlers/create_adoption/createAdoption.py` — parses JSON, validates required fields, generates an application id, adds `submitted_at`, writes to DynamoDB, and returns `201`
- `backend/tests/test_create_adoption.py` — backend tests for successful writes, invalid JSON, missing fields, empty pet selections, and DynamoDB write failures
- `backend/scripts/postDataTestPayload.json` — sample payload for deployed API smoke testing
- `backend/template.yaml` — adds `CreateAdoptionLambda`, `POST /adoptions`, CORS support for POST, and CloudFormation outputs for the create route
- `backend/samconfig.example.toml` — keeps deploy defaults portable and avoids committing personal or lab-specific SAM configuration
- `pet-shelter-client/src/components/AdoptionForm.jsx` — submits live adoption applications and navigates to `/applications/{id}` from the created response
- `phase-4-aws-migration-guide.md` — documents setup, deployment, validation, teardown, troubleshooting, and the Week 4 IAM/service setup audit

### What Was Verified
- Frontend validation passed with `npm ci`, `npm run lint`, `npm run build`, and a Vite dev server HTTP `200 OK` smoke check
- Backend validation passed with `python -m unittest discover backend/tests -v` and `python -m compileall backend`
- The Week 4 archive was rebuilt under `docs/phase-zips/` and checked for excluded generated or sensitive content
- AWS deployment was not executed in this environment because AWS CLI and SAM CLI are not installed; the package includes exact deployment and validation commands for a personal AWS account

### Summary
Week 4 turns the adoptions workflow from read-only into a create-capable serverless flow. The archive now contains the frontend POST integration, a portable SAM backend with scoped DynamoDB write permissions, backend tests, a smoke-test payload, and a migration guide that calls out which AWS resources and IAM permissions are handled by SAM versus which items still need manual setup or production review.

</details>

<details>
<summary><b>Week 5</b> - Secure Employee Application Review with Amazon Cognito</summary>

### Sprint Focus
- Add Amazon Cognito employee authentication to the React client
- Configure hosted UI sign-in/sign-out values through Vite environment variables
- Hide employee-only navigation until a user signs in
- Send Cognito bearer tokens to protected adoption read endpoints
- Document API Gateway Cognito authorizer setup, callback/logout URL matching, validation checks, and IAM/service audit steps

### Status
**Completed**

### Outcome
The Week 5 snapshot secures the employee-facing application review workflow. Public visitors can still browse pets and submit adoption applications, while signed-in employees can access the Applications navigation and send authenticated requests to the adoption list and adoption detail APIs.

### What Was Added
- `pet-shelter-client/src/App.jsx` — Cognito hosted UI login/logout URL construction, token capture from the URL hash, local token storage, and signed-in state handling
- `pet-shelter-client/src/components/Header.jsx` — conditional `Applications` navigation for signed-in employees
- `pet-shelter-client/src/components/Applications.jsx` — bearer-token request headers for `GET /adoptions`
- `pet-shelter-client/src/components/ApplicationDetail.jsx` — sign-in guard plus bearer-token request headers for `GET /adoptions/{id}`
- `pet-shelter-client/.env` — session-specific API Gateway, S3 image, Cognito hosted UI, client ID, and redirect URI configuration values
- `phase-5-aws-migration-guide.md` — personal-account setup guide for backend deployment, S3 images, DynamoDB seeding, Cognito hosted UI, API Gateway authorizers, validation, troubleshooting, and production hardening
- `setup.sh`, `requirements.txt`, and `requirements-dev.txt` — packaged local setup and validation support for backend syntax/template checks and frontend lint/build checks

### What Was Verified
- The Week 5 archive contains the Cognito-aware frontend files, backend SAM template, setup script, requirements files, and Week 5 migration guide
- The packaged setup workflow validates backend Python syntax, checks the SAM/CloudFormation template with `cfn-lint`, optionally runs `sam validate --lint` when SAM CLI is installed, and runs frontend lint/build
- The Week 5 guide includes expected signed-out and signed-in frontend behavior, protected API checks, CloudFormation/DynamoDB/Lambda/API Gateway/Cognito/S3 console checks, and common troubleshooting paths
- Live Cognito hosted UI and API Gateway authorizer validation must be rerun in the target AWS account because those values depend on the deployed account, Region, frontend URL, and Cognito app client

### Summary
Week 5 adds the security layer for employee-only adoption review. The archive now preserves Cognito login/logout wiring in the React client, token-bearing adoption read requests, conditional employee navigation, and a migration guide that explains which Cognito and API Gateway authorizer pieces must be created manually when moving out of the lab preset.

</details>

<details>
<summary><b>Week 6</b> - Build the Reporting Microservice with AWS Step Functions</summary>

### Sprint Focus
- Add a report-generation entry point through `POST /create-report`
- Orchestrate reporting work with AWS Step Functions instead of placing all logic in one Lambda
- Generate adoption-interest report data, write `report.html` to S3, create a presigned URL, and send the URL through SNS email notification
- Preserve the Week 5 Cognito-protected application review workflow while extending the backend with reporting resources

### Status
**Completed**

### Outcome
The Week 6 snapshot adds a reporting microservice to the pet shelter application. Employees can trigger an adoption-interest report workflow through API Gateway, the backend starts a Step Functions execution, and the workflow coordinates Lambda tasks for data preparation, HTML report generation, presigned URL creation, and SNS notification delivery.

### What Was Added
- `backend/handlers/create_report/createReport.py` — starts the report-generation state machine from `POST /create-report`
- `backend/handlers/generate_report_data/generateReportData.py` — reads pets and pet-interest data for the report
- `backend/handlers/generate_html/generateHtml.py` — writes the generated `report.html` object to S3
- `backend/handlers/generate_presigned_url/generatePresignedUrl.py` — creates the temporary report access URL
- `backend/statemachine/report_generation.asl.json` — defines the Step Functions workflow
- `backend/scripts/populate_pets_interest_table.py`, `pets_interest_data.json`, and `create_report_bucket.py` — prepare report source data and report storage
- `backend/template.yaml` — adds reporting Lambdas, `PetsInterestTable`, `ReportGenerationStateMachine`, SNS resources, and the `/create-report` API route

### What Was Verified
- The Week 6 archive is present under `docs/phase-zips/week-6-pet-shelter-client.zip`
- The package tree includes the expected reporting handlers, state machine definition, SAM template, helper scripts, Cognito-aware frontend, and report workflow resources
- The archive preserves lab-generated `.aws-sam`, `node_modules`, and session `.env` artifacts, so it should be treated as a lab snapshot rather than the cleaned final package

### Summary
Week 6 moves reporting out of a single synchronous request path and into a serverless workflow. The archive demonstrates how API Gateway, Lambda, Step Functions, DynamoDB, S3, and SNS can work together to generate and deliver an adoption-interest report while keeping the Week 5 authentication foundation intact.

</details>

<details>
<summary><b>Week 7</b> - Implement AWS X-Ray Observability and Tracing</summary>

### Sprint Focus
- Add AWS X-Ray tracing for Lambda, API Gateway, and the Step Functions reporting workflow through SAM/CloudFormation
- Add IAM permissions for X-Ray trace segment and telemetry writes
- Improve CloudWatch troubleshooting with a custom pets handler log message that includes trace context
- Add retry behavior to the report workflow and keep temporary lab failure simulations out of the final archive
- Rebuild the package as a cleaner production-near final deliverable with `.env.example` and without generated dependency/build folders

### Status
**Completed**

### Outcome
The Week 7 snapshot adds observability to the reporting-enabled pet shelter application. The SAM template now defines X-Ray tracing settings for the API, Lambda functions, and state machine; the reporting workflow retries the HTML generation task; and the cleaned package gives future deployments a safer baseline than the Week 6 lab snapshot.

### What Was Added
- `Globals.Function.Tracing: Active` in `backend/template.yaml` for Lambda active tracing
- `TracingEnabled: true` on the `PetsAPI` API Gateway stage
- `Tracing.Enabled: true` on `ReportGenerationStateMachine`
- `LambdaApplicationRoleXRayPolicy` for X-Ray trace and telemetry write permissions
- `LambdaApplicationRoleReportBucketPolicy` for scoped report object access
- Retry behavior on the `GenerateHTML` Step Functions task
- `GenerateHTMLLambda` timeout set to 5 seconds
- `pet-shelter-client/.env.example` for reusable frontend configuration
- `phase-7-aws-migration-guide.md` with observability deployment and validation guidance

### What Was Verified
- The Week 7 archive is present under `docs/phase-zips/week-7-pet-shelter-client.zip`
- The package tree contains 73 files and excludes `node_modules`, `.aws-sam`, and session-specific `.env` files
- `backend/template.yaml` contains the expected API Gateway, Lambda, Step Functions, SNS, Cognito, DynamoDB, IAM, and X-Ray infrastructure
- `backend/statemachine/report_generation.asl.json` contains retry behavior for `GenerateHTML`
- The migration guide documents the expected X-Ray, CloudWatch, API Gateway, Lambda, and Step Functions validation checks

### Summary
Week 7 turns the reporting-enabled application into an observable serverless workload. The final archive keeps the lab-aligned service-level X-Ray tracing, CloudWatch-friendly logging, retry behavior, SAM-managed observability resources, and reusable environment guidance while removing temporary failure simulations and generated local artifacts.

</details>

<!-- Future sprint entries will be added here after completion.
Keep upcoming sprint placeholders hidden from rendered README output until that work is actually completed and documented.
-->

---

## Milestones

### Remaining Hardening

The current Week 7 package now covers the completed pet shelter read/create flow, Cognito-protected employee review, Step Functions reporting, SNS notification, and X-Ray observability path. The remaining follow-up work is focused on target-account validation and production hardening rather than reshaping the archive.

- Deploy the Week 7 backend in the target AWS account, seed DynamoDB tables, create or update report/image S3 buckets, confirm the SNS email subscription, configure frontend `.env` values from `.env.example`, and run the documented API, reporting, Cognito, CloudWatch, and X-Ray checks.
- Replace lab/session defaults before reuse, including callback/logout URLs, report bucket names, notification email, CloudFront preview URLs, stack names, and any frontend environment values.
- Review the fixed `LambdaApplicationRoleSam` role with least-privilege tooling, including IAM Access Analyzer and a manual check of DynamoDB, S3, SNS, Step Functions, X-Ray, and CloudWatch Logs permissions.
- Replace learning-friendly wildcard CORS with the deployed frontend origin while keeping the `Authorization` header allowed for protected adoption reads.
- For production, replace the lab-compatible implicit grant with Authorization Code with PKCE for the browser client.
- Add CloudWatch alarms, dashboards, log retention settings, and sampling-rule review for API Gateway, Lambda errors, Step Functions failures, report generation latency, and Cognito authorization failures.
- Evaluate ADOT/OpenTelemetry before adding application-level tracing instrumentation beyond the lab's service-level X-Ray active tracing.
- Host production frontend builds with CloudFront plus private S3 origin access control, then add Route 53 and an ACM TLS certificate if a custom domain is needed.
- Add CI/CD with GitHub Actions for frontend lint/build, backend syntax/template validation, SAM validation/build, package tree checks, and deployment smoke tests.
- Separate dev, staging, and production environments with distinct SAM parameters, stack names, DynamoDB tables, S3 buckets, Cognito pools, SNS topics, X-Ray sampling choices, and budgets.

### Completion Checklist

- [x] Archive structure prepared under `docs/phase-zips/`
- [x] `week-1-pet-shelter-client.zip` completed with the React baseline, local setup workflow, starter tests, and Week 1 migration guide
- [x] `week-2-pet-shelter-client.zip` completed with the pets API backend, frontend API integration, validation support, and Week 2 migration guide
- [x] `week-3-pet-shelter-client.zip` completed with the pets and adoptions read APIs, frontend adoptions integration, validation support, and Week 3 migration guide
- [x] `week-4-pet-shelter-client.zip` completed with POST request handling, frontend create integration, validation support, Week 4 migration guide, and IAM/service setup audit
- [x] `week-5-pet-shelter-client.zip` completed with Cognito employee authentication, protected adoption read requests, Week 5 migration guidance, and IAM/service setup audit notes
- [x] `week-6-pet-shelter-client.zip` completed with Step Functions report orchestration, report-generation Lambdas, S3 report output, SNS notification, and lab snapshot tree notes
- [x] `week-7-pet-shelter-client.zip` completed with X-Ray tracing, CloudWatch-friendly logging, Step Functions retry behavior, `.env.example`, and cleaned package contents
- [x] Weekly sprint log aligned with the completed Week 1 through Week 7 zip coverage
- [ ] Run target-account production validation for the Week 7 stack, frontend environment, X-Ray traces, CloudWatch logs/alarms, SNS email delivery, and report workflow smoke tests
