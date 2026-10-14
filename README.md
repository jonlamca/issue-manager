# Issue Manager

A static GitLab dashboard on one page. Each milestone gets a column, and you drag issues between columns to assign them. Works for a group or a project, and signs you in with GitLab SSO (OAuth + PKCE, no backend).

## Setup

1. In GitLab, go to **User settings → Applications** (or the group's **Settings → Applications**) and add an application:
   - Redirect URI: the exact Pages URL, e.g. `https://<namespace>.gitlab.io/<project>/`
   - Confidential: **off**
   - Scope: `api`
2. At the top of `public/index.html`, set:
   - `CLIENT_ID`: the application ID.
   - `GITLAB`: your instance URL if you self-host. Browser SSO needs GitLab 15.1+. On versions before 16.7, the page detects the version and uses the older milestone parameter.
   - `GROUPS` (optional): the groups to manage, e.g. `['my-group', 'other/sub']`. They become the top-level list and copy targets, and startup skips fetching every group you belong to.
3. Push this repo to GitLab. `.gitlab-ci.yml` uses the classic `pages` job with a `public/` artifact, which works on every GitLab version, including pre-17.9 Pages.

## Use

- Start at **All groups**, then drill down: the bar under the header lists the current group's subgroups (📁) and projects, and the breadcrumb takes you back up. A group board covers every project under it.
- **Moving projects:** drag a project button in that bar onto a 📁 subgroup or a breadcrumb group to transfer it there (you'll be asked to confirm).
- **Manage group** lists every project under the group, including archived ones and those in subgroups. Tick projects to **Archive**, **Unarchive** or **Move to…** another group. It also lists empty subgroups (no projects and no subgroups) for **Delete**. Delete the deepest ones first, and their parents become empty in turn.
- You can also type or pick any group or project path. Columns are its active milestones (plus inherited ones), "No milestone", and any closed milestone that still has open issues.
- Tick several cards, then drag one of them (or click **Move selected here**) to move them all.
- **✎** on a card edits its title, description, labels, assignees, start and due dates, or closes the issue. Start dates use GitLab work items through GraphQL; the field is hidden if your instance doesn't support them.
- **Edit selected** on ticked cards adds or removes labels and sets start or due dates across all of them. Blank fields are left unchanged.
- **Edit** on a column edits the milestone's title, description, and start and due dates (both optional). The header shows the period. **Close/Reopen** sits next to it, and **+ Milestone** creates one.
- **Labels** shows one section per level, from the top group down to what you've loaded. Each label is added or edited at its own level, so group labels can be edited from inside a project. **Copy to…** (one label) and **Copy all to…** (a whole level) copy labels into other groups or projects you've loaded or configured. A label that already exists there by name gets its colour and description updated.
- Open `index.html#selftest` to check the PKCE encoding.
