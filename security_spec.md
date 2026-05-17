# Security Specification for s7bi GO

## Data Invariants
1. **User Identity**: A user's profile can only be modified by the user themselves, except for the `role`, `subscription`, and `approved` fields which are admin-exclusive.
2. **Subscription Integrity**: Workers and Shops cannot set their own `approved` status or `subscription` tier to anything other than `none` without admin intervention.
3. **Shop Ownership**: Only the `ownerId` of a shop can add products or modify shop details.
4. **Order Security**: 
   - Users can only read their own orders.
   - Shops can only read orders assigned to their `shopId`.
   - Workers can only read orders they have accepted or that are pending in their wilaya (if allowed).
5. **Payment Proofs**: Users can create payments but cannot modify them once created (except for admin approval/rejection). Users can only view their own payments.

## The "Dirty Dozen" Payloads (Anti-Patterns)
1. **Self-Promotion**: `{ "role": "admin" }` sent during user registration.
2. **Instant Approval**: `{ "approved": true }` sent by a Worker during sign-up.
3. **Shadow Update**: `{ "name": "New Name", "isAdmin": true }` where `isAdmin` is a ghost field.
4. **Subscription Bypass**: `{ "subscription": "lifetime" }` sent by a Shop owner.
5. **Orphaned Shop**: Creating a shop with a `ownerId` that doesn't match the authenticated user.
6. **Price Tampering**: Updating a product price with a negative value or a non-numeric string.
7. **Order Hijack**: A user trying to view orders of another user by changing the `userId` in the query.
8. **Payment Forgery**: Trying to update a pending payment's `status` to `approved` from the client.
9. **Fake Order acceptance**: A worker accepting an order that is already `accepted` by another worker.
10. **ID Poisoning**: Sending a 2MB string as a Document ID.
11. **Email Spoofing**: Setting `email` to `admin@s7bi.com` without verification.
12. **System Field Injection**: Manually setting `createdAt` to a future date instead of `serverTimestamp()`.

## Test Runner (Logic Verification)
All operations involving the above payloads must return `PERMISSION_DENIED`.
