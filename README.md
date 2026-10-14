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
- **✎** on a card edits its title, description, labels, assignees and due date, or closes the issue.
- **Edit** on a column edits the milestone's title, description, start and due dates. **Close/Reopen** sits next to it, and **+ Milestone** creates one.
- **Labels** lists every label available to the group or project, including inherited group labels, and lets you add or edit them. New labels are created at the level you have loaded.
- Open `index.html#selftest` to check the PKCE encoding.
