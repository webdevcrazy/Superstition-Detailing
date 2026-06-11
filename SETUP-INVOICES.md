# Invoice System — 5-Minute Supabase Setup

The invoice builder lives at **superstitiondetailing.com/buildinvoice** (team login required)
and produces shareable links like **superstitiondetailing.com/invoice/192012**.

## 1. Create the tables

In your Supabase dashboard: **SQL Editor → New query**, paste ALL of this, hit Run:

```sql
create table billers (
  id uuid primary key default gen_random_uuid(),
  display_name text not null,
  check_payee text,
  zelle text,
  created_at timestamptz default now()
);

create table customers (
  id uuid primary key default gen_random_uuid(),
  name text not null,
  phone text, email text, address text,
  created_at timestamptz default now()
);

create table invoices (
  id text primary key,
  issued_date date,
  biller jsonb, customer jsonb, items jsonb,
  discount numeric default 0,
  water_credit numeric default 0,
  payment_methods jsonb,
  template text default 'color',
  notes text,
  status text default 'unpaid',
  created_at timestamptz default now()
);

alter table billers enable row level security;
alter table customers enable row level security;
alter table invoices enable row level security;

-- team (logged in) can do everything
create policy "team all billers"   on billers   for all to authenticated using (true) with check (true);
create policy "team all customers" on customers for all to authenticated using (true) with check (true);
create policy "team all invoices"  on invoices  for all to authenticated using (true) with check (true);

-- anyone with a link can VIEW an invoice (needed for customer links)
create policy "public read invoices" on invoices for select to anon using (true);
```

## 2. Create your team login

Dashboard → **Authentication → Users → Add user** → enter your email + a strong password
(check "Auto confirm user"). This is what you'll sign into /buildinvoice with.

## 3. Connect the site

Open **invoice-config.js** and paste in your values from
**Project Settings → API**: the Project URL and the `anon` `public` key. Commit it.

## 4. Done

- Build invoices at **/buildinvoice**
- Customers/billers/invoices all save to Supabase
- Each saved invoice gets a link + "Text it to customer" button
- Three templates: Color (brand), Black & White, Minimalist — all print to PDF cleanly

### Notes
- The anon key is safe to publish (that's its purpose); security comes from the
  RLS policies above — the public can only READ invoices, never write.
- Anyone who guesses a 6-digit invoice number could view that invoice. These
  contain names/phones, so if that ever bothers you, ask Claude to switch IDs
  to longer random codes.
- robots are blocked from indexing /buildinvoice and /invoice pages.
