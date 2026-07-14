# wadv-frontend

React 19 + Vite 8 + Tailwind CSS 3 SPA. Task manager frontend with real-time sync.

## Commands

| Command | Purpose |
|---------|---------|
| `npm run dev` | Start Vite dev server (port 5173) |
| `npm run build` | Production build to `dist/` |
| `npm run preview` | Preview built app |
| `npm run lint` | ESLint (flat config, `eslint.config.js`) |

No test, typecheck, or format commands configured.

## API & Proxy

- `vite.config.js` proxies `/api` and `/auth` → `http://localhost:3000`
- Axios base URL is `/api/v1` (see `src/lib/axios.js:5`)
- Backend must be running at `localhost:3000` before `npm run dev`

## Auth

- Access token stored in-memory (`_accessToken` var), refresh token in `sessionStorage("rf_token")`
- Axios response interceptor auto-refreshes on 401 (queues concurrent retries)
- On refresh failure: clears tokens, redirects to `/login`
- No `.env` needed — proxy handles URL config

## Real-time (Socket.IO)

- Socket connects to `http://localhost:3000` with token in `auth` option
- Events consumed in `useRealTimeTasks` hook: `task:created`, `task:updated`, `task:deleted`, `notification`
- Event namespaces used: `users:online`, `task:*`, `notification`

## Project structure

```
src/
├── components/    # Navbar, TaskCard, TaskForm, ProtectedRoute, ToastContainer
├── contexts/      # AuthContext, SocketContext, NotifContext (toast)
├── hooks/         # useRealTimeTasks
├── lib/           # axios.js (interceptors), tokenStore.js
├── pages/         # LoginPage, RegisterPage, TasksPage, ProfilePage
├── services/      # task.service.js (CRUD)
└── App.jsx        # Router
```

## Style / UI conventions

- Tailwind CSS v3 with custom `primary` color palette (`src/index.css` for `@tailwind` directives)
- Glassmorphism: `glass` class used in Navbar (defined in `index.css`)
- Toast notifications via `NotifContext` + `ToastContainer` (bottom-right, 4s auto-dismiss)
- Status values: `TODO`, `IN_PROGRESS`, `DONE`
- Priority values: `LOW`, `MEDIUM`, `HIGH`
- TaskCard has priority-colored top border strip (`h-1`)
- Forms use `react-hook-form` with modal overlay pattern (`TaskForm`)
- Indonesian locale for dates (`id-ID`)
- No TypeScript — plain JSX files

## Key notes

- `TokenStore` uses in-memory access token + `sessionStorage` refresh token — **not** localStorage
- `ProtectedRoute` checks `loading` state before redirecting; must handle correctly
- Task list fetches via `useCallback` + `useEffect` pattern; real-time socket updates merge into same `tasks` state
- `dist/` and `node_modules/` are gitignored
