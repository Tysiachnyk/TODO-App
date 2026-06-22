# ✅ React TypeScript Todo App
 
A fully-featured, production-ready Todo application built with **React** and **TypeScript**, integrated with a live REST API. Developed in three progressive stages with a strong focus on clean architecture, async state management, and smooth user experience.
 
---
 
## 🚀 Live Demo
 
> [DEMO LINK](https://Tysiachnyk.github.io/TODO-App/)

---
 
## 🛠️ Tech Stack
 
| Category | Tools |
|---|---|
| Frontend | React (Hooks, Functional Components) |
| Type Safety | TypeScript |
| Styling | CSS / Bulma |
| API Client | Custom `fetchClient.ts` (Fetch API) |
| Code Quality | ESLint + Prettier |
 
---
 
## ✨ Features
 
The app is built around the philosophy: **"Logic as simple as possible, UX as smooth as possible."**
 
- **Optimistic UI & Loaders** — Per-item loading spinners during create, toggle, rename, and delete operations
- **Double-Action Prevention** — Controls are disabled while any API request is in progress
- **Smart Focus Management** — Input fields auto-focus on load, after submission, and on errors
- **Toast Error Notifications** — Non-intrusive error messages that auto-dismiss after 3 seconds
- **API-First State** — No `localStorage`; all data is strictly synced with the backend
---
 
## 📋 Development Stages
 
### Stage 1 — Loading & Filtering
 
- User-specific todo fetching via `userId`
- Dynamic rendering: list and footer hidden when no todos exist
- Status filtering: **All**, **Active**, **Completed** with active state highlighting
- CSS-based error component (hidden without unmounting to avoid layout flicker)
### Stage 2 — Adding & Deleting
 
- Form validation: trims whitespace, blocks empty submissions
- Temporary optimistic todo (`id: 0`) rendered instantly while `POST` resolves
- Input text preserved on API failure for quick re-submission
- Per-item loading overlay on deletion
- **"Clear Completed"** — parallel `DELETE` requests; successful deletions proceed even if one fails
### Stage 3 — Toggling & Renaming
 
- Toggle individual todo status with loading state
- **Toggle All** — smart logic sends API requests only for todos that actually need to change
- **Inline Editing:**
  - Triggered by double-click
  - Saves on `Enter` or `onBlur`
  - Cancels on `Escape` or if title is unchanged
  - Triggers deletion workflow if title is cleared completely
---
 
## 📡 API
 
All requests are handled via a custom `fetchClient.ts` wrapper.
 
### Todo Interface
 
```typescript
interface Todo {
  id: number;
  userId: number;
  title: string;
  completed: boolean;
}
```
 
### Endpoints Used
 
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/todos?userId={id}` | Fetch user's todos |
| `POST` | `/todos` | Create a new todo |
| `DELETE` | `/todos/{id}` | Delete a todo |
| `PATCH` | `/todos/{id}` | Update title or status |
 
---
 
## ⚙️ Getting Started
 
### 1. Clone the repository
 
```bash
git clone https://github.com/Tysiachnyk/TODO-App.git
cd TODO-App
```
 
### 2. Install dependencies
 
```bash
npm install
```
 
### 3. Set your User ID
 
Open `src/utils/api/todos.ts` and replace the placeholder with your registered `userId`:
 
```typescript
const USER_ID = YOUR_USER_ID; // 👈 replace this
```
 
### 4. Start the development server
 
```bash
npm start
```
 
## 🧹 Code Style
 
This project uses **ESLint** and **Prettier** for consistent code formatting. Formatting is applied automatically on save.
 
To run the linter manually:
 
```bash
npm run lint
```
 
---
 
## 📁 Project Structure
 
```
src/
├── components/
│   ├── TodoApp/
│   ├── TodoList/
│   ├── TodoItem/
│   ├── TodoFilter/
│   └── ErrorNotification/
├── utils/
│   └── api/
│       ├── fetchClient.ts
│       └── todos.ts
├── types/
│   └── Todo.ts
└── App.tsx
```