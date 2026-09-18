# MR LuxeCart — Production Deployment Package

A production-oriented Node.js + Express + PostgreSQL e-commerce starter for Bangladesh.

## Included
- Premium storefront and responsive mobile UI
- PostgreSQL database with transaction-safe stock/order creation
- Secure admin login with bcrypt password hashing + HttpOnly cookie JWT
- Admin dashboard: products, edit/delete, stock, orders, customers, payment status
- Product image uploads (JPEG/PNG/WebP/GIF)
- bKash, Nagad and Cash on Delivery checkout flows
- Manual bKash/Nagad transaction-ID verification workflow
- Health endpoint: `/health`
- Helmet security headers and login rate limiting
- Docker Compose for local PostgreSQL
- Database migration and admin bootstrap scripts

## Important payment note
The included bKash/Nagad checkout is a **merchant-number + transaction-ID workflow**. It does not falsely claim automatic gateway settlement. Automatic bKash/Nagad checkout must be activated with approved merchant credentials and the provider's current official API/callback requirements. Put credentials in hosting environment variables; never commit them to Git.

Official provider starting points:
- bKash developer portal: https://developer.bka.sh/
- Nagad merchant/payment information: https://nagad.com.bd/services/?service=merchant-payment

## Local setup
1. Copy `.env.example` to `.env` and fill values.
2. Start PostgreSQL: `docker compose up -d db`
3. Install dependencies: `npm install`
4. Run schema: `npm run migrate`
5. Create/update admin: `npm run admin:create`
6. Start: `npm start`
7. Open `http://localhost:3000`
8. Admin: `http://localhost:3000/admin.html`

## Production checklist
- Use a managed PostgreSQL/Supabase database with backups.
- Set a strong random `JWT_SECRET`.
- Use HTTPS and set `NODE_ENV=production`.
- Set `APP_URL` to the real domain.
- Use persistent/object storage for product images; local disk is not suitable for ephemeral hosts.
- Put secrets only in the hosting provider's secret/environment-variable manager.
- Configure your approved bKash/Nagad gateway credentials and callback/webhook verification before advertising automatic online payment.
- Add email/SMS notifications and an operational monitoring service as needed.
- Review Bangladesh tax, consumer, privacy and payment-provider requirements before launch.
