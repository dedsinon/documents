# 🎮 AGS — Development Guidelines

> Version 1.0.0 | Maintained by the Engineering Team

---

## Table of Contents

1. Tech Stack
2. Folder Structure
3. Naming Conventions
4. Code Conventions
5. State Management
6. Forms & Validation
7. HTTP Conventions
8. Styling Conventions
9. Branching Strategy
10. Commit Message Format
11. Environment Variables
12. Internationalization
13. Testing

---

## 1. Tech Stack

| Category | Technology | Version | Purpose |
|---|---|---|---|
| Runtime | Next.js | v15 | App framework (App Router) |
| Runtime | React | v19 | UI library |
| Runtime | TypeScript | v5 | Type safety |
| Runtime | Node.js | v22 | JavaScript runtime |
| UI | MUI | v6 | Component library |
| UI | Material Icons | latest | Icon set |
| State | Redux Toolkit | latest | Global state management |
| State | RTK Query | latest | Server state & data fetching |
| Forms | React Hook Form | latest | Form handling |
| Forms | Zod | latest | Schema validation |
| HTTP | Axios | latest | Client-side requests with interceptors |
| HTTP | Native fetch | - | Server-side / Next.js Server Components |
| Realtime | Socket.io | latest | Live features |
| Cache | ioRedis | latest | Redis client (server-side only) |
| Testing | Playwright | latest | E2E testing |
| Error | Sentry | latest | Error tracking |
| PWA | @serwist/next | latest | Service worker / offline support |
| i18n | next-intl | latest | Internationalization |
| Docs | Notion | - | Team documentation |

---

## 2. Folder Structure

```
src/
├── app/                          # Next.js App Router — routing only, no business logic
│   └── [locale]/                 # next-intl locale prefix (e.g. /en, /ph)
│       ├── page.tsx              # Home route
│       ├── (auth)/               # Route group
│       │   ├── login/
│       │   │   └── page.tsx
│       │   └── register/
│       │       └── page.tsx
│       ├── (dashboard)/
│       │   ├── leaderboard/
│       │   │   └── page.tsx
│       │   ├── tournaments/
│       │   │   └── page.tsx
│       │   └── teams/
│       │       └── page.tsx
│       └── api/                  # Route handlers
│
├── features/                     # Feature modules — colocated UI, hooks, types
│   └── <feature>/
│       ├── components/           # UI components for this feature only
│       ├── hooks/                # Hooks scoped to this feature
│       ├── types/                # Types scoped to this feature
│       └── index.ts              # Public API — only export what other features need
│
├── services/                     # RTK Query API endpoints per domain
│   ├── index.ts                  # Base createApi instance (axiosBaseQuery)
│   └── <feature>/index.ts        # Feature endpoints via injectEndpoints
│
├── store/                        # Redux slices — global state only
│   ├── index.ts                  # configureStore — imports all reducers
│   └── <feature>/index.ts        # createSlice for that domain
│
├── schemas/                      # Zod validation schemas per domain
│   └── <feature>/index.ts
│
├── components/                   # Shared UI components used across features
│   ├── ui/                       # Pure UI — no data, no store, props only
│   │   ├── Button/
│   │   ├── Input/
│   │   ├── Badge/
│   │   ├── Modal/
│   │   ├── Avatar/
│   │   └── Card/
│   ├── shared/                   # Data-aware — connected to store/API
│   │   ├── GameCard/
│   │   ├── PlayerAvatar/
│   │   ├── LeaderboardRow/
│   │   └── TournamentCard/
│   └── layout/                   # App shell, navbar, sidebar, footer
│       ├── Navbar/
│       ├── Sidebar/
│       ├── PageWrapper/
│       └── Footer/
│
├── lib/                          # External client and integration setup
│   ├── axios/                    # Axios instance + request/response interceptors
│   ├── socket/                   # socket.io client + connection manager
│   ├── fetch/                    # Server-side native fetch wrapper
│   ├── redis/                    # ioRedis client (server-side only)
│   └── mui/                      # MUI theme, tokens, and SSR registry
│       ├── theme.ts              # darkTheme + lightTheme
│       ├── ThemeRegistry.tsx     # Emotion SSR cache + ThemeProvider
│       ├── colors.ts             # Color tokens
│       ├── gradients.ts          # Gradient presets
│       ├── typography.ts         # Typography scale
│       └── mixins.ts             # Flex helpers + sx mixins
│
├── hooks/                        # Shared custom hooks across features
│
├── types/                        # Global TypeScript types
│   ├── api.ts                    # Response envelopes, pagination, error shapes
│   ├── auth.ts                   # User, session, role types
│   ├── common.ts                 # Nullable, AsyncState, ID primitives
│   └── env.d.ts                  # process.env declarations
│
├── utils/                        # Pure utility functions grouped by concern
│   ├── format/                   # Date, currency, score formatting
│   ├── string/                   # Capitalize, truncate, slugify
│   ├── array/                    # Sort, group, deduplicate
│   ├── object/                   # Pick, omit, deep merge
│   ├── date/                     # Relative time, expiry, UTC
│   ├── storage/                  # localStorage/sessionStorage wrappers
│   ├── auth/                     # Token decode, expiry checks
│   ├── error/                    # Axios/fetch error normalization
│   ├── game/                     # Game-specific helpers
│   ├── validation/               # Lightweight checks outside Zod
│   └── index.ts                  # Root re-export of all utils
│
├── styles/
│   └── common.ts                 # Global reusable sx style constants
│
├── constants/                    # App-wide constant values
├── config/                       # Env-based config and feature flags
└── i18n/
    └── messages/                 # next-intl translation files
        ├── en.json
        └── fil.json
```

---

### Page vs Layout

| File | When to Create |
|---|---|
| `page.tsx` | Every routable URL requires one |
| `layout.tsx` | Only when child routes share UI (sidebar, auth guard, tabs) |

### Services vs Store

| `services/<name>` | `store/<name>` |
|---|---|
| RTK Query API endpoints | Redux slice state and reducers |
| "How do I call the API?" | "What do I store globally?" |
| `injectEndpoints`, `createApi` | `createSlice`, `createReducer` |

### Components — `ui/` vs `shared/`

| | `ui/` | `shared/` |
|---|---|---|
| Data source | Props only | Redux / RTK Query / API |
| Reusability | Anywhere | Across features |
| Example | `Button`, `Input`, `Badge` | `GameCard`, `PlayerAvatar` |
| Has store access | ❌ Never | ✅ Yes |

> **Rule:** Can this component work without knowing anything about the app's data?
> - ✅ Yes → `ui/`
> - ❌ No → `shared/`
> - 🏗️ It's a layout/wrapper → `layout/`

---

## 3. Naming Conventions

### Folders

| Type | Convention | Example |
|---|---|---|
| Domain folders | singular | `services/auth` `features/game` `store/wallet` |
| Collection folders | plural | `components/` `hooks/` `utils/` `types/` |
| Route segments | kebab-case | `game-launcher/` `verify-email/` |
| Dynamic segments | bracketed | `[slug]` `[provider]` `[code]` |
| Component folders | PascalCase | `GameCard/` `Leaderboard/` |

> **Rule:** If the folder represents a domain/resource → singular. If it holds many unrelated things → plural. If it exports a component → PascalCase.

### Files

| Type | Convention | Example |
|---|---|---|
| Components | PascalCase | `LoginForm.tsx` `GameCard.tsx` |
| Hooks | camelCase + `use` prefix | `useAuth.ts` `useGameList.ts` |
| Utilities | camelCase | `formatDate.ts` `slugify.ts` |
| Types | camelCase | `auth.ts` `common.ts` |
| Constants | camelCase file, SCREAMING_SNAKE values | `appConfig.ts` → `APP_NAME` |
| Styles | always `styles.ts` | `features/auth/components/styles.ts` |
| Barrel | always `index.ts` | `features/auth/index.ts` |

### TypeScript

```ts
// Interfaces — PascalCase
interface UserProfile { ... }

// Types — PascalCase
type AuthState = { ... }

// Enums — PascalCase with SCREAMING_SNAKE values
enum GameStatus {
  ACTIVE = 'ACTIVE',
  INACTIVE = 'INACTIVE',
}

// Constants — SCREAMING_SNAKE
const MAX_RETRY_COUNT = 3

// Functions / hooks — camelCase
const formatCurrency = () => { ... }
const useGameLauncher = () => { ... }
```

---

## 4. Code Conventions

### Components

- All pages in `app/` are **Server Components** by default — no MUI, no hooks
- Add `'use client'` only when the component needs interactivity, hooks, or MUI
- Keep pages **thin** — import the feature component, do not add logic in `page.tsx`
- Use functional components only — no class components
- One component per file
- Use named exports for components, default export only for pages

```tsx
// ✅ Correct — page stays thin
// app/[locale]/leaderboard/page.tsx
import { LeaderboardPage } from '@/features/leaderboard'
export default LeaderboardPage

// ❌ Wrong — logic directly in the page file
export default function LeaderboardPage() {
  const [data, setData] = useState([])
  return <Box>...</Box>
}
```

### Imports Order

```ts
// 1. React / Next.js
import { useState } from 'react'
import { useRouter } from 'next/navigation'

// 2. Third-party
import { Box, Typography } from '@mui/material'

// 3. Internal — absolute (@/)
import { useAuth } from '@/hooks'
import { Colors } from '@/lib/mui/colors'

// 4. Feature-local — relative (./)
import { styles } from './styles'
import { loginSchema } from './schemas'
```

### Barrel Files

- Every folder has an `index.ts` with a JSDoc description
- Feature `index.ts` = public API — only export what other features need
- Do not mix Server and Client components in the same barrel

```ts
/**
 * @description Auth feature — login, register, and session management
 */
export { LoginForm } from './components/LoginForm'
export { RegisterForm } from './components/RegisterForm'
```

---

## 5. State Management

### Redux Toolkit Rules

- Use `createSlice` for all state slices
- Use RTK Query (`createApi`) for all API calls — avoid manual fetch in components
- Keep slices small and feature-scoped
- Never mutate state directly outside of a slice reducer

```ts
// store/auth/index.ts
import { createSlice, PayloadAction } from '@reduxjs/toolkit'

interface AuthState {
  user: IUser | null
  isAuthenticated: boolean
}

const initialState: AuthState = {
  user: null,
  isAuthenticated: false,
}

export const authSlice = createSlice({
  name: 'auth',
  initialState,
  reducers: {
    setUser: (state, action: PayloadAction<IUser>) => {
      state.user = action.payload
      state.isAuthenticated = true
    },
    logout: (state) => {
      state.user = null
      state.isAuthenticated = false
    },
  },
})

export const { setUser, logout } = authSlice.actions
export default authSlice.reducer
```

### RTK Query

```ts
// services/game/index.ts
import { baseApi } from '@/services'

export const gameApi = baseApi.injectEndpoints({
  endpoints: (builder) => ({
    getGames: builder.query<TGame[], void>({
      query: () => '/games',
    }),
    getGameById: builder.query<TGame, string>({
      query: (id) => `/games/${id}`,
    }),
  }),
})

export const { useGetGamesQuery, useGetGameByIdQuery } = gameApi
```

---

## 6. Forms & Validation

- Use React Hook Form for all forms — never uncontrolled inputs manually
- Define all validation schemas in `src/schemas/` using Zod
- Use `@hookform/resolvers/zod` to connect Zod with React Hook Form
- Always show field-level error messages

```ts
// schemas/auth/index.ts
import { z } from 'zod'

export const loginSchema = z.object({
  email: z.string().email('Invalid email address'),
  password: z.string().min(8, 'Minimum 8 characters'),
})

export type TLoginForm = z.infer<typeof loginSchema>
```

```tsx
// Usage in component
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { loginSchema, TLoginForm } from '@/schemas/auth'

const { register, handleSubmit, formState: { errors } } = useForm<TLoginForm>({
  resolver: zodResolver(loginSchema),
})
```

---

## 7. HTTP Conventions

### Axios — Client Side

- Create a single Axios instance in `src/lib/axios/`
- Use request interceptors to attach auth tokens
- Use response interceptors to handle 401 / refresh tokens
- Never call `axios` directly in components — always use RTK Query

```ts
// lib/axios/index.ts
import axios from 'axios'

export const axiosInstance = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL,
  timeout: 10000,
})

axiosInstance.interceptors.request.use((config) => {
  const token = localStorage.getItem('token')
  if (token) config.headers.Authorization = `Bearer ${token}`
  return config
})

axiosInstance.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // handle token refresh or redirect to login
    }
    return Promise.reject(error)
  }
)
```

### Native fetch — Server Side

- Use native `fetch` in Server Components and Route Handlers
- Always pass `cache` and `revalidate` options explicitly
- Wrap in `try/catch` and return typed responses

```ts
// ✅ Server-side fetch
const res = await fetch(`${process.env.API_URL}/games`, {
  next: { revalidate: 60 },
})

if (!res.ok) throw new Error('Failed to fetch games')

const data: TGame[] = await res.json()
```

---

## 8. Styling Conventions

- Use `sx` prop for all component styling — no SCSS, no styled-components
- Extract reusable `sx` objects into `styles.ts`
- Type all `sx` constants with `SxProps<Theme>`
- Use design tokens from `@/lib/mui/` — never hardcode hex values in components
- Always use **mobile-first** breakpoints with `breakpoints.up()`

```ts
// features/auth/components/styles.ts
import { SxProps, Theme } from '@mui/material/styles'

export const styles: Record<string, SxProps<Theme>> = {
  wrapper: { display: 'flex', flexDirection: 'column', gap: 2 },
  title: { fontSize: 24, fontWeight: 700, color: 'primary.main' },
}
```

```tsx
// ✅ Use design tokens
import { Colors } from '@/lib/mui/colors'
import { Mixins } from '@/lib/mui/mixins'

<Box sx={{ ...Mixins.flex.rowCenterBetween, background: Colors.background.card }} />

// ❌ Never hardcode hex values
<Box sx={{ display: 'flex', alignItems: 'center', background: '#272727' }} />
```

### Breakpoints — Mobile First

Always use `breakpoints.up()` — start from `xs` and scale up.

```tsx
// ✅ Mobile first
<Box sx={{ fontSize: { xs: 12, mobile: 14, sm: 16, md: 18 } }} />

// ❌ Desktop first
<Box sx={{ fontSize: { xl: 18, lg: 16, md: 14 } }} />
```

### Custom Breakpoints

| Token | Value | Target |
|---|---|---|
| `xs` | 0px | Small phones (base) |
| `mobile` | 480px | Standard/large phones |
| `sm` | 600px | Small tablets |
| `md` | 900px | Tablets |
| `lg` | 1200px | Desktop |
| `xl` | 1536px | Large desktop |

### Flex vs Grid

| Situation | Use |
|---|---|
| Navbar, button groups, centering | Flex / `Stack` |
| Card grids, dashboard sections, multi-column layouts | Grid |

> **Rule:** 1D layout → Flex. 2D layout → Grid.

---

## 9. Branching Strategy

Uses Git Flow with the following branches:

| Branch | Purpose |
|---|---|
| `main` | Production — protected, no direct commits |
| `staging` | Pre-production / QA testing |
| `develop` | Integration branch — all features merge here |
| `feature/<ticket>-<short-desc>` | New features |
| `fix/<ticket>-<short-desc>` | Bug fixes |
| `hotfix/<ticket>-<short-desc>` | Urgent production fixes |
| `chore/<short-desc>` | Deps, config, tooling — no logic changes |
| `release/<version>` | Release preparation |

### Branch Name Examples

```
feature/CGP-101-auth-login
feature/CGP-205-leaderboard-page
fix/CGP-312-token-refresh-loop
hotfix/CGP-401-score-display-error
chore/upgrade-mui-v6
release/1.0.0
```

### Merge Flow

```
feature/* ──► develop ──► staging ──► main
hotfix/*  ──► main (then back-merge to develop)
```

### Rules

- Branch off `develop` for features and fixes
- Branch off `main` for hotfixes only
- Delete branches after merging
- Never commit directly to `main`, `staging`, or `develop`
- `main` and `staging` require at least 1 reviewer approval

---

## 10. Commit Message Format

Follows the [[Conventional Commits](https://www.conventionalcommits.org/)](https://www.conventionalcommits.org/) specification.

### Structure

```
<type>(<scope>): <short description>

[optional body]

[optional footer]
```

### Types

| Type | When to Use |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `chore` | Tooling, deps, config — no logic change |
| `refactor` | Code restructure — no feature or fix |
| `style` | Formatting only — no logic change |
| `test` | Adding or updating tests |
| `docs` | Documentation only |
| `perf` | Performance improvement |
| `ci` | CI/CD pipeline changes |
| `revert` | Revert a previous commit |

### Scope

Use the feature/domain name as scope:

```bash
feat(auth): add OTP login flow
fix(leaderboard): correct score sorting logic
chore(deps): upgrade MUI to v6.1.0
refactor(game): extract game card into shared component
```

### Examples

```bash
feat(auth): add login with OTP support

fix(game-launcher): resolve token expiry on provider handoff

chore(deps): upgrade @reduxjs/toolkit to 2.3.0

refactor(store): split auth slice into session and profile

style(components): apply prettier formatting to shared ui

docs: update README with setup instructions

perf(leaderboard): lazy load player avatars on scroll

feat(auth): implement forgot password via email

BREAKING CHANGE: removed legacy login endpoint, use /auth/signin
```

### Rules

- Use **present tense** — `add` not `added`, `fix` not `fixed`
- Keep the subject line **under 72 characters**
- Reference ticket numbers in the footer when applicable

```bash
feat(tournaments): add bracket generation component

Closes CGP-215
```

---

## 11. Environment Variables

- Never commit `.env` files — only commit `.env.example`
- All variables must be documented in `.env.example` with placeholder values
- Client-side variables must be prefixed with `NEXT_PUBLIC_`
- Secret/server-only variables must **not** have the `NEXT_PUBLIC_` prefix

```bash
# .env.example

# App
NEXT_PUBLIC_APP_NAME=Company Gaming App
NEXT_PUBLIC_API_URL=https://api.example.com
NEXT_PUBLIC_SOCKET_URL=https://socket.example.com

# Server only
API_SECRET_KEY=your_secret_here
DATABASE_URL=postgresql://user:pass@localhost:5432/db
REDIS_URL=redis://localhost:6379
SENTRY_DSN=your_sentry_dsn
```

---

## 12. Internationalization (i18n)

- Use `next-intl` for all user-facing strings — no hardcoded text in components
- Message files live in `src/i18n/messages/`
- Keys use dot notation: `section.subsection.key`
- Default locale is `en` — `fil` (Filipino) as secondary locale

```json
// src/i18n/messages/en.json
{
  "leaderboard": {
    "title": "Leaderboard",
    "rank": "Rank",
    "player": "Player",
    "score": "Score"
  },
  "auth": {
    "login": "Log In",
    "logout": "Log Out",
    "email": "Email",
    "password": "Password"
  }
}
```

```tsx
// Usage in component
import { useTranslations } from 'next-intl'

export const Leaderboard = () => {
  const t = useTranslations('leaderboard')
  return <h1>{t('title')}</h1>
}
```

---

## 13. Testing

### Playwright — E2E

- All critical user flows must have an E2E test
- Tests live in `/tests/e2e/` directory
- Use **Page Object Model** pattern for test organization
- Run tests before merging to `staging`

```ts
// tests/e2e/auth/login.spec.ts
import { test, expect } from '@playwright/test'

test('user can log in', async ({ page }) => {
  await page.goto('/login')
  await page.fill('[name=email]', 'user@company.com')
  await page.fill('[name=password]', 'password123')
  await page.click('[type=submit]')
  await expect(page).toHaveURL('/dashboard')
})
```

---

> This document is maintained by the engineering team.
> Keep it updated as the codebase evolves. 🚀
