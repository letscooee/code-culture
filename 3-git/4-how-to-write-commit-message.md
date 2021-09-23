# How to write commit messages

In order to create a useful revision history, teams should first agree on a commit message convention.

## 1. General

A commit message must be clear and meaningful and explain what changes you have made and why you made them.

1. Capitalize the message and each paragraph.
2. Commit message must use proper English and Grammar.
3. Do not end the subject line with a period.
4. Do not assume the reviewer understands what the original problem was.
5. Do not assume the code is self-evident/self-documenting.
6. Describe any limitations of the current code.

     :white_check_mark:   |   :x:
   -----------------------|----------
   Fix in forgot password endpoint | fix in forgot password endpoint
   Update in login page based on review | Some review changes.
   Fix in forgot password endpoint | Some fixes
   Update in login page UI based on review | Review changes

## 2. Subject/Title/Header

This used to be the first line of the commit. Must be short (50 chars or less). This first commit line is the most 
important.

## 3. Body (optional)

Commits can have body i.e. a more detailed explanatory text, if necessary. If you add a commit body then a blank 
line must separate it from the subject.

## 4. Footer (optional)

Commits can also have footer which can be used to reference issues affected by this code change. For example-
`Fixes #1108`

## 5. Jira or Issue Reference

Commit title/subject must end with the Jira ticket number or the repository's issue number.
   
**Examples:**

- `Fix the forgot password endpoint COO-11` 
- `Update the home page UI KIDS-2105`.
- `Change in the login page UI #1108`

## 6. Commit Types

Commit message should begin with a type of commit-

| Commit Type | Description                                                                                                 | Emoji |
|:-----------:|-------------------------------------------------------------------------------------------------------------|:-----:|
|   `feat`    | A new feature                                                                                               |  ✨   |
|    `fix`    | A bug Fix                                                                                                   |  🐛   |
|   `docs`    | Documentation only changes                                                                                  |  📚   |
|   `style`   | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)      |  💎   |
| `refactor`  | A code change that neither fixes a bug nor adds a feature                                                   |  📦   |
|   `perf`    | A code change that improves performance                                                                     |  🚀   |
|   `test`    | Adding missing tests or correcting existing tests                                                           |  🚨   |
|   `build`   | Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)         |  🛠   |
|    `ci`     | Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack)            |  ⚙️   |
|   `chore`   | Other changes that don't modify src or test files                                                           |  ♻️   |
|  `revert`   | Reverts a previous commit                                                                                   |  🗑   |

(Referenced from- https://github.com/pvdlg/conventional-changelog-metahub/tree/v4.0.1#commit-types)

**Examples:**

- `fix: Forgot password endpoint for sending OTP COO-11`
- `feat: Auto cleaning of expired OTP KIDS-1105`
- `refactor: Separate reference & rename capabilities #401108`
- `build: Update Angular dependencies to latest CUR-4567`
- `docs: Steps to update database for local development`

## 7. Scope

A scope is provided in parentheses after the commit type. A scope is a phrase describing parts of the code affected 
by the changes.

- `fix(customer-module): Forgot password endpoint for sending OTP COO-11`
- `refactor(common): Separate reference & rename capabilities #401108`

## 8. Imperative mood while writing messages

Your commit message should be in imperative mood. For example: `fix: Change xyz to do foo-bar` instead of
`fix: Changed xyz to do foo-bar` as if you are giving orders to the codebase to change its behaviour. A few examples 
of commit messages written in imperative mood-

- `chore: Add .gitignore`
- `fix: Fix forgot password link`
- `Merge branch xyz into abc`
- `test: Remove unneeded tests`
- `docs: Add steps to update database for local development`

**Git itself uses the imperative whenever it creates a commit on your behalf. For example:**

- When you merge a branch- `Merge branch 'foo'`.
- When you revert a commit- `Revert 'Fix the forgot password endpoint'`

## Examples-

In general, 
```
<type>: <subject> <optional ticket#>

[optional body]

[optional footer]
```

A readable quick example-

```
Capitalized, short (50 chars or less) summary

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the
two together.

Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
or "Fixes bug."  This convention matches up with commit messages generated
by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too
- Typically a hyphen or asterisk is used for the bullet, followed by a
  single space, with blank lines in between, but conventions vary here
- Use a hanging indent

If you use an issue tracker, add a reference(s) to them at the bottom,
like so:

Resolves: #123
```

A typical full example can be-

```
(feat): Implement login endpoint FOO-1108

The login API will allow user to generate an access token by passing the username &
password as JSON body. This is a POST endpoint and is available at /v1/login.

Upon successful authentication, this endpoint will return 200 status code along with
the access token in the JSON response. This endpoint will return error with non 20x
status code for wrong credentials.

Required POST parameters (in JSON)-

- username
- password
- source

Endpoint must not be called more than thrice with the wrong credential within a minute.

Resolves: FOO-1108
```

## Few References

Following are a few referenced used to pick & decide this culture document of git commits-

- https://chris.beams.io/posts/git-commit/#end
- https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53
- https://www.freecodecamp.org/news/writing-good-commit-messages-a-practical-guide/
- https://hashnode.com/post/which-commit-message-convention-do-you-use-at-work-ck3e4jbdd00zyo4s1h7mc7e0g