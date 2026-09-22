# Mohammad Umar Sikandri — Portfolio (self-hosted, self-editable)

This is a single-page site (`index.html`) with a free backend (Supabase) so you can:
- Add / edit / delete certificates (with a description and an optional image), without touching code
- Update your coding stats (Codolio numbers) any time, without touching code
- Only **you** can sign in and make changes — everyone else just sees the public site

Everything below is free. No credit card needed anywhere.

---

## Part 1 — Create your free Supabase backend (~10 minutes)

1. Go to https://supabase.com → **Start your project** → sign up (free, no card).
2. Click **New project**. Pick any name (e.g. `portfolio`), set a database password (save it somewhere), pick the region closest to India, and create it. Wait ~2 minutes for it to spin up.
3. In the left sidebar, open **SQL Editor** → **New query**. Open the `supabase-schema.sql` file from this folder, paste its entire contents in, and click **Run**. This creates your `certificates` table, `stats` table, and image storage bucket, with the right permissions already set up.
4. Go to **Authentication → Providers → Email**, and turn **off** "Allow new users to sign up" (so nobody else can ever create an account on your site).
5. Go to **Authentication → Users → Add user**, and create the one account you'll use to log in and edit the site — your email + a password you'll remember. This is the *only* login the site will ever have.
6. Go to **Project Settings → API**. Copy two values:
   - **Project URL** (looks like `https://xxxxx.supabase.co`)
   - **anon public** key (a long string)

   These are both safe to put directly in your public site code — they don't grant write access on their own; the database rules (from the SQL script) only allow writes from someone who's actually logged in as you.

---

## Part 2 — Connect the site to your backend

1. Open `index.html` in a text editor.
2. Find this block near the bottom (search for `SUPABASE_URL`):
   ```js
   var SUPABASE_URL = "YOUR_SUPABASE_PROJECT_URL";
   var SUPABASE_ANON_KEY = "YOUR_SUPABASE_ANON_KEY";
   ```
3. Replace the two placeholder strings with the Project URL and anon key you copied in Part 1. Save the file.

That's it — the certificates and stats sections will now load live from your database, and the 👤 icon in the top-right lets you sign in.

---

## Part 3 — Put it online for free

**Easiest option — Vercel:**
1. Go to https://vercel.com → sign up free with GitHub.
2. Create a new GitHub repo (e.g. `my-portfolio`), upload `index.html` to it.
3. In Vercel, click **Add New → Project**, pick that repo, leave all settings default, click **Deploy**.
4. You'll get a free link like `my-portfolio.vercel.app` — share that.

**Alternative — GitHub Pages (also free):**
1. Create a GitHub repo, upload `index.html`, rename it to `index.html` in the repo root (already named that).
2. Go to the repo's **Settings → Pages**, set source to your main branch, save.
3. Your site will be live at `https://yourusername.github.io/my-portfolio`.

Either way, works forever for free on the free tier — no card needed.

---

## How to use it day to day

- Visit your live site, click the **👤** icon top-right, sign in with the email/password from Part 1, step 5.
- The certifications section will now show a green **"+ Add certificate"** bar — click it, fill in title/issuer/date/description, optionally attach an image or a verify link, save. It appears instantly for every visitor.
- Click **✎** on any certificate card to edit it, or **🗑** to delete it.
- In the coding-stats section, click **"Update stats"** to paste your latest Codolio numbers (questions solved, streaks, difficulty split, topics). Saves instantly for every visitor.
- Click the 👤 icon again to sign out (e.g. on a shared computer).

## Important limitation — please read

There is **no way**, on any free platform, for the site to automatically pull your numbers from Codolio itself. This isn't a limitation of this build specifically — browsers block any website from silently reading another website's private dashboard (a security rule called CORS), and Codolio doesn't offer a public API for this. The "Update stats" form above is the practical free alternative: it takes 30 seconds each time you want to refresh your numbers, and it's saved for good — no code editing required.

## Files in this folder

- `index.html` — the whole site (design, content, and the backend wiring)
- `supabase-schema.sql` — run this once in Supabase to set up your database
- `README.md` — this file
