# MAHAMUD EFX Korean Study Master v3 Upgrade

This package keeps the existing single-page Korean Study Master and adds:

- Username + email + password registration
- Case-insensitive unique usernames
- Username or email login
- Forgot-password email reset
- Per-exam countdown timers with automatic submission
- Online exam result/points sync
- Personal profile with rank, points, exam history and average score
- Global leaderboard
- Admin dashboard
- Korean image OCR translation fallback

## 1. Create Supabase project

Create a free Supabase project.

## 2. Create database

Open Supabase SQL Editor and run `supabase-schema.sql` completely.

## 3. Configure Auth

In Supabase Authentication settings:

- Add `https://mahamudefx.xyz` as the Site URL.
- Add `https://mahamudefx.xyz/**` as an allowed redirect URL.
- If you want users to enter the site immediately after registration, disable mandatory email confirmation. Password reset still uses email.

## 4. Put Supabase browser credentials in the website

Open `supabase-config.js` and replace:

- `YOUR_SUPABASE_PROJECT_URL`
- `YOUR_SUPABASE_PUBLISHABLE_KEY`

Use only the browser-safe Publishable/anon key. Never put a `sb_secret_...` or service-role key in a GitHub Pages file.

## 5. Make yourself Admin

Register your own account first. Then in Supabase SQL Editor run:

```sql
update public.profiles
set role='admin'
where username_normalized='mahamud';
```

Replace `mahamud` with your actual username if different.

## 6. What appears after login

After a successful login, the top toolbar shows **Profile**, **Leaderboard**, **Admin** (admin accounts only), the current username, and **Logout**. Profile shows rank, points, exam count, average score and recent results.

## 7. GitHub Pages

Upload the updated `index.html` and `supabase-config.js` together with the existing project files. Keep the same custom domain `mahamudefx.xyz`.

## Timer mapping

1-4 Vocabulary Section 1-4: 10 minutes each
5-8 Wrong Vocabulary: no timer
9 Native Korean: 5 minutes
10 Sino Korean: 5 minutes
11 Mixed Number: 5 minutes
12 Digital Clock: 5 minutes
13 Analog Clock: 5 minutes
14 Week: 5 minutes
15 Month: 5 minutes
16 Date: 10 minutes
17 Word Listening: 10 minutes
18 Native Number Listening: 5 minutes
19 Sino Number Listening: 5 minutes
20 Clock Listening: 5 minutes
21 Synonym + Antonym: 5 minutes
22 Grammar Practice: no timer
23 Grammar Exam: 5 minutes
24 Wrong Grammar: no timer
25 Mixed 25: 5 minutes
26 Mixed 50: 10 minutes
27 Mixed 75: 15 minutes
28 Mixed 100: 20 minutes

## Security notes

Passwords are handled by Supabase Auth and are never displayed to the Admin dashboard. The browser only uses the publishable/anon key. A secret/service-role key must never be exposed in this static GitHub Pages app.

The image translator first checks the local Korean vocabulary, then tries normalized matching, then uses a MyMemory Korean-to-Bengali fallback for short detected terms. MyMemory's API documentation describes the GET translation endpoint and UTF-8 query support.
