# To Do List – Frontend

A React-based frontend for the [To Do List REST API](https://github.com/amalk-au/to-do-list-api). The application retrieves tasks from the backend API and displays task information, status breakdowns, and completion statistics.

## Overview

This project demonstrates frontend integration with a RESTful API using React and Vite.

The frontend communicates with the deployed Express backend to retrieve tasks from a PostgreSQL database.

## Features

- **Task Listing:** Retrieve and display tasks from the backend API.

- **Task Statistics:** Display the total number of tasks.

- **Completion Tracking:** Calculate the percentage of completed tasks.

- **Status Breakdown:** Display task counts by status.

- **Loading State:** Show feedback while retrieving tasks.

- **Error Handling:** Display API request errors.

- **Empty State:** Display a message when no tasks are available.

## Live Demo

- **Frontend:**[https://amalk.au/to-do-list-api/](https://amalk.au/to-do-list-api/)

- **Backend API:** [https://to-do-list-api-kh03.onrender.com](https://to-do-list-api-kh03.onrender.com)

- **Repository:** [to-do-list-api](https://github.com/amalk-au/to-do-list-api)

## Tech Stack

| Technology              | Purpose                              |
| ----------------------- | ------------------------------------ |
| React 19                | UI development                       |
| Vite 7                  | Development server and build tooling |
| JavaScript (ES Modules) | Application logic                    |
| CSS                     | Application styling                  |
| Fetch API               | Backend communication                |
| ESLint 9                | Code linting                         |
| pnpm                    | Package management                   |
| GitHub Pages            | Frontend hosting                     |

## Getting Started

### Prerequisites

- Node.js

- pnpm

### Installation

Clone the repository:

```
git clone https://github.com/amalk-au/to-do-list-api.git

cd to-do-list-api/client
```

Install dependencies:

```
pnpm install
```

### Development

Start the development server:

```
pnpm dev
```

Open:

```
http://localhost:5173
```

**Note:** The frontend currently uses the production backend URL directly. To connect to a locally running backend, update the API URL in `src/App.jsx`:

```
"http://localhost:4000/tasks"
```

## Available Scripts

Run these commands from the `client/` directory.

| Command        | Description                            |
| -------------- | -------------------------------------- |
| `pnpm dev`     | Start the Vite development server      |
| `pnpm build`   | Generate the production build          |
| `pnpm preview` | Preview the production build           |
| `pnpm lint`    | Run ESLint                             |
| `pnpm deploy`  | Deploy the frontend using GitHub Pages |

**Deployment note:** The existing `predeploy` script uses `npm run build`. Update it to `pnpm run build` to ensure deployment uses pnpm exclusively.

## Project Structure

```
client/
├── public/              # Public static assets
├── src/
│   ├── assets/          # Frontend assets
│   ├── App.jsx          # Main React application
│   ├── App.css          # Application styles
│   ├── index.css        # Global styles
│   └── main.jsx         # React entry point
├── index.html           # HTML entry point
├── vite.config.js       # Vite configuration
└── package.json         # Dependencies and scripts
```

## Deployment

The frontend is deployed using GitHub Pages and hosted under the portfolio domain.

**Live URL:**

[https://amalk.au/to-do-list-api/](https://amalk.au/to-do-list-api/)

The Vite configuration uses a subdirectory base path:

```
export default defineConfig({
  base: "/to-do-list-api/",
  plugins: [react()],
});
```

Build the production application:

```
pnpm build
```

The production files are generated in the `dist/` directory.

The project includes `gh-pages` for deployment.

## Limitations

- The frontend currently supports displaying tasks and statistics only.

- Task creation, editing, and deletion are
