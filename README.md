# Monthly Budget Tracker

A single-file, password-protected budget web app ([index.html](index.html)). Tracks actual
spend vs. monthly budget against gross/net payroll, with a built-in tax estimator for the
US (federal + all 50 states + DC), Canada (federal + all provinces/territories), and the
UK (rUK + Scottish rates), plus a manual-rate option for anywhere else.

## Features

- **Password protected** — on first visit you set a password; all budget data is encrypted
  with AES-256-GCM (key derived via PBKDF2, 210k iterations) and stored only in the
  browser's localStorage. The hosted site contains no personal data.
- **Income & Taxes** — annual salary, currency, pay frequency (weekly → annual), country
  and state/province. Shows a full gross → net breakdown (income tax, state/provincial
  tax, Social Security/CPP/EI/National Insurance) and per-paycheck amounts.
- **Budget** — expense items classified Mandatory/Discretionary with monthly amounts,
  annualized totals, and planned savings vs. net income.
- **Monthly Tracking** — enter actual spend per item per month; variance to budget and
  remaining cash for savings are computed per month (mirrors the original Excel layout).
- **Dashboard** — KPIs, budget-vs-actual chart, category doughnut, monthly + cumulative
  savings chart, and a monthly summary table.
- **Export / Import** — move data between devices/browsers as a JSON file
  (the export file is unencrypted — keep it private).

## Run locally

Just open `index.html` in a browser, or serve it:

```
python -m http.server 8741
```

## Deploy publicly (free options)

The app is one static file, so any static host works:

1. **Netlify Drop** (easiest): go to <https://app.netlify.com/drop> and drag the folder
   containing `index.html` onto the page. You get a public URL immediately.
2. **GitLab Pages**: create a project on gitlab.com and push this folder (it already
   contains the required `.gitlab-ci.yml`). The pipeline publishes the site to
   `https://<username>.gitlab.io/<project>/`. To keep the repo private but the site
   public: Settings → General → Visibility → set **Pages** to "Everyone".
3. **GitHub Pages**: push this folder to a GitHub repo → Settings → Pages → deploy from
   branch. The site will be at `https://<user>.github.io/<repo>/`.
4. **Vercel**: `npx vercel` in this folder, or import the repo at vercel.com.

## Important caveats

- **Data lives in the browser, per device.** Visiting the site from a new device starts
  empty — use Export/Import to move your budget across devices. Clearing browser site
  data deletes the budget.
- **Forgotten password = unrecoverable data.** There is no reset email; the password is
  the encryption key. Keep an exported JSON as a backup.
- **Tax figures are estimates** (2025/26 published rates, single filer, standard
  deduction/basic personal amounts; excludes local/city taxes, benefits, pensions,
  credits). For planning only — not tax advice.
