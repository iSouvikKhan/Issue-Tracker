# Issue Tracker

A MEAN stack (MongoDB, Express, Angular, Node.js) issue tracking application. The Angular frontend lets you create, list, edit and delete issues, and the Express backend stores them in MongoDB through a small REST API.

## Features

- List all issues in a table showing title, responsible person, severity and status
- Create a new issue with a title (required), responsible person, description and severity (Low, Medium, High)
- Edit an existing issue, including its status (Open, In Progress, Done)
- Delete issues from the list
- New issues get the status `Open` by default

## Tech Stack

- **Frontend:** Angular 7, Angular Material, RxJS, TypeScript
- **Backend:** Node.js, Express 4, Mongoose 5, CORS, Babel (`babel-watch` with `babel-preset-env`)
- **Database:** MongoDB

## Project Structure

```
Issue-Tracker/
├── backend/
│   ├── models/Issue.js      # Mongoose schema for an issue
│   ├── server.js            # Express server and REST routes (port 4000)
│   ├── .babelrc
│   └── package.json
└── frontend/                # Angular CLI project
    ├── src/app/
    │   ├── components/
    │   │   ├── list/        # Issue table with Edit/Delete actions
    │   │   ├── create/      # Form to create an issue
    │   │   └── edit/        # Form to update an issue
    │   ├── issue.service.ts # HTTP calls to the backend
    │   ├── issue.model.ts
    │   └── app.module.ts    # Module and route definitions
    ├── angular.json
    └── package.json
```

## Prerequisites

- Node.js and npm (the project uses Angular CLI 7 and Babel 6, so an older Node.js LTS release, such as 10.x, is the most likely to work without issues)
- MongoDB running locally on the default port

## Installation

```bash
git clone https://github.com/iSouvikKhan/Issue-Tracker.git
cd Issue-Tracker

# Backend dependencies
cd backend
npm install

# Frontend dependencies
cd ../frontend
npm install
```

## Running the Application

1. **Start MongoDB** locally. The backend connects to `mongodb://localhost/issues` (the connection string is hard-coded in `backend/server.js`).

2. **Start the backend** (runs on `http://localhost:4000`):

   ```bash
   cd backend
   npm run dev
   ```

3. **Start the frontend** in a second terminal (runs on `http://localhost:4200`):

   ```bash
   cd frontend
   npm start
   ```

4. Open `http://localhost:4200` in your browser. The app redirects to `/list`.

The frontend calls the backend at `http://localhost:4000`, set in `frontend/src/app/issue.service.ts`.

## Frontend Routes

| Route       | Description                    |
|-------------|--------------------------------|
| `/list`     | List of all issues (default)   |
| `/create`   | Create a new issue             |
| `/edit/:id` | Edit an existing issue         |

## REST API

| Method | Endpoint              | Description               |
|--------|-----------------------|---------------------------|
| GET    | `/issues`             | Get all issues            |
| GET    | `/issues/:id`         | Get one issue by ID       |
| POST   | `/issues/add`         | Create an issue           |
| POST   | `/issues/update/:id`  | Update an issue           |
| GET    | `/issues/delete/:id`  | Delete an issue           |

An issue document has the fields `title`, `responsible`, `description`, `serverity` (spelled this way in the schema) and `status`.

## Other Frontend Scripts

Run these from the `frontend` folder:

- `npm run build` - build the app into `frontend/dist/`
- `npm test` - run unit tests with Karma
- `npm run lint` - lint with TSLint
- `npm run e2e` - run end-to-end tests with Protractor

## Known Issues

- The update route assigns `severity`, while the schema and frontend use `serverity`, so changing an issue's severity on the edit page is not saved.
- `backend/server.js` imports `body-parser`, which is not listed in `backend/package.json`; it is currently available because Express 4 installs it as a dependency.
