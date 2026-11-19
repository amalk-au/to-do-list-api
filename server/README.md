# To Do List – Backend API

A RESTful API built with Node.js and Express for managing tasks. The application uses PostgreSQL for data persistence and Prisma ORM for database operations.

Part of the [To Do List full-stack application](https://github.com/amalk-au/to-do-list-api).

## Features

- **CRUD Operations:** Create, retrieve, update and delete tasks.

- **RESTful API:** HTTP endpoints for task management.

- **PostgreSQL:** Relational database for persistent storage.

- **Prisma ORM:** Database queries and schema management.

- **Input Validation:** Validate required fields when creating tasks.

- **CORS:** Allow communication with the frontend application.

- **Task Status Management:** Support predefined task statuses.

## Live Demo

- **API:** [https://to-do-list-api-kh03.onrender.com](https://to-do-list-api-kh03.onrender.com)

- **Tasks Endpoint:** [https://to-do-list-api-kh03.onrender.com/tasks](https://to-do-list-api-kh03.onrender.com/tasks)

- **Frontend:** [https://amalk.au/to-do-list-api/](https://amalk.au/to-do-list-api/)

## Tech Stack

| Technology              | Purpose                       |
| ----------------------- | ----------------------------- |
| Node.js                 | JavaScript runtime            |
| Express 5               | Backend framework             |
| JavaScript (ES Modules) | Application logic             |
| PostgreSQL              | Relational database           |
| Prisma 6                | ORM and database management   |
| CORS                    | Cross-origin resource sharing |
| dotenv                  | Environment configuration     |
| pnpm                    | Package management            |

## Getting Started

### Prerequisites

- Node.js

- pnpm 10.21.0

- PostgreSQL database

### Installation

Clone the repository:

```
git clone https://github.com/amalk-au/to-do-list-api.git

cd to-do-list-api/server
```

Install dependencies:

```
pnpm install
```

### Environment Variables

Create a `.env` file in the `server/` directory:

```
DATABASE_URL="postgresql://username:password@localhost:5432/todo_db?schema=public"
PORT=4000
```

Update the database connection string with your PostgreSQL credentials.

### Database Setup

Apply Prisma migrations:

```
pnpm exec prisma migrate dev
```

### Start Development Server

```
pnpm dev
```

The API will be available at:

```
http://localhost:4000
```

## Available Scripts

Run these commands from the `server/` directory.

| Command                        | Description                                          |
| ------------------------------ | ---------------------------------------------------- |
| `pnpm dev`                     | Start the development server with Node.js watch mode |
| `pnpm start`                   | Start the server                                     |
| `pnpm run seed`                | Execute the database seed script                     |
| `pnpm exec prisma migrate dev` | Apply database migrations                            |

## API Reference

### Base URL

**Local:**

```
http://localhost:4000
```

**Production:**

```
https://to-do-list-api-kh03.onrender.com
```

### Endpoints

| Method | Endpoint     | Description               |
| ------ | ------------ | ------------------------- |
| GET    | `/`          | Retrieve API information  |
| GET    | `/tasks`     | Retrieve all tasks        |
| POST   | `/tasks`     | Create a task             |
| PUT    | `/tasks/:id` | Update a task             |
| DELETE | `/tasks/:id` | Permanently delete a task |

### Task Statuses

The database supports the following statuses:

- `not_started`

- `started`

- `complete`

- `deleted`

**Note:** The DELETE endpoint permanently removes tasks rather than assigning the `deleted` status.

### Example: Create a Task

**POST**`/tasks`

```
{
  "task_title": "Complete documentation",
  "task_description": "Document the backend API",
  "task_owner": "amal",
  "task_status": "not_started"
}
```

Required fields:

- `task_title`

- `task_owner`

## Project Structure

```
server/
├── prisma/
│   ├── migrations/             # Database migrations
│   ├── schema.prisma           # Database schema
│   └── seed.ts                 # Database seed script
│
├── index.js                    # Express server entry point
├── routes.js                   # API route definitions
├── controller.js               # Request controllers
├── database-queries.js         # Prisma database operations
├── prisma.config.ts            # Prisma configuration
├── package.json                # Dependencies and scripts
└── .env                        # Environment variables (not committed)
```

## Deployment

The backend is deployed on [Render](https://render.com/) and uses a hosted PostgreSQL database provided by [Neon](https://neon.com/).

Configure the following environment variables in the hosting environment:

| Variable       | Description                                                   |
| -------------- | ------------------------------------------------------------- |
| `DATABASE_URL` | Production PostgreSQL connection string                       |
| `PORT`         | Server port supplied by the hosting platform, when applicable |

Ensure database migrations have been applied before starting the production server.

**Production API:** [https://to-do-list-api-kh03.onrender.com](https://to-do-list-api-kh03.onrender.com)

**Hosting consideration:** Render's free instances may spin down after inactivity, causing delays on initial requests.

## Limitations

- No authentication or authorisation.

- No automated backend test suite currently configured.

- No pagination or advanced task filtering.

- The DELETE endpoint permanently removes records.

- Update operations do not explicitly return HTTP 404 for missing tasks.

## Related Links

- **Frontend:** [React Client](../client)

- **Repository:** [to-do-list-api](https://github.com/amalk-au/to-do-list-api)

- **Portfolio:** [https://amalk.au](https://amalk.au)

## License

Licensed under the [GNU General Public License v3.0](../LICENSE).

---

Developed by [Amal K.](https://amalk.au).
