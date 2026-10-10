# Implementation Plan - Firebase Persistence, Live Sync & Reseller Referral Logic

## User Requirements Summary
1. **Firebase Persistence & Permanent Delete**: Ensure all product changes, customer orders, reseller accounts, and transaction records persist to Firestore in real-time, and permanent deletion from admin completely removes items from both Firestore and the web store without restoration capability.
2. **Live Sync on Sync Click**: Ensure publishing/syncing updates immediately reflect across the live website and AI Studio preview.
3. **Reseller Referral & Commission Logic**:
   - Hidden official reference code for standard signups (no extra fee/markup).
   - Signups under an active reseller apply a dynamic wholesale markup (default +10 ৳).
   - Admin dynamic control of reseller margin/commission rates.
   - Proportional percentage commission calculation based on actual reseller profit margins.

## Proposed Changes

### 1. Backend Persistence & Permanent Delete (`server.ts`, `server/db.ts`, `server/firebase.ts`)
- Verify Firestore real-time write/sync operations on entity creations, updates, and permanent deletions.
- Ensure permanent deletion endpoints (`DELETE /api/admin/products/:id`, etc.) purge records permanently from both in-memory state, local persistence, and Firebase Firestore collections.

### 2. Reseller Referral & Dynamic Admin Margin Control (`server.ts`, `src/utils/pricing.ts`, `src/components/reseller/...`)
- Update backend registration and reseller lookup to handle hidden official root reference vs active reseller upline.
- Apply dynamic wholesale price adjustment (`+10 ৳` default or custom admin margin per reseller).
- Implement proportional percentage commission calculation for referral bonuses based on actual profit ratios.

### 3. Admin & Reseller UI Updates (`src/components/AdminPortal.tsx`, `src/components/EmployeePortal.tsx`, etc.)
- Provide admin controls to inspect and adjust individual reseller commission rates and markups.
- Ensure smooth synchronization across all tabs and components.

## Verification Plan
- Run `compile_applet` and `lint_applet` to verify zero type errors.
- Test Firebase persistence and sync flows.
