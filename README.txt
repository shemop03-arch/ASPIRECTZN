ASPIRECTZN LIVE STORE + PRIVATE ADMIN DASHBOARD

WHAT'S INCLUDED
- index.html: customer-facing storefront
- admin.html: private, sign-in protected product dashboard
- store-config.js: shared online database connection settings (fill this in)
- products-default.json: included starter catalogue
- supabase/setup.sql: database, security policies, image storage and realtime setup
- supabase/seed-products.sql: one-time import of the 11 included products
- SUPABASE-SETUP.md: complete setup and deployment guide
- images/: brand and product images, including both Superstar tees

IMPORTANT DIFFERENCE
The old dashboard stored edits only in one browser. That cannot update a public website for every customer. This version uses Supabase as a shared online database. After the one-time setup and deployment, the admin dashboard and customer storefront use the same catalogue. Product edits sync to visitors' open storefronts through realtime and to new visitors on page load.

START HERE
1. Read SUPABASE-SETUP.md.
2. Create a Supabase project and run supabase/setup.sql.
3. Run supabase/seed-products.sql once to add the included 11 products.
4. Create your own Supabase Auth user, whitelist its UID in public.store_admins, and put the Project URL + public anon/publishable key in store-config.js.
5. Upload the contents of this folder to your existing website hosting, replacing the old website files.
6. Open your public website link for customers. Open /admin.html to sign in and manage the store.

SECURITY
Never put a Supabase service_role key or secret key in store-config.js. Only the public anon/publishable key belongs in browser code. The database policies restrict all product and image changes to the user IDs explicitly whitelisted in store_admins. Disable public signups after creating your owner login.

This ZIP does not deploy itself to your hosting or create a Supabase project. Those account-side steps must be completed before shared live editing works.
