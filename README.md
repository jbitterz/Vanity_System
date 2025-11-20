# Vanity Ordering System  Full Project Package (Vanity)

## 1. System Overview
Vanity is a web-based ordering platform for cosmetics enthusiasts. Customers register, log in, explore curated products from Sephora, MAC, Maybelline, Olay, and LOréal, build carts, and complete checkout with calculated subtotal, shipping, taxes, and discounts. Inventory is tracked in real time, and each order links to a unique user profile. Admins manage products, stock, and order statuses, while the platform logs critical events for traceability.

**Primary actors**: Customer, Admin/Staff, Payment Gateway.

## 2. Functional Requirements (summary)
1. Email/password registration & login with JWT sessions.
2. Product catalog with brand filters, search, and pagination.
3. Cart management: add/update/remove, persistent per user.
4. Stock validation and decrement on checkout; prevent overselling.
5. Pricing engine: subtotal + configurable shipping/tax + coupons.
6. Checkout workflow with transaction id and error handling.
7. Order history with statuses (pending, paid, shipped, delivered, cancelled).
8. Admin UI/API for product CRUD, restock, and order status changes.
9. User-to-order linkage plus audit logging (inventory, checkout).
10. Optional addresses per user/order for shipping records.

## 3. Non-Functional Requirements
- Responsive UI (desktop/mobile) built with semantic HTML + Tailwind/Bootstrap.
- Secure password hashing (bcrypt/argon2) and input validation.
- REST APIs respond within 200500ms under normal load.
- Atomic checkout transactions ensure consistency.
- Automated backups, GDPR/PIPEDA-friendly data minimization.
- Observability via structured logs + alerting on checkout failures.

## 4. High-Level Architecture
Frontend SPA or classic HTML views consume Laravel REST APIs. Backend enforces business logic, integrates with payment gateway (Stripe/mocked), and persists to MySQL/MariaDB (SQLite allowed for dev). Queue workers handle async emails/notifications. See `docs/architecture.md` for component diagram narrative.

## 5. Data Model & ERD
Entities: users  orders  order_items, products referenced by order_items, inventory_logs for stock deltas, optional addresses. ASCII ERD:
```
[users] 1---* [orders] 1---* [order_items] *---1 [products]
```
Full SQL DDL lives in `sql/schema.sql`.

## 6. UML (Class Skeleton)
PlantUML text in `uml/vanity_classes.puml` covers `User`, `Product`, `Order`, `OrderItem` relationships. Import into any renderer for diagrams.

## 7. Use Cases & Flows
Detailed descriptions (UC1UC9) plus checkout flow narrative in `docs/use_cases.md`. Includes primary/alternate flows and validation steps.

## 8. Sequence Diagram (Checkout)
`docs/sequence_checkout.md` explains the REST + DB interactions from cart submission through payment confirmation and stock updates, mirroring the transactional steps outlined earlier.

## 9. REST API Surface
`docs/api_endpoints.md` enumerates endpoints, verbs, auth requirements, request/response payloads, and admin-only routes.

## 10. UI Deliverables
- Textual wireframes and annotations: `ui/wireframes.md`.
- Single-file HTML mockup demonstrating layout, filters, product cards, and cart summary: `ui/mockup.html`.
Both are lightweight and can be opened locally.

## 11. C# Windows Forms Scaffold
`csharp/WinFormsScaffold.cs` defines basic models and suggested forms (Login, Catalog, Cart, Checkout) with control mappings and data-binding notes.

## 12. Laravel Structure
`laravel/structure.md` outlines migrations (users, products, orders, order_items, inventory_logs), Eloquent models, controllers (Auth, ProductController, CartController, CheckoutController, Admin/OrderController), policies, and routes (api/web). Includes transaction-safe checkout pseudocode.

## 13. Test Cases / Acceptance Criteria
`tests/acceptance.md` lists priority functional tests for auth, catalog, cart, stock enforcement, checkout, admin workflows, and logging requirements.

## 14. Deployment & Next Steps
`deployment/plan.md` covers environment setup, secrets management, CI/CD, database migrations, payment integration tasks, monitoring, and backlog items. Follow it after scaffolding the codebase.

## 15. Optional Artifacts
Ready to provide on request: sample SQL seed data, rendered PlantUML PNGs, full Laravel starter project, Windows Forms project zip, or a higher-fidelity UI prototype.

> This repository now holds every artifact required to kick off Vanity as a greenfield system, isolated from previous projects.
