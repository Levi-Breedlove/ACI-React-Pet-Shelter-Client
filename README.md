# Pet Shelter Client

A React-based pet shelter application built with Vite.

## Prerequisites

Make sure you have the following installed before getting started:

- [Node.js](https://nodejs.org/) v18 or higher
- npm (comes with Node.js)

## Setup Instructions

### 1. Install dependencies

After unzipping the project, navigate to the project folder and run:

```bash
npm install
```

This will install all required packages defined in `package.json`, including:

**Dependencies:**
- `react` ^18.3.1
- `react-dom` ^18.3.1
- `react-router-dom` ^6.24.1

**Dev Dependencies:**
- `vite` ^7.3.2
- `@vitejs/plugin-react` ^4.3.1
- `vitest` ^4.1.3
- `@vitest/coverage-v8` ^4.1.3
- `@testing-library/react` ^16.0.0
- `eslint` ^8.57.1 (+ react plugins)
- `jsdom` ^24.1.1
- `@types/react` ^18.3.3
- `@types/react-dom` ^18.3.0

### 2. Run the development server

```bash
npm run dev
```

The app will be available at `http://localhost:8081`

## Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start the development server on port 8081 |
| `npm run build` | Build the app for production |
| `npm run preview` | Preview the production build |
| `npm run lint` | Run ESLint on the src folder |
| `npm run test` | Run tests with Vitest and generate coverage report |
