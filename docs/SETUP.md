# Running Your Own Instance

This is the public overview of how a Mission Scheduler instance is stood up. The application
repository is private; you receive access to a copy after a conversation
(start here: https://missionscheduler.com).

Every organization runs its **own instance** — nothing is shared between organizations. Your
instance consists of:

1. **A Supabase project** (Postgres database, authentication, file storage, edge functions).
   You create this under your own Supabase account; the schema ships as migrations you apply
   with the Supabase CLI.
2. **An organization seed** — a single SQL file holding your settings: organization name, site
   URL, admin contact, brand colors, timezone. You copy the sample and fill in your values.
3. **Branding** — your logo, login logo, and login background photos, uploaded to your
   instance's storage bucket.
4. **The web app** — a Next.js application. Any Node host works; the reference setup is a small
   Ubuntu VM with nginx and pm2 and an included zero-downtime deploy script.
5. **Notification providers** — your own Twilio account (SMS) and SMTP account (email),
   configured as secrets in your instance. Pilots and passengers are messaged from *your*
   number and address.
6. **Mobile apps** — built from the same codebase with Expo/EAS under your own Apple Developer
   and Google Play accounts, with your own app name and icon.

## What you need before setup

- A Supabase account (free tier is fine to start)
- A domain or subdomain for the web app
- A Twilio account and phone number (for SMS)
- An SMTP/transactional email account
- For the mobile apps: an Apple Developer account and a Google Play Console account
- Somewhere to run a small Node web app (a ~2GB VM is plenty)

## Accounts and roles

Roles are `super_admin`, `admin`, `pilot`, and `patient` (passenger). Admins and pilots sign in
with email/password; passengers use email magic links. Row-level security in the database
enforces who can see and change what — it is not just hidden in the UI.

## Data migration

New organizations start empty. If you are replacing an existing system, the schema is documented
well enough to write an importer; ask in Discussions.

## Getting help

Community support lives in [GitHub Discussions](../../discussions). Post in **Q&A** with what
you tried and what you saw.
