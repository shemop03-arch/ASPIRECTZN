# ASPIRECTZN live store setup

This version is designed so the admin dashboard and every customer's storefront read and update the **same online catalogue**. It uses Supabase (database, login and image storage). It cannot sync across customers with browser-only storage, so this setup step is essential.

## 1. Create the shared database

1. Create a project at https://supabase.com/ and keep the project dashboard private.
2. In the Supabase project, open **SQL Editor → New query**.
3. Open `supabase/setup.sql` from this website package, copy all its contents into the SQL editor, and click **Run**.
4. Still in SQL Editor, run `supabase/seed-products.sql` once to load the included catalogue, including both Superstar tees.
5. In **Project Settings → API**, copy the **Project URL** and the **anon / publishable key**. Do not use or expose the `service_role` or secret key.
6. Open `store-config.js` and replace the two placeholder values:

```js
window.ASPIRECTZN_CONFIG = {
  supabaseUrl: 'https://YOUR-PROJECT.supabase.co',
  supabaseAnonKey: 'YOUR_PUBLIC_ANON_OR_PUBLISHABLE_KEY'
};
```

Use the same config file for both the storefront and admin dashboard. Keep it beside `index.html` and `admin.html`.

## 2. Create your private admin login

1. In Supabase, open **Authentication → Users → Add user → Create new user**.
2. Enter your own email and a strong password. Confirm the user if Supabase offers that option.
3. Copy that user's **UID** from the Users list.
4. In **SQL Editor**, run this query, replacing the sample UUID with your own UID:

```sql
insert into public.store_admins (user_id)
values ('PASTE-YOUR-AUTH-USER-UID-HERE');
```

5. In **Authentication → Settings**, turn off public sign-ups if you do not want other people creating accounts. You can still sign in with the admin user you created.

Only user IDs in `store_admins` can add, edit, delete products or upload product photos. The public storefront can only read the catalogue.

## 3. Publish the website

Upload the **contents** of this package (not the ZIP itself) to the same hosting site/folder that currently serves your public store. Keep the folder structure, especially `images/` and `supabase/`.

- Customer link: your existing public website URL (the `index.html` page).
- Private dashboard: the same domain followed by `/admin.html`.

Example: `https://your-store-domain.com/admin.html`

Use your real domain, not this example. Keep the dashboard URL private. It is protected by sign-in and database permissions, but a private URL alone is not security.

## 4. Add or update products

After setup and deployment, open `/admin.html`, sign in, and add the catalogue items. The 11 included products (including the white and black Superstar tees at ₦20,000 each) are loaded by the seed script. Existing image files in `images/` are included in this package and can be referenced by their relative paths. New photos uploaded through the dashboard are stored online automatically.

## How updates work

- Save a price edit: the database changes and the public store refreshes its product list.
- Add/delete a product: all storefront visitors see the changed catalogue on refresh; already-open pages receive realtime updates.
- Mark a product sold out: it remains in the dashboard but is hidden from the available-to-buy product grid.
- Images uploaded from the dashboard go into the public `store-images` bucket; database writes remain admin-only.

## Important

I cannot publish to your hosting account or create a Supabase project without your account access. This package is the connected-store implementation and setup guide; it becomes live only after you complete the Supabase setup and upload these files to your hosting. Never share your Supabase password, admin password, service-role key, or secret key in chat.
