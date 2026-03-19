# CONVENTIONS — {PROJECT_NAME}

> Coding standards cho dự án. AI PHẢI tuân thủ MỌI quy tắc trong file này.
> Template: APEX v6.0

---

## Code Style

- **Language:** TypeScript strict mode
- **Formatter:** Prettier (config: `.prettierrc`)
- **Linter:** ESLint + `@typescript-eslint`
- **Import order:** Framework → External → Internal → Types → Styles
- **No `any`:** Dùng `unknown` + type guard thay vì `any`

## Naming

| Loại | Quy tắc | Ví dụ |
|---|---|---|
| Components | PascalCase | `UserProfile.tsx` |
| Files/modules | camelCase | `formatDate.ts` |
| Constants | SCREAMING_SNAKE | `MAX_RETRY_COUNT` |
| CSS classes | BEM | `block__element--modifier` |
| DB tables | snake_case (số ít) | `user_profile` |
| API endpoints | kebab-case | `/api/user-profile` |
| Env vars | SCREAMING_SNAKE | `DATABASE_URL` |

## Architecture Patterns

- **State management:** {pattern — e.g., Zustand stores in src/stores/}
- **API layer:** {pattern — e.g., React Query hooks in src/hooks/}
- **Components:** {pattern — e.g., Atomic Design (atoms/molecules/organisms)}
- **Error handling:** {pattern — e.g., Custom Error classes in src/errors/}
- **Logging:** {pattern — e.g., Winston logger in src/lib/logger.ts}

## Git

- **Branch strategy:**
  - `main` — production, protected
  - `develop` — integration branch
  - `feature/{desc}` — new features
  - `fix/{desc}` — bug fixes
  - `hotfix/{desc}` — production emergency
- **Commit format:** Conventional Commits
  - `feat(scope): mô tả` — feature mới
  - `fix(scope): mô tả` — bug fix
  - `chore(scope): mô tả` — maintenance
  - `perf(scope): mô tả` — performance
  - `test(scope): mô tả` — tests
  - `sec(scope): mô tả` — security
- **PR rules:** {e.g., must pass CI + 1 review}
- **Merge strategy:** {e.g., squash merge vào develop}

## Testing

- **Unit test:** {framework — e.g., Vitest + React Testing Library}
- **E2E test:** {framework — e.g., Playwright}
- **Coverage target:** ≥80% cho code mới
- **Test file location:** Cùng folder với source (`.test.ts` suffix)
- **Naming:** `describe('ClassName/functionName')` → `it('should ...')`

## Security

- **Không commit secrets** — dùng `.env` + `.env.example`
- **Input validation** — validate MỌI user input
- **SQL injection** — dùng parameterized queries ONLY
- **XSS** — escape output, dùng framework built-in protection
- **Auth** — {pattern — e.g., JWT + httpOnly cookies}
- **CORS** — whitelist domains, không dùng `*`

## File Organization

```
src/
├── {layer-1}/           ← e.g., modules, features, pages
├── {layer-2}/           ← e.g., shared, common, lib
├── {layer-3}/           ← e.g., config, types, constants
└── index.ts             ← Entry point
```

> **Rule:** Import chỉ được đi **1 chiều**: layer-1 → layer-2 → layer-3. Không import ngược.
