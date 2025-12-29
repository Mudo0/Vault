
```txt
<type>(<scope>): <description>
```

- **Type:** The category of the change (e.g., feature, fix).
- **Scope (Optional):** The specific part of the codebase affected (e.g., `login`, `navbar`, `api`).
- **Description:** A short, imperative summary of what changed.

### 2. Commit Types (Prefixes)

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

Here is how these commits look in a real project:

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

To sound professional and follow the standard, apply these grammatical rules:

1. **Use the Imperative Mood:** Write as if you are giving a command.
    
    - ✅ Correct: `add date filter`
        
    - ❌ Incorrect: `added date filter` or `adding date filter`
        
    - _Tip:_ The message should complete the sentence: _"If applied, this commit will..."_ -> _"add date filter"_.
        
2. **Keep it Short:** Aim for **50 characters** or less for the title. If you need to explain _why_ or _how_, add a body paragraph after a blank line.
    
3. **No Punctuation:** Do not end the title line with a period (`.`).
    

> **Note on Emojis (Gitmoji):** Many teams use emojis to make the history visual.
> 
> - `feat`: ✨ (`:sparkles:`)
>     
> - `fix`: 🐛 (`:bug:`)
>     
> - `docs`: 📝 (`:memo:`)
>     
> - _Example:_ `✨ feat(ui): add dark mode toggle`
>     
