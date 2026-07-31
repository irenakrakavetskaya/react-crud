# React CRUD — Project Manager

A lightweight **React + Vite** project manager app that lets you create and manage projects with their associated tasks. All state is managed in-memory with React's `useState` hook — no backend or persistence layer required.

## Features

- **Create projects** — provide a title, description, and due date (all fields are required; a modal error dialog is shown on invalid input)
- **Select projects** — click any project in the sidebar to view its details
- **Delete projects** — remove the currently selected project along with its tasks
- **Add tasks** — attach free-text tasks to the selected project
- **Delete tasks** — remove individual tasks from the task list
- **Empty state** — a friendly prompt guides users to create their first project

## Tech Stack

| Tool | Version |
|------|---------|
| [React](https://react.dev/) | ^19 |
| [Vite](https://vitejs.dev/) | ^8 |
| [Tailwind CSS](https://tailwindcss.com/) | ^4 |
| [ESLint](https://eslint.org/) | ^9 |

## Project Structure

```
src/
├── App.jsx                  # Root component — holds all state and handler functions
├── main.jsx                 # React entry point
├── index.css                # Global styles (Tailwind base)
└── components/
    ├── ProjectsSidebar.jsx  # Left sidebar with project list and "Add Project" button
    ├── NewProject.jsx       # Form to create a new project (uses refs for inputs)
    ├── NoProjectSelected.jsx# Empty-state screen shown on initial load
    ├── SelectedProject.jsx  # Project detail view (title, due date, description)
    ├── Tasks.jsx            # Task list with inline delete buttons
    ├── NewTask.jsx          # Input row for adding a new task
    ├── Modal.jsx            # Reusable dialog (rendered via React portal into #modal-root)
    ├── Button.jsx           # Shared styled button component
    └── Input.jsx            # Shared input / textarea component
```

## Getting Started

```bash
npm install
npm run dev
```

The dev server starts at `http://localhost:5173` by default.

## Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start the Vite dev server |
| `npm run build` | Production build (output to `dist/`) |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run ESLint across the project |

## Key Implementation Notes

- **State shape** — a single `projectsState` object in `App.jsx` holds `selectedProjectId`, `projects[]`, and `tasks[]`. Tasks are filtered by `projectId` when rendering the selected project.
- **`selectedProjectId` sentinel values** — `undefined` = no project selected (empty state), `null` = "add project" form is open, any other value = a project is selected.
- **Refs over controlled inputs** — `NewProject` and `NewTask` use `useRef` to read input values on save rather than managing controlled state.
- **Modal via portal** — `Modal.jsx` uses `createPortal` to render into `#modal-root` (defined in `index.html`), keeping the dialog outside the component tree for correct stacking context.
- **No persistence** — state lives in memory only; refreshing the page resets everything.
