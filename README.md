# MADE Funnel · Landing Page

Single-file landing page for the MADE digital marketing course by AM Agency.

---

## Placeholders to replace before deploy

Open `index.html` and search for each placeholder listed below. Every occurrence is also marked with a `<!-- PLACEHOLDER -->` comment nearby.

| Placeholder | Where | What to put |
|---|---|---|
| `[META_PIXEL_ID]` | `<head>` (×2) | Your Facebook / Meta Pixel numeric ID (e.g. `123456789012345`) |
| `[CALENDLY_URL]` | CTA section `<a href>` | Full Calendly booking URL (e.g. `https://calendly.com/yourname/30min`) |
| `[WHATSAPP_NUMBER]` | CTA section `<a href>` | WhatsApp number in international format, digits only (e.g. `34612345678` for Spain) |

> **YouTube video** is already set to ID `JngUUg487ig`. To change it, update `var YT_VIDEO_ID` in the `<script>` block.
>
> **Supabase** credentials are already embedded. If you ever rotate the key, update `SUPABASE_URL` and `SUPABASE_KEY` in the same script block.

---

## Deploy to Vercel

### One-time setup

```bash
npm i -g vercel   # install Vercel CLI globally (skip if already installed)
```

### Deploy

```bash
# from the made-funnel/ directory:
vercel --prod
```

Vercel will detect a static site automatically (no framework). The output URL is your live page.

### Custom domain (optional)

```bash
vercel domains add yourdomain.com
```

Then point your domain's DNS to the Vercel nameservers shown in the CLI output.

---

## Verify leads are arriving in Supabase

1. Go to [https://supabase.com](https://supabase.com) and open your project (`zggckdkddbwbkauttvjg`).
2. Navigate to **Table Editor → leads**.
3. Submit a test entry through the landing page form.
4. Refresh the table — you should see a new row with `nombre`, `email`, and `whatsapp` columns populated.

### Query via SQL Editor (optional)

```sql
select * from leads order by id desc limit 20;
```

### If no rows appear

- Open browser DevTools → **Network** tab → filter for `supabase.co`.
- Submit the form and check the POST request to `/rest/v1/leads`.
- A `201 Created` response means success.
- A `401` or `403` means the API key or table RLS policy needs attention — make sure the `leads` table has an **INSERT** policy for the anon/public role, or that RLS is disabled for testing.

---

## File structure

```
made-funnel/
├── index.html   ← entire landing page (HTML + CSS + JS)
└── README.md    ← this file
```

No build step. No dependencies. Just open `index.html` in a browser or deploy the folder as a static site.
