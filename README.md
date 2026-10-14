# AI Fire Calculator

Mobile-first fire insurance quotation builder using GitHub Pages/Vercel frontend and Supabase PostgreSQL.

## Current build
- Occupancy search against `public.tariff_occupancies`.
- Policy band selector: Sookshma, Laghu, SFSP.
- District/EQ-rate lookup from `public.eq_rate_master`.
- Component-wise Basic, STFI, EQ, Terrorism and Floater breakdown.
- Premium summary, print / Save as PDF, and quotation persistence to `public.fire_quotations`.
- Responsive layout for desktop and mobile.
- Uses the Supabase publishable key only; no service-role key is included in the browser.

## Supabase setup
The current Supabase project has the required tables and row-level security configured for this build:
- `tariff_occupancies`: existing 50 occupancy rows; rows not yet verified are clearly flagged as provisional in the UI.
- `eq_rate_master`: initial 11 rows from the attached workbook (3 named Rajasthan districts plus the workbook's manual industry classifications).
- `fire_quotations`: new table for saved quotation snapshots; public clients can insert, but cannot read back other customers' quotations.

The workbook contains a larger tariff master than the 50 rows currently in Supabase. Import the complete `Tarrif` sheet and all `EQ` rows, including TAC codes, before using this for production quotes. The VBA rules for Pro Rata, Short Period, and Floater should be fully ported and checked against Excel outputs before binding quotes. The current interface labels tenure as provisional and must not be treated as final tariff automation.

## Deploy to Vercel
1. Open [Vercel](https://vercel.com/) and sign in with GitHub.
2. Select **Add New → Project**.
3. Import repository `Arunsonly/AI-Fire-Calculator-`.
4. Keep Framework Preset as **Other**. No build command or output directory is needed for this static `index.html` app.
5. Click **Deploy**. Vercel will provide a `*.vercel.app` URL.
6. For future updates, commit changes to the `main` branch on GitHub; Vercel will redeploy automatically.
7. Test occupancy search, calculation, save quotation, and print on the deployed URL.

## Calculation cautions
- Premium components use the displayed per-mille rate formula: sum insured × rate ÷ 1,000.
- Basic discount is applied only to Basic.
- GST is currently displayed at 18% of net premium.
- Missing optional cover rates block calculation unless an explicit override is entered.
- The current tariff master is not complete and some records require source verification. Do not issue a binding quote until tariff data and the Excel macro's period/floater rules have been validated.

## Security
Only the Supabase publishable key is used in the frontend. Never expose the Supabase service-role/secret key in GitHub or browser code. The public insert policy on `fire_quotations` is intended for quote submissions; add authentication, rate limiting, and an admin workflow before broad public use.
