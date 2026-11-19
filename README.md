# To Do List API & Frontend

A full-stack To-Do List application featuring a RESTful API built with Node.js and Express, PostgreSQL database integration through Prisma ORM, and a React frontend for displaying and monitoring tasks.

## Table of Contents

- [Overview](#overview)

- [Features](#features)

- [Screenshots](#screenshots)

- [Live Demo](#live-demo)

- [Tech Stack](#tech-stack)

- [Architecture](#architecture)

- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)

  - [Installation](#installation)

  - [Environment Variables](#environment-variables)

- [Project Structure](#project-structure)

- [Available Scripts](#available-scripts)

- [Development](#development)

- [Testing](#testing)

- [API Reference](#api-reference)

- [Deployment](#deployment)

- [Troubleshooting](#troubleshooting)

- [Contributing](#contributing)

- [License](#license)

- [Acknowledgements](#acknowledgements)

- [Contact](#contact)

---

## Overview

The To Do List API is a full-stack application demonstrating RESTful API development, relational database integration, and frontend-to-backend communication.

The backend provides an API for managing tasks, including creating, retrieving, updating, and deleting records. PostgreSQL stores the task data, while Prisma ORM handles database queries and schema management.

The frontend is built with React and Vite. It retrieves tasks from the deployed API and displays task information alongside basic statistics, including total tasks, task counts by status, and completion percentage.

The project demonstrates:

- RESTful API design and HTTP methods.

- Node.js and Express backend development.

- PostgreSQL database integration.

- Prisma ORM and database schema management.

- React component-based frontend development.

- Frontend and backend integration.

- Deployment of a frontend and backend as separate applications.

## Features

### Backend API

- **Retrieve Tasks:** Fetch all tasks stored in the PostgreSQL database.

- **Create Tasks:** Add new tasks with a title, owner, optional description, and status.

- **Update Tasks:** Modify existing task information, including task status.

- **Delete Tasks:** Permanently delete individual tasks.

- **Database Integration:** Use Prisma ORM to interact with PostgreSQL.

- **Task Status Management:** Support predefined task statuses through a PostgreSQL-compatible Prisma enum.

- **Input Validation:** Validate required task title and owner fields when creating tasks.

### Frontend

- **Task List:** Display task IDs, titles, descriptions, and statuses.

- **Task Statistics:** Display the total number of tasks.

- **Completion Percentage:** Calculate the percentage of completed tasks.

- **Status Breakdown:** Display the number of tasks belonging to each status.

- **Loading State:** Display a loading message while retrieving tasks.

- **Error Handling:** Display an error message when the API request fails.

- **Empty State:** Display a message when no tasks are available.

### Future Enhancements

The following features are potential improvements and are not currently implemented:

- User authentication and authorisation using JWT.

- Task deadlines and reminders.

- Interactive task creation, editing, and deletion through the frontend.

- Task filtering and sorting.

- Task activity tracking.

- Kanban-style task management.

- More comprehensive form validation.

- Expanded automated testing.

- Improved mobile and responsive layouts.

- Stronger typing with TypeScript across the application.

## Screenshots

Screenshots can be added to `docs/screenshots/` to demonstrate the application's interface.

### Task Dashboard

### Task Statistics

### API Response

## Live Demo

The application is deployed using separate hosting services for the frontend, backend, and database.

| Component          | Platform         | URL                                                                                              |
| ------------------ | ---------------- | ------------------------------------------------------------------------------------------------ |
| Frontend           | GitHub Pages     | [https://amalk.au/to-do-list-api/](https://amalk.au/to-do-list-api/)                             |
| Backend API        | Render           | [https://to-do-list-api-kh03.onrender.com](https://to-do-list-api-kh03.onrender.com)             |
| API Tasks Endpoint | Render           | [https://to-do-list-api-kh03.onrender.com/tasks](https://to-do-list-api-kh03.onrender.com/tasks) |
| Database           | Neon PostgreSQL  | [Neon](https://neon.com/)                                                                        |
| Portfolio          | Personal Website | [https://amalk.au](https://amalk.au)                                                             |

**Hosting considerations:**

The backend is hosted on a free Render instance. Free instances may spin down after periods of inactivity, resulting in a delay when the application receives its first request after becoming inactive.

The frontend and backend are deployed independently. The frontend communicates with the hosted backend API to retrieve task information.

## Tech Stack

| Category                  | Technology                            |
| ------------------------- | ------------------------------------- |
| Frontend                  | React 19                              |
| Frontend Tooling          | Vite 7                                |
| Backend                   | Node.js                               |
| Backend Framework         | Express 5                             |
| Language                  | JavaScript (ES Modules)               |
| Database                  | PostgreSQL                            |
| ORM                       | Prisma 6                              |
| Database Hosting          | Neon                                  |
| Frontend Hosting          | GitHub Pages                          |
| Backend Hosting           | Render                                |
| Package Manager           | pnpm 10.21.0 (declared by the server) |
| Frontend Linting          | ESLint 9                              |
| Middleware                | CORS                                  |
| Environment Configuration | dotenv                                |

### Key Dependencies

**Frontend**

- `react` – Component-based user interface development.

- `react-dom` – React DOM rendering.

- `vite` – Development server and production build tooling.

- `eslint` – JavaScript linting.

- `gh-pages` – GitHub Pages deployment.

**Backend**

- `express` – HTTP server and API routing.

- `@prisma/client` – Database access through Prisma.

- `prisma` – Database schema and migration tooling.

- `cors` – Cross-origin resource sharing.

- `dotenv` – Environment variable configuration.

## Architecture

The application follows a separated frontend and backend architecture.

### Application Flow

```
                User's Browser
                      |
                      |
                React Frontend
                  (Vite)
                      |
                      |
                HTTP Requests
                      |
                      v
              Express REST API
                (Node.js)
                      |
                      |
                 Prisma ORM
                      |
                      |
                      v
              PostgreSQL Database
                   (Neon)
```

### Frontend

The frontend is a React application built with Vite.

It retrieves task information from the backend using the Fetch API and displays the returned data.

The frontend also calculates basic task statistics using the retrieved records.

The Vite configuration specifies `/to-do-list-api/` as the deployment base path to support hosting under the portfolio domain's subdirectory.

### Backend

The backend uses Node.js and Express to expose RESTful API endpoints.

The API handles incoming HTTP requests, performs basic input validation, and delegates database operations to dedicated database query functions.

Express middleware handles:

- JSON request parsing.

- URL-encoded request parsing.

- Cross-origin resource sharing.

### Database

PostgreSQL stores the application's task records.

Prisma ORM provides the database access layer and defines the task schema.

The `Task` model contains:

| Field              | Type              | Description                   |
| ------------------ | ----------------- | ----------------------------- |
| `task_id`          | Integer           | Auto-incrementing primary key |
| `task_title`       | String            | Task title                    |
| `task_description` | String (optional) | Task description              |
| `task_status`      | TaskStatus enum   | Current task status           |
| `task_owner`       | String            | Task owner                    |
| `created_at`       | DateTime          | Record creation timestamp     |
| `updated_at`       | DateTime          | Last update timestamp         |

Supported task statuses:

- `not_started`

- `started`

- `complete`

- `deleted`

The `deleted` status is defined in the database enum. However, the current DELETE endpoint permanently removes records rather than changing their status to `deleted`.

## Getting Started

Follow these instructions to run the frontend and backend locally.

### Prerequisites

Ensure the following tools are installed:

- **Node.js:** A version compatible with the project's Vite and Express dependencies.

- **pnpm:** Version 10.21.0 is declared in the server package configuration.

- **PostgreSQL:** A running PostgreSQL database, either locally or through a hosted provider.

- **Git:** For cloning the repository.

You can verify your installations:

```
node --version
pnpm --version
git --version
```

### Installation

#### 1\. Clone the Repository

```
git clone https://github.com/amalk-au/to-do-list-api.git

cd to-do-list-api
```

#### 2\. Configure the Backend

Navigate to the server directory:

```
cd server
```

Install backend dependencies:

```
pnpm install
```

#### 3\. Configure Environment Variables

Create a `.env` file inside the `server/` directory.

```
touch .env
```

Add your PostgreSQL connection string:

```
DATABASE_URL="postgresql://username:password@localhost:5432/todo_db?schema=public"
PORT=4000
```

Replace the database credentials and connection details with your own PostgreSQL configuration.

#### 4\. Configure the Database

Ensure PostgreSQL is running and the target database exists.

Apply the Prisma migrations:

```
pnpm exec prisma migrate dev
```

This command uses the Prisma CLI to apply the database migrations.

#### 5\. Start the Backend

Start the backend development server:

```
pnpm dev
```

The API will be available at:

```
http://localhost:4000
```

#### 6\. Configure the Frontend

Open another terminal and navigate to the project directory.

```
cd to-do-list-api/client
```

Install frontend dependencies:

```
pnpm install
```

#### 7\. Start the Frontend

```
pnpm dev
```

The frontend development server will be available at:

```
http://localhost:5173
```

The frontend currently uses the deployed backend URL directly. To develop against your local backend, update the API URL in `client/src/App.jsx` to:

```
http://localhost:4000/tasks
```

The backend CORS configuration already allows requests from `http://localhost:5173`.

### Environment Variables

The backend uses the following environment variables:

| Variable       | Description                                           | Required |
| -------------- | ----------------------------------------------------- | -------- |
| `DATABASE_URL` | PostgreSQL connection string used by Prisma           | Yes      |
| `PORT`         | Backend server port. Defaults to `4000` when omitted. | No       |

Environment variables must be configured in `server/.env`.

The frontend currently uses a hardcoded backend URL in `client/src/App.jsx`. It does not currently have a documented environment-variable configuration.

**Important:** Never commit `.env` files, database credentials, or production secrets.

## Project Structure

```
to-do-list-api/
│
├── client/                     # React frontend
│   ├── public/                 # Public static assets
│   ├── src/
│   │   ├── assets/             # Frontend assets
│   │   ├── App.jsx              # Main React application
│   │   ├── App.css              # Application styles
│   │   ├── index.css            # Global styles
│   │   └── main.jsx             # React entry point
│   │
│   ├── index.html               # HTML entry point
│   ├── vite.config.js            # Vite configuration
│   └── package.json              # Frontend dependencies and scripts
│
├── server/                      # Node.js and Express backend
│   ├── prisma/
│   │   ├── migrations/           # Database migrations
│   │   ├── schema.prisma         # Prisma database schema
│   │   └── seed.ts               # Database seed script
│   │
│   ├── index.js                  # Express server entry point
│   ├── routes.js                 # API route definitions
│   ├── controller.js             # Request controllers
│   ├── database-queries.js       # Prisma database operations
│   ├── prisma.config.ts          # Prisma configuration
│   └── package.json              # Backend dependencies and scripts
│
├── docs/
│   └── screenshots/              # Project screenshots (to be added)
│
├── .gitignore
├── LICENSE
└── README.md
```

## Available Scripts

The frontend and backend have separate `package.json` files. Run commands from their respective directories.

### Backend Scripts

Run these commands from `server/`.

| Command                        | Description                                 |
| ------------------------------ | ------------------------------------------- |
| `pnpm dev`                     | Start the backend using Node.js watch mode  |
| `pnpm start`                   | Start the backend in normal execution mode  |
| `pnpm run seed`                | Execute the configured database seed script |
| `pnpm exec prisma migrate dev` | Apply Prisma database migrations            |

### Frontend Scripts

Run these commands from `client/`.

| Command          | Description                              |
| ---------------- | ---------------------------------------- |
| `pnpm dev`       | Start the Vite development server        |
| `pnpm build`     | Build the frontend for production        |
| `pnpm preview`   | Preview the production build locally     |
| `pnpm lint`      | Run ESLint                               |
| `pnpm predeploy` | Run the configured pre-deployment script |
| `pnpm deploy`    | Deploy the frontend using GitHub Pages   |

**Note:** The frontend's existing `predeploy` script invokes `npm run build`. The deployment scripts should be reviewed if pnpm-only execution is required.

There is no root-level package configuration or shared command for running both applications.

## Development

The project separates frontend and backend development into independent applications.

### Backend Development

1.  Navigate to `server/`.

2.  Install dependencies using `pnpm install`.

3.  Configure the PostgreSQL connection string in `.env`.

4.  Apply database migrations.

5.  Start the development server using `pnpm dev`.

The backend uses Node.js ES modules and Express routing.

Database operations are separated into `database-queries.js`, while request handling is implemented in `controller.js`.

### Frontend Development

1.  Navigate to `client/`.

2.  Install dependencies using `pnpm install`.

3.  Start the Vite development server using `pnpm dev`.

4.  Update the API URL when switching between local and production backends.

The frontend uses React hooks, including `useState` and `useEffect`, to retrieve and display task information.

### Development Guidelines

1.  Create a feature branch before implementing changes.

2.  Follow the existing project structure and coding conventions.

3.  Keep frontend and backend responsibilities separated.

4.  Validate API changes against the database schema.

5.  Run the available linting and build commands.

6.  Test API endpoints using an HTTP client such as Postman.

7.  Commit focused changes with descriptive messages.

## Testing

The project does not currently have a functional automated test suite.

The backend's `test` script is a placeholder that exits with an error indicating that no tests are specified.

The frontend does not currently define a test script.

### Manual API Testing

Use Postman or another HTTP client to test the backend endpoints.

| Method | Endpoint     | Expected Operation |
| ------ | ------------ | ------------------ |
| GET    | `/tasks`     | Retrieve all tasks |
| POST   | `/tasks`     | Create a task      |
| PUT    | `/tasks/:id` | Update a task      |
| DELETE | `/tasks/:id` | Delete a task      |

### Frontend Verification

Run the frontend development server:

```
pnpm dev
```

Verify:

- Tasks load from the API.

- Task statistics display correctly.

- Loading and error messages behave as expected.

- Empty task lists display the appropriate message.

Run the available frontend checks:

```
pnpm lint
pnpm build
```

## API Reference

The backend exposes a RESTful API for managing tasks.

### Base URLs

**Local development:**

```
http://localhost:4000
```

**Production:**

```
https://to-do-list-api-kh03.onrender.com
```

### API Endpoints

| Method | Endpoint     | Description               |
| ------ | ------------ | ------------------------- |
| GET    | `/`          | Retrieve API information  |
| GET    | `/tasks`     | Retrieve all tasks        |
| POST   | `/tasks`     | Create a new task         |
| PUT    | `/tasks/:id` | Update an existing task   |
| DELETE | `/tasks/:id` | Permanently delete a task |

### GET /tasks

Retrieve all tasks from the database.

**Example request:**

```
GET /tasks
```

**Example response:**

```
{
  "tasks": [
    {
      "task_id": 1,
      "task_title": "Learn Prisma ORM",
      "task_description": "Read documentation and practise CRUD examples",
      "task_status": "started",
      "task_owner": "amal",
      "created_at": "2025-11-05T12:30:00.000Z",
      "updated_at": "2025-11-05T12:30:00.000Z"
    }
  ]
}
```

### POST /tasks

Create a new task.

**Required fields:**

- `task_title`

- `task_owner`

**Optional fields:**

- `task_description`

- `task_status`

**Example request:**

```
POST /tasks
Content-Type: application/json
```

```
{
  "task_title": "Complete project documentation",
  "task_description": "Document API endpoints and installation instructions",
  "task_owner": "amal",
  "task_status": "not_started"
}
```

**Successful response:** HTTP `201 Created`.

The API returns a success message and the newly created task.

**Validation response:** HTTP `400 Bad Request` if the required title or owner is missing.

### PUT /tasks/

Update an existing task.

The endpoint accepts the task ID as a URL parameter and the fields to update in the JSON request body.

**Example request:**

```
PUT /tasks/1
Content-Type: application/json
```

```
{
  "task_status": "complete"
}
```

Supported update fields:

- `task_title`

- `task_description`

- `task_status`

- `task_owner`

### DELETE /tasks/

Permanently delete a task using its ID.

**Example request:**

```
DELETE /tasks/1
```

The endpoint returns a success message and the deleted task when successful.

A missing task returns HTTP `404 Not Found`.

### Task Status Values

The database schema defines the following status values:

| Status        | Description                                                                            |
| ------------- | -------------------------------------------------------------------------------------- |
| `not_started` | Task has not been started                                                              |
| `started`     | Task is currently in progress                                                          |
| `complete`    | Task has been completed                                                                |
| `deleted`     | Reserved status value; the current DELETE endpoint performs permanent deletion instead |

### API Notes

- Requests containing JSON must use `Content-Type: application/json`.

- Creating a task requires both `task_title` and `task_owner`.

- New tasks default to `not_started` when no status is provided.

- The current API does not implement authentication or authorisation.

- The current update controller does not explicitly handle missing records as HTTP 404 responses.

## Deployment

The application is deployed as separate frontend and backend services.

### Frontend Deployment

**Hosting:** GitHub Pages

**Live URL:**

[https://amalk.au/to-do-list-api/](https://amalk.au/to-do-list-api/)

The Vite configuration contains:

```
export default defineConfig({
  base: "/to-do-list-api/",
  plugins: [react()],
});
```

The `base` configuration is important because the application is deployed under a subdirectory of the portfolio domain.

Changing the deployment path requires updating this configuration.

To create a production build:

```
cd client
pnpm build
```

The build output is generated in the `dist/` directory.

The project also includes a GitHub Pages deployment script:

```
pnpm deploy
```

Review the existing deployment scripts before using them with pnpm, as the configured pre-deployment command currently invokes npm.

### Backend Deployment

**Hosting:** Render

**Live URL:**

[https://to-do-list-api-kh03.onrender.com](https://to-do-list-api-kh03.onrender.com)

The backend uses the `PORT` environment variable when provided by the hosting platform. Otherwise, it defaults to port `4000`.

Configure the following environment variables in the hosting environment:

| Variable       | Description                                        |
| -------------- | -------------------------------------------------- |
| `DATABASE_URL` | Production PostgreSQL connection string            |
| `PORT`         | Port supplied by the hosting platform, if required |

Ensure the production database is accessible and the Prisma schema is migrated before starting the application.

### Database Deployment

**Hosting:** Neon PostgreSQL

The production database is hosted separately from the backend.

Configure the database connection string through the backend's `DATABASE_URL` environment variable.

### CORS Configuration

The backend currently permits requests from:

```
origin: [
  "https://amalk.au",
  "http://localhost:5173"
]
```

If the frontend is moved to another domain or development port, update the backend CORS configuration accordingly.

## Troubleshooting

| Issue                                 | Possible Solution                                                                                |
| ------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Dependency installation fails         | Verify Node.js and pnpm versions. Run `pnpm install` from the appropriate application directory. |
| Database connection fails             | Verify PostgreSQL is running and check the `DATABASE_URL` value.                                 |
| Prisma migration fails                | Check database permissions, connection details, and migration state.                             |
| Backend fails to start                | Check the `.env` configuration and server logs.                                                  |
| Frontend cannot retrieve tasks        | Verify the backend is running and check the browser console and network requests.                |
| CORS errors                           | Confirm the frontend origin is included in the backend CORS configuration.                       |
| First API request is slow             | The free Render instance may have been inactive and require time to start.                       |
| Frontend deployment has broken assets | Verify the Vite `base` configuration matches the deployment subdirectory.                        |
| Frontend build fails                  | Run `pnpm install` and inspect the Vite build output.                                            |

## Contributing

Contributions and suggestions are welcome.

To contribute:

1.  Fork the repository.

2.  Create a feature branch.

3.  Implement your changes.

4.  Test the frontend and backend.

5.  Run the available linting and build commands.

6.  Commit your changes.

7.  Open a pull request describing the changes.

For significant changes, consider opening an issue before implementing them.

## License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.

You are free to use, modify, and distribute this software under the terms of the licence.

See the [LICENSE](LICENSE) file for the complete licence text.

## Acknowledgements

- [React](https://react.dev/) – Frontend library.

- [Vite](https://vite.dev/) – Frontend development and build tooling.

- [Node.js](https://nodejs.org/) – JavaScript runtime.

- [Express](https://expressjs.com/) – Backend web framework.

- [Prisma](https://www.prisma.io/) – Database ORM.

- [PostgreSQL](https://www.postgresql.org/) – Relational database.

- [Neon](https://neon.com/) – Hosted PostgreSQL database.

- [Render](https://render.com/) – Backend hosting.

- [GitHub Pages](https://pages.github.com/) – Frontend hosting.

## Contact

- **Author:** Amal K.

- **GitHub:** [@amalk-au](https://github.com/amalk-au)

- **Repository:** [to-do-list-api](https://github.com/amalk-au/to-do-list-api)

- **Portfolio:** [https://amalk.au](https://amalk.au)

- **Issues:** [GitHub Issues](https://github.com/amalk-au/to-do-list-api/issues)

---

Developed by [amalk-au](https://amalk.au).
