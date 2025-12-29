| **Type**     | **Meaning**   | **When to use it**                                         |
| ------------ | ------------- | ---------------------------------------------------------- |
| **feat**     | Feature       | A new feature for the user.                                |
| **fix**      | Fix           | A bug fix.                                                 |
| **docs**     | Documentation | Documentation only changes (README, comments).             |
| **style**    | Style         | Formatting, missing semi-colons, etc. (no code change).    |
| **refactor** | Refactor      | A code change that neither fixes a bug nor adds a feature. |
| **test**     | Tests         | Adding missing tests or correcting existing tests.         |
| **chore**    | Chores        | Updates to build process, tools, or dependencies.          |
| **perf**     | Performance   | A code change that improves performance.                   |

### 3. Practical Examples

**✨ New Features (`feat`)**
- `feat(auth): add "Forgot Password" button`
- `feat(api): implement product search endpoint`
- `feat: allow users to upload avatars`

**🐛 Bug Fixes (`fix`)**

- `fix(nav): fix menu collapse on mobile devices`
- `fix(cart): prevent negative total in shopping cart`

**📚 Maintenance (`chore`, `docs`, `style`)**

- `chore(deps): upgrade react to version 18`
- `docs: add installation instructions to README`
- `style(home): remove unnecessary whitespace`

**♻️ Code Improvements (`refactor`, `perf`)**

- `refactor(auth): simplify token validation logic`
- `perf(images): implement lazy loading for gallery`

---

### 4. The 3 Golden Rules for Descriptions
1. **Use the Imperative Mood:** Write as if you are giving a command.
    
    - ✅ Correct: `add date filter`
    - ❌ Incorrect: `added date filter` or `adding date filter`
