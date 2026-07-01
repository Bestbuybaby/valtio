```markdown
# valtio Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches the core development patterns and workflows used in the `valtio` TypeScript codebase. It covers coding conventions, dependency upgrade workflows, and testing patterns, providing practical examples and command references to streamline contributions and maintenance.

## Coding Conventions

### File Naming
- Use **camelCase** for file names.
  - Example: `proxyState.ts`, `useSnapshot.ts`

### Import Style
- Use **relative imports** within the codebase.
  - Example:
    ```typescript
    import { getVersion } from './version'
    ```

### Export Style
- Use **named exports** for modules.
  - Example:
    ```typescript
    export function createProxy<T>(obj: T): T { ... }
    export const version = '1.0.0'
    ```

### Commit Messages
- Follow **conventional commit** style.
- Use the `build` prefix for build-related changes.
  - Example:  
    ```
    build: update dependencies in website and examples directories
    ```

## Workflows

### Multi-Directory Dependency Upgrade
**Trigger:** When dependencies need to be upgraded across multiple subdirectories (e.g., examples, website), such as during a Dependabot update or routine maintenance.  
**Command:** `/upgrade-dependencies-multi`

1. **Identify outdated dependencies** in each relevant directory (e.g., `examples/*`, `website/`).
2. **Update dependency versions** in each directory's lockfiles (`yarn.lock`, `pnpm-lock.yaml`) and manifests (`package.json`).
3. **Commit all updated lockfiles and manifests together**, ideally with a detailed changelog in the commit message.

**Files Involved:**
- `examples/*/yarn.lock`
- `website/package.json`
- `website/pnpm-lock.yaml`

**Example Commit Message:**
```
build: upgrade dependencies in website and all examples
- Updated react to 18.2.0 in website
- Updated zustand in examples/todo
- Refreshed lockfiles
```

## Testing Patterns

- Test files use the `*.test.*` naming convention (e.g., `proxy.test.ts`).
- The specific testing framework is **unknown**, but typical patterns suggest usage of Jest or similar.
- Example test file:
  ```typescript
  // proxy.test.ts
  import { createProxy } from './proxyState'

  test('should create a proxy object', () => {
    const obj = { count: 0 }
    const proxy = createProxy(obj)
    expect(proxy.count).toBe(0)
  })
  ```

## Commands

| Command                   | Purpose                                                        |
|---------------------------|----------------------------------------------------------------|
| /upgrade-dependencies-multi | Upgrade dependencies and lockfiles across multiple directories |

```