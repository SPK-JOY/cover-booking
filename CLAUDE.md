# Cover booking page

Cover artist booking page at https://booking.sparkjoy.in.th. The whole site is `index.html` (HTML + CSS + JS). Vercel deploys it: every pull request gets a preview URL, and merging into `main` puts it live.

The people asking for changes are the SparkJoy marketing team, not developers. Reply in Thai, short and friendly, no code unless asked.

## Every change, in this order
1. Start from the latest `main`. Make a new branch.
2. Ask a question if the request is unclear. Otherwise make only the requested change.
3. Commit and open a pull request into `main`. Title in Thai, saying what changed.
4. Wait for the Vercel preview (the Vercel bot comments the URL on the PR), then send the preview link and one line on what changed. Login does not work on preview URLs, so they can only check how the page looks.
5. Merge only when the user clearly says so (e.g. "ขึ้นจริง", "โอเค ปล่อยเลย"). After merging, do not fetch or poll the live site (Vercel's bot check blocks it, so you will wait forever). Tell the user it goes live in about 1 minute and to open https://booking.sparkjoy.in.th to check.

If the live page is broken: open a PR that reverts the last merge, and merge it once the user agrees.

## Free to change
Text, wording, rules shown on the page, colors, fonts, spacing, layout, images/banners (by URL), sections, the order of things, mobile layout. Everything inside `<style>` and the visible HTML.

## Do not change (the page stops working)
Keep this JS logic exactly as it is unless a developer asks:
- `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `createClient(...)`, `blobUrl`.
- Login and logout: `login()`, `signInWithOAuth`, `redirectTo`, `onAuthStateChange`, `signOut`.
- Every `sb.rpc(...)`, `sb.from(...)` and `sb.storage...` call, and the names and arguments they send (`book`, `cancel_booking`, `is_admin`, tables `config`, `artists`, `bookings`, `booking_contacts`, `cancellations`, bucket `artist-images`).
- `load()`, `phase()`, `canCancel()`, `maxPer()` and the booking/cancel handlers.
- Element `id`s and `data-*` attributes that the script uses. If you rename or remove one, update the script too. If you are not sure, keep it.

If a request needs any of these (new booking rule, new field in the form, change to who is admin, new data), do not do it. Say it needs a developer and ask them to message the dev team.

## Data is edited in the page, not here
Artists, images, slots, booking rounds, open/close and cancel times, and the page title are edited in the page's admin tab after Google login. Point the user there instead of editing code.

## Never
- Never push straight to `main` or merge without the user's go-ahead.
- Never add other files, build tools, or frameworks. The site stays one static `index.html`.
- This repo is public: never put passwords, private keys or personal data in it. `SUPABASE_ANON_KEY` is a publishable key and is fine.
