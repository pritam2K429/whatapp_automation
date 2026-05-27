# WACRM

Private WhatsApp CRM for managing conversations, contacts, pipelines, broadcasts, templates, and no-code automations.

## Live App

Production is deployed on Vercel:

```text
https://wacrm-orcin.vercel.app
```

WhatsApp webhook callback URL:

```text
https://wacrm-orcin.vercel.app/api/whatsapp/webhook
```

## Stack

- Next.js 16 App Router
- React 19
- TypeScript
- Tailwind CSS
- Supabase Auth, Postgres, Storage, and Realtime
- Meta WhatsApp Cloud API
- Vercel hosting

## Features

- Shared WhatsApp inbox
- Contacts, tags, and custom fields
- Sales pipelines
- Broadcast campaigns with template messages
- WhatsApp message status tracking
- No-code automations and flows
- Dashboard metrics
- Supabase row-level security
- HMAC-verified WhatsApp webhooks
- Encrypted WhatsApp access token storage

## Local Development

Install dependencies:

```bash
npm install
```

Create a local environment file:

```bash
cp .env.local.example .env.local
```

Fill in the required values:

```env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
ENCRYPTION_KEY=
META_APP_SECRET=
NEXT_PUBLIC_SITE_URL=
```

Run locally:

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

## Production Deployment

The app is deployed as a single Next.js project. Frontend pages and backend API routes are deployed together on Vercel.

Vercel settings:

```text
Framework: Next.js
Install Command: npm install
Build Command: npm run build
Output Directory: default
Node.js: 20 or newer
```

Required production environment variables:

```env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
ENCRYPTION_KEY=
META_APP_SECRET=
NEXT_PUBLIC_SITE_URL=https://wacrm-orcin.vercel.app
```

Optional environment variable for scheduled automation endpoints:

```env
AUTOMATION_CRON_SECRET=
```

## Supabase

Apply the SQL migrations in:

```text
supabase/migrations
```

The production Supabase project must have all migrations applied before using the CRM with real WhatsApp traffic.

## WhatsApp Setup

In Meta for Developers, configure the webhook callback URL:

```text
https://wacrm-orcin.vercel.app/api/whatsapp/webhook
```

Then open the deployed CRM settings page and save:

- WhatsApp access token
- WABA ID
- Phone number ID
- Webhook verify token

The verify token in Meta must match the verify token saved in the CRM.

## Cron Notes

The app includes cron endpoints for delayed automations and flow cleanup:

```text
/api/automations/cron
/api/flows/cron
```

These endpoints require `AUTOMATION_CRON_SECRET` through the `x-cron-secret` header. Vercel Hobby cron is limited, so frequent automation scheduling may require Vercel Pro or an external cron service.

## Scripts

```bash
npm run dev
npm run build
npm run start
npm run lint
npm run typecheck
npm run test
```

## Ownership

This repository is intended to be privately owned and maintained by the project owner only.
