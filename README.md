# Studio MBM Field Reports

Field reports for Studio MBM site meetings. Items are managed on the Items page (level, room, responsible parties, dated updates, photos and markups); reports are built from them and export as letter-size PDFs in the Studio MBM template.

The website is hosted free on **GitHub Pages**. Reports, photos and sign-ins are stored free in **Supabase**.

---

## One-time setup (about 30 minutes)

You need: the Supabase setup script (`Studio_MBM_Field_Reports_Supabase_Setup.txt`), this folder (`index.html`, `config.js`, `README.md`), and the import folder `E10St_import`.

### Part 1: Supabase (database, photo storage, sign-ins)

1. Go to **supabase.com**, sign in, click **New project**.
   Name it `studio-mbm-field-reports`, set a database password (save it), choose the **East US** region, click **Create new project**. Wait about 2 minutes.
2. In the left sidebar open **SQL Editor** → **New query**. Paste the whole setup script and click **Run**. You should see "Success".
3. **Authentication → Sign In / Providers**: turn **off** "Allow new users to sign up". Save.
   *This is what keeps the site private. Only people you add can sign in.*
4. Click **Connect** at the top of your project page (or go to **Project Settings → API Keys**). Copy the **Project URL** and the **Publishable key** (starts with `sb_publishable_`). If you only see an "anon" key under **Legacy API keys**, that works too. You need both values in Part 2.

### Part 2: GitHub (the website)

5. Go to **github.com** and sign in (or create a free account).
6. Click **+** (top right) → **New repository**.
   - Name: `field-reports`
   - Visibility: **Public** (free GitHub Pages needs a public repository; your reports and photos stay private in Supabase).
   - Click **Create repository**.
7. On the new repository page, click **uploading an existing file**. Drag in **index.html**, **config.js** and **README.md**. Click **Commit changes**.
   **Do not upload the `E10St_import` folder.** The repository is public; those photos belong only in Supabase.
8. Click **config.js** in the repository, then the **pencil icon** (Edit). Replace `YOUR-PROJECT-URL` and `YOUR-PUBLISHABLE-KEY` with the two values from step 4. Keep the quote marks. Click **Commit changes**.
9. Go to the repository's **Settings → Pages**. Under "Build and deployment", set **Source: Deploy from a branch**, **Branch: main**, folder **/ (root)**, and click **Save**.
   After 1 to 2 minutes the page shows your site address, like `https://YOUR-GITHUB-NAME.github.io/field-reports/`.

### Part 3: Connect the two and add people

10. Back in Supabase: **Authentication → URL Configuration**. Set **Site URL** to your site address from step 9, add the same address under **Redirect URLs**, and save.
11. **Authentication → Users → Add user → Create new user**. Enter an email and a password, tick **Auto Confirm User**, click **Create user**. Do this for yourself and each colleague, then give each person their password.
    *Alternative: "Send invitation" emails a sign-up link instead, but Supabase's free email service only sends a few emails per hour, so creating users directly is more reliable.*
    Anyone can change their password later with **Forgot password?** on the sign-in screen.

### Part 4: Bring in the E 10 St report

12. Open your site and sign in.
13. Click **Import report** in the top bar (it only appears while the site has no reports).
14. Select **all 10 files** in the `E10St_import` folder (report.json and 9 photos) and click **Import**. The 10/16/2026 report appears with its 10 items, photos, and your Floor Level column.

Done. Send colleagues the site address.

---

## Updating to version 2 (Items page)

1. Supabase → **SQL Editor → New query**: paste `Studio_MBM_Field_Reports_Update_v2.txt` and click **Run**.
2. GitHub: upload the new `index.html` (**Add file → Upload files → Commit changes**). Leave `config.js` as is.
3. Open the site and click **Move items now** on the blue banner. Your items move to the Items page; the old reports are kept.

## Day to day

- **Items page (the workspace):** add, edit and delete items here. Pick a project at the top. Change Level, Room or Status right in the list, or click an item to open it.
- **An item** has a heading, Level, Room, one or more responsible parties, a description, dated updates/responses, photos and markups, and editable dates (created, last updated, closed). Text can be bold, italic, underlined, colored or highlighted.
- **Status** is Open or Closed. A closed item shows once as CLOSED in the next report, then drops off.
- **Columns:** drag a column edge to resize (double-click to reset), click a header to sort.
- **Project settings** (Items page, project selected): levels, rooms, responsible parties, extra columns and the project number. **Import from Excel** reads the template workbook (sheets "Room Schedule" and "Responsible Parties").
- **Reports:** Reports tab → **New report** → pick the project, report date and site meeting date. It shows that project's open items on the site meeting date, plus items closed since the previous report. Reports are live: editing an item updates every report it appears in (updates and photos dated after a report's site meeting don't show in that report). Hover an item in a report and click **Hide** to leave it out of that one report.
- **PDF:** open a report and click **Download PDF**. It's letter size and matches the report view.

## Things to know about the free plans

- **Supabase free plan:** 1 GB of photo storage (roughly 2,000–3,000 site photos at the size the app saves them) and a 500 MB database (reports barely use any).
- **Pausing:** Supabase pauses free projects after 1 week with no activity. If the site stops loading after a quiet stretch, sign in to supabase.com, open the project and click **Restore**. Nothing is lost.
- **Updating the app later:** replace `index.html` in the GitHub repository with the new version (upload it again and commit). Leave `config.js` as is.
- **The old Claude version** of this tool doesn't sync with this site. Use the GitHub site only.
