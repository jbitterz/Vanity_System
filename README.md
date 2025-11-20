# Vanity Ordering Make-Up System

A greenfield Laravel + Breeze platform where customers browse, order, and track cosmetics from Sephora, MAC, Maybelline, Olay, and L'Oreal. The stack is strictly **PHP / HTML / CSS / Laravel Breeze / MariaDB (SQL)**, optimized for responsive layouts and reliable order tracking.

---

## 1. System Overview
- Users register/login, browse catalog, add products to cart, and checkout with transparent pricing.
- Orders store subtotal, shipping, tax, final total, and transaction IDs; inventory adjusts atomically.
- Admins manage products and stock, update order statuses, and audit sales history.

### Actors
Customer, Admin/Staff, Payment Gateway.

---

## 2. Key Features
1. **User Authentication**
   - Sign-Up and Login pages handled by Laravel Breeze.
   - Unique user IDs stored in MariaDB; passwords hashed with bcrypt/argon2.
   - Authenticated users access ordering workflow and purchase history.
2. **Product Ordering (5 Brands)**
   - Catalog lists Sephora, MAC, Maybelline, Olay, L'Oreal items.
   - Each record shows name, brand, unit price, stock flag, and Add-to-Cart action.
   - Users mix products across brands in one order.
3. **Inventory Management**
   - Stock decrements on successful checkout; prevents oversell.
   - Admin endpoints to restock or adjust quantities with audit logs.
4. **Price Computation**
   - Subtotal = sum(item price × quantity).
   - Total Cost = Subtotal + Shipping Fee + Tax (configurable via `config/pricing.php`).
   - Coupon/discount hooks included for future use.
5. **Checkout & Transaction Handling**
   - Checkout screen shows order summary, calculated totals, and confirmation.
   - Each purchase generates a transaction ID, persists to DB, and logs critical events.
6. **Order Database**
   - Tables cover users, products, inventory logs, orders, and order_items.
   - Orders store timestamps, totals, and user linkage for analytics.
7. **User Purchase History**
   - Logged-in users view past transactions with product lines, amounts, and status (pending/paid/shipped/delivered/cancelled).

---

## 3. Technology Summary
- **Backend**: Laravel 11 + Breeze auth, REST controllers.
- **Frontend**: Blade or lightweight SPA using HTML/CSS and optional Alpine.js.
- **Database**: MariaDB/MySQL using SQL schema in `sql/schema.sql` (also compatible with SQLite for dev).
- **Tooling**: Composer, npm/Vite for assets, Pest/PHPUnit for tests.

---

## 4. Documentation & Deliverables
| Area | File |
| --- | --- |
| Architecture | `docs/architecture.md` |
| Use cases & flows | `docs/use_cases.md` |
| Checkout sequence | `docs/sequence_checkout.md` |
| API endpoints | `docs/api_endpoints.md` |
| SQL schema | `sql/schema.sql` |
| PlantUML classes | `uml/vanity_classes.puml` |
| UI mock | `ui/mockup.html` (wireframes pending manual edit) |
| WinForms reference | `csharp/WinFormsScaffold.cs` |
| Laravel plan | `laravel/structure.md` |
| Acceptance tests | `tests/acceptance.md` |
| Deployment plan | `deployment/plan.md` |

---

## 5. Next Steps
1. Initialize Laravel Breeze project targeting MariaDB.
2. Implement migrations using `sql/schema.sql` as the baseline.
3. Wire up controllers/services per `laravel/structure.md`.
4. Build responsive Blade views mirroring `ui/mockup.html`.
5. Execute acceptance tests and follow the deployment plan for staging/prod.

Need additional artifacts (seed data, rendered UML, Breeze project scaffolding)? Let me know and I'll add them within this folder.
