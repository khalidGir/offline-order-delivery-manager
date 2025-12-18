STATUS: SCOPE LOCKED — Any changes require explicit revision approval.

## Project Scope & Goals

**1. Primary Objective**
Replace WhatsApp + paper-based order tracking with a **single offline-first system** that lets a local shop reliably manage orders and deliveries even with unstable internet.

**2. Success Metrics**

- Orders processed per day without loss
- Reduction in missed / duplicated orders
- Time from order creation → delivery completion
- Zero data loss during offline usage

**3. Target Customer**
Single local shop (one physical location).
No marketplace. No multi-vendor in v1.

---

## User Personas & Roles

**4. User Roles (v1)**

- Shop Manager
- Delivery Driver

**5. Permissions**

**Shop Manager**

- Create / edit products
- Create orders
- Assign orders to drivers
- Update order status
- View all orders and history

**Delivery Driver**

- View only assigned orders
- Update order status (Out for Delivery → Delivered)
- Cannot edit products or prices

No System Admin role in v1.

**6. End-Customer Interaction**
None.
Customers do **not** log in.
Customer data is entered by the shop only.

---

## Core Features & Functionality

**7. Authentication**

- Phone number + OTP (Firebase Auth)
- No email, no social login

**8. Product Details (v1)**

- Name
- Price
- Optional notes
  No SKU, variants, or images in v1.

**9. Inventory Management**

- No automatic stock decrement
- Inventory tracking is **out of scope** for v1

**10. Order Lifecycle (Final)**

```
Pending → Assigned → Out for Delivery → Delivered
Optional: Cancelled
```

**11. Order Information (Required Fields)**

- Customer name
- Customer phone number
- Delivery address (free text)
- Order items (product + quantity)
- Delivery fee
- Payment status (Cash / Paid)
- Order status
- createdAt / updatedAt (serverTimestamp)

**12. Driver Assignment**
Manual assignment by Shop Manager only.

**13. Driver Tools**

- No route optimization
- No GPS tracking
- Optional “Open in Google Maps” link only

**14. Notifications (v1)**
None.
No SMS, no push notifications.

**15. Payments**
Tracking only.
No online payment processing.

**16. Dashboard & Reporting (v1)**

- Today’s orders
- Orders by status
- Simple totals (count, cash collected)
  No exports or advanced analytics.

---

## Technical & Architectural Requirements

**17. Firebase Services Used**

- Firebase Authentication
- Firestore
- Firebase Hosting

No Cloud Functions, no FCM in v1.

**18. Third-Party Integrations**
None required.

**19. Security & Compliance**

- Firebase security rules
- No formal regulatory compliance required (local shop tool)

---

## Offline & Synchronization Strategy

**20. Offline Data Access**

- Managers: products + recent orders
- Drivers: assigned orders only

**21. Conflict Resolution**

- Firestore default last-write-wins
- serverTimestamp is authoritative
  No manual merge logic.

**22. UI for Sync Status**

- Simple banner: “Offline mode”
- Optional “Syncing…” indicator
  No manual sync buttons.

---

## Deployment & Operations

**23. Hosting**
Firebase Hosting.

**24. CI/CD**
Yes, minimal pipeline:

```
install → test → build
```

No auto-deploy in v1.

**25. Monitoring**
None in v1 beyond console logs.

---

## Future Vision (Non-blocking)

**26. Expected Scale (Year 1)**

- 1–5 shops
- < 200 orders/day per shop

**27. Future Features (Explicitly Deferred)**

- Multi-shop admin
- Customer tracking links
- Inventory management
- Payments
- Notifications
- Analytics

---

## Scope Lock Status

- MVP scope: ✅ **Defined**
- Assumptions removed: ✅
- Overengineering avoided: ✅
- Safe to document and freeze: ✅
