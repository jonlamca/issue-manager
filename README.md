# Issue Manager

A static GitLab dashboard on one page. Each milestone gets a column, and you drag issues between columns to assign them. Works for a group or a project, and signs you in with GitLab SSO (OAuth + PKCE, no backend).

## Setup

1. In GitLab, go to **User settings → Applications** (or the group's **Settings → Applications**) and add an application:
   - Redirect URI: the exact Pages URL, e.g. `https://<namespace>.gitlab.io/<project>/`
   - Confidential: **off**
   - Scope: `api`
2. Set `CLIENT_ID` (and `GITLAB` if you self-host) at the top of `public/index.html`.
3. Push this repo to GitLab. `.gitlab-ci.yml` publishes `public/` to Pages.

## Use

- Pick a group or project. Columns are its active milestones (plus inherited ones), "No milestone", and any closed milestone that still has open issues.
- Tick several cards, then drag one of them (or click **Move selected here**) to move them all.
- Set due dates and close or reopen milestones from the column header, and use **+ Milestone** to create one.
- Open `index.html#selftest` to check the PKCE encoding.
