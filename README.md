# kindle-rss-feed

Automatically converts your RSS feeds to an EPUB and delivers it to your Kindle on a schedule — powered by [KindleRSS](https://github.com/ekarlsn/KindleRSS).

## Setup

### 1. Create your repository

Click **"Use this template"** → **"Create a new repository"** at the top of this page.

### 2. Add your RSS feeds

Edit `config.yaml` to add your feeds:

```yaml
Settings:
  max_history: 7    # Include articles from the last N days
  load_images: true # Download and embed images

Feeds:
  - url: "https://example.com/feed.xml"
    title: "Example Blog"

  - url: "https://another-blog.com/rss"
    title: "Another Blog"
```

### 3. Add GitHub Secrets

Go to **Settings → Secrets and variables → Actions → Secrets** and add:

| Secret | Description |
|---|---|
| `SMTP_SERVER` | SMTP server address (e.g. `smtp.gmail.com`) |
| `SMTP_PORT` | SMTP port (e.g. `587`) |
| `SENDER_EMAIL` | Your sender email address |
| `SENDER_PASSWORD` | App password for your email account |
| `KINDLE_EMAIL` | Your Kindle's email address (e.g. `yourname@kindle.com`) |

### 4. Whitelist your sender email on Kindle

1. Go to [Manage Your Content and Devices](https://www.amazon.com/mn/dcw/myx.html)
2. **Preferences** → **Personal Document Settings**
3. Find your Kindle email address under *Send-to-Kindle E-Mail Settings*
4. Under **Approved Personal Document E-mail List**, add your `SENDER_EMAIL`

That's it — the workflow will now run automatically on the configured schedule.

---

## Schedule

The default schedule is **every Friday at 1 AM UTC**. To change it, edit the `cron` line in `.github/workflows/rss_to_kindle.yml`:

```yaml
on:
  schedule:
    - cron: "0 1 * * 5"  # minute hour day month weekday
  workflow_dispatch:      # also allows manual runs from the Actions tab
```

You can also trigger a run manually from the **Actions** tab at any time.

---

## Advanced configuration

For full documentation — CSS selector extraction, per-feed options, custom filename templates, and more — see the [KindleRSS docs](https://github.com/ekarlsn/KindleRSS).

### Gmail tip

Gmail requires an [App Password](https://support.google.com/accounts/answer/185833) (not your regular password). Enable 2-Factor Authentication first, then generate one under **Security → App passwords**.