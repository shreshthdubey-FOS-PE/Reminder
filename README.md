# Freightoscope Activity Reminder Management - Prototype

## Overview
This is a fully functional, pixel-accurate interactive web prototype for **Activity Reminder Management** inside the Freightoscope ERP web application.

## Getting Started

### Quick Start
Simply open **`index.html`** in any modern web browser (Chrome, Edge, Firefox, Safari).

No installation, no server setup, no dependencies needed!

---

## Features Implemented

### ✅ Core Functionality

1. **Sales Settings → Activity Reminder Tab**
   - Configure default reminder duration per activity type (Calls, Email, Meeting, Task)
   - Inline editing with dropdown selectors
   - Persistent settings stored in localStorage

2. **Activities Listing Page**
   - Complete table with search and date filters
   - Sub-tabs for filtering by activity type
   - Live reminder status indicator for each activity
   - Create, edit, and delete operations

3. **Add / Edit Activity Drawer**
   - Segmented Activity Type selector
   - **NEW: Reminder Duration dropdown** with smart defaults
   - Dynamic preview showing calculated trigger time
   - All original fields preserved (Party, Opportunity, Contacts, Date/Time, Duration, Direction, Purpose, Outcome, Status, Priority, Owner, Notes)

4. **Reminder Engine (Business Logic)**
   - **Future Activity** → Automatically creates exactly ONE reminder
   - **Past Activity** → NO reminder created
   - **Calculation**: `Reminder Trigger = Activity Time - Duration`
   - **Edit scenarios** fully handled:
     - Future date/time changed → Reminder recalculated (no duplicates)
     - Past changed to future → Reminder created
     - Future changed to past → Reminder cancelled
     - Duration changed → Trigger recalculated

5. **On-Screen Pop-Up Reminder Alert Modal (Real-time Alerting)**
   - Appears modally on screen at the exact time of reminder trigger, regardless of what view/tab the user is navigating.
   - Prominent Amber Alert header with Activity details (Type, Title, Party, Opportunity, Owner, Notes).
   - **Snooze Actions**:
     - **Snooze (5m)**: Postpones the notification for 5 minutes; modal automatically pops up again after 5 minutes.
     - **Snooze (15m)**: Postpones the notification for 15 minutes.
   - **Mark as Read / Dismiss Action**: Clears the modal alert and updates the reminder status to "Dismissed / Read" in the System Reminders store.

6. **System Reminders Store & Bell Popover**
   - Click the bell icon (bottom left sidebar) to view all scheduled, snoozed, and dismissed reminders.
   - Shows: Subject, Activity Date, Trigger Date, Status badge, Source, Owner.
   - Live status badges: `Scheduled`, `ALERTING (Due Now)`, `Snoozed (until HH:mm)`, `Dismissed / Read`.
   - Direct Snooze and Dismiss action buttons included on each item in the store.

---

## Business Rules Verified ✅

### AC1-AC18 (All 18 Acceptance Criteria)

✅ **AC1**: Activity Reminder Settings available under Settings  
✅ **AC2**: Admin can configure default per activity type  
✅ **AC3**: Form auto-loads configured default  
✅ **AC4**: User can override for individual activity  
✅ **AC5**: Future activity creates one reminder  
✅ **AC6**: Past activity creates no reminder  
✅ **AC7**: Trigger = Activity Time - Duration  
✅ **AC8**: Editing date/time updates existing reminder  
✅ **AC9**: Changing duration updates existing reminder  
✅ **AC10**: Past→Future creates reminder  
✅ **AC11**: Future→Past cancels reminder  
✅ **AC12**: No duplicate reminders  
✅ **AC13**: Subject = Activity Title  
✅ **AC14**: Source = Sales Activity  
✅ **AC15**: Source Number = Empty  
✅ **AC16**: Uses system timezone  
✅ **AC17**: Existing UI preserved  
✅ **AC18**: Existing reminder infrastructure reused  
✅ **NEW**: On-Screen Pop-Up Alert Modal with Snooze (5m/15m) and Mark as Read / Dismiss  

---

## How to Test

### Scenario 1: On-Screen Real-Time Pop-Up Alert
1. Look at an activity (e.g. Initial Sales Discussion with Maersk at 4:00 PM with 30 min reminder → Trigger time is 3:30 PM).
2. In the top **Time Controller** bar, check **"Use Custom Time"** and set the time to **"2026-09-09 15:30"** (3:30 PM).
3. ✅ An on-screen pop-up alert modal immediately pops up over the screen showing the activity details.

### Scenario 2: Test Snooze (5m / 15m)
1. When the pop-up alert appears, click **"5 min"** under Snooze.
2. ✅ The modal closes, and toast confirms snooze until 3:35 PM.
3. Advance the Time Controller to **"15:35"** (3:35 PM).
4. ✅ The pop-up modal re-appears on screen automatically!

### Scenario 3: Test Mark as Read / Dismiss
1. When the pop-up alert appears, click **"Mark as Read / Dismiss"**.
2. ✅ The alert closes.
3. Click the **bell icon** (bottom-left sidebar) → Verify reminder status is **"Dismissed / Read"**.

### Scenario 4: Create a Future Call
1. Click **"+ Create Activity"**
2. Select **"Calls"** as Activity Type
3. Notice the **Reminder** field auto-populated with **"15 minutes before"** (default for Calls)
4. Enter Title: "Client Follow-up"
5. Set Date/Time to a **future** time (e.g., 2 hours from now)
6. Click **Save**
7. ✅ Check the Activities table → **Reminder Status** column shows "15m before, Trigger: [time]"
8. ✅ Click the **bell icon** (bottom left) → Verify the reminder is listed

### Scenario 2: Create a Meeting with Custom Reminder
1. Click **"+ Create Activity"**
2. Select **"Meeting"**
3. Notice **Reminder** auto-populated with **"30 minutes before"** (default for Meeting)
4. **Override** it: Change to **"1 hour before"**
5. Set a future date/time
6. Click **Save**
7. ✅ Verify reminder shows **"1 hour before"** in the table

### Scenario 3: Past Activity (No Reminder)
1. Create an activity
2. Set Date/Time to a **past** time (e.g., yesterday)
3. Click **Save**
4. ✅ Check Reminders Store → **No reminder** created for this activity

### Scenario 4: Edit Activity Date
1. Open an existing **future** activity
2. Change its date/time to 2 hours later
3. Click **Save**
4. ✅ Reminder trigger time recalculated automatically (no duplicate created)

### Scenario 5: Change Settings Default
1. Navigate to **Settings** (left sidebar → Sales → Settings)
2. Click **"Activity Reminder"** tab
3. Click **"Configure Default"** for **Meeting**
4. Change from **30 minutes** to **1 hour**
5. Click **Save**
6. ✅ Create a **new** Meeting → Reminder defaults to **1 hour**
7. ✅ Check **existing** Meeting activities → Their reminders remain **unchanged**

---

## Data Persistence

- All activities and settings are stored in **browser localStorage**
- Data persists across browser refresh
- Click the **sync/refresh icon** (bottom left sidebar) to reset to initial demo data

---

## UI Fidelity

The prototype **exactly replicates** the Freightoscope design language from the provided screenshots:

- ✅ Navy blue sidebar (`#16325c`)
- ✅ Active menu highlighting (`#0070d2`)
- ✅ White content cards with subtle borders
- ✅ Table styling (gray headers, hover states)
- ✅ Segmented Activity Type buttons
- ✅ Drawer slide-in animation (620px width)
- ✅ Red circular close button
- ✅ Enterprise gray background (`#f4f6f9`)
- ✅ Font: System UI stack (Segoe UI, Roboto, sans-serif)

---

## Architecture

- **Single-page application** (React 18 via CDN)
- **No build process required**
- **No backend needed**
- **Self-contained**: All CSS, JavaScript inline
- **External dependencies**:
  - React 18.3.1 (CDN)
  - Day.js 1.11.10 (Date/time calculations)
  - Tailwind CSS 3 (CDN Play mode)
  - FontAwesome 6.5.2 (Icons)

---

## File Structure

```
D:\Projects\Reminder\
├── index.html                          # Main prototype application
├── README.md                           # This file
├── Prompt.txt                          # Original specification (1000 lines)
├── Notes_Meeting.txt                   # Meeting notes
├── Activity Listing Page.png           # Screenshot reference
├── Add New Activity - Side Drawer.png  # Screenshot reference
├── Add New Activity - Full DrawerPage.png # Screenshot reference
└── Sales Settings Page.png             # Screenshot reference
```

---

## Browser Compatibility

✅ Chrome 90+  
✅ Edge 90+  
✅ Firefox 88+  
✅ Safari 14+

---

## Known Limitations (Prototype)

- No actual email/SMS notifications sent (visual indicator only)
- No backend API integration
- Data stored locally (not synced across devices)
- Simulated user authentication (always logged in as "Shreshth Dubey")

---

## Next Steps for Production

1. **Backend Integration**
   - Connect to actual Freightoscope API endpoints
   - Real database persistence (PostgreSQL / MySQL)
   - User authentication & authorization

2. **Notification System**
   - Email notifications at trigger time
   - SMS integration (optional)
   - Browser push notifications

3. **Multi-user Support**
   - Real-time collaboration
   - User permissions & roles
   - Activity assignment workflow

4. **Enhanced Features**
   - Recurring reminders
   - Reminder templates
   - Bulk operations
   - Export/import functionality

---

## Contact

For questions or feedback about this prototype, contact the Freightoscope development team.

---

**Version**: 1.0  
**Date**: September 9, 2026  
**Status**: ✅ Prototype Complete - All 18 Acceptance Criteria Verified
