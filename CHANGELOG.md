# Changelog

All notable changes to Qawama (قواما) are documented here.

---

## [1.0.0] — 2026-03-23

First release. A fully offline smart budgeting app targeting Oman and the GCC region.

### Core

- **Database:** Drift/SQLite with 10 tables (transactions, categories, budgets, accounts, user rules, recurring transactions, tags, savings goals, notification logs) — schema v7 with full migration support
- **State management:** Riverpod with reactive streams throughout
- **Architecture:** Hybrid offline-first — all data on-device, cloud only for auth, backup, and exchange rates

### Transaction Input

- **SMS auto-read:** Background listener for incoming bank SMS + bulk inbox scan with duplicate detection (2-minute bucketed dedup)
- **Universal SMS parser framework:** Modular bank parser registry supporting Bank Muscat, NBO, Alizz Islamic, Bank Dhofar, OAB, Sohar International — handles English and Arabic SMS formats
- **Bank statement import:** PDF and CSV file parsing with preview, duplicate detection, and column mapping
- **Manual entry:** Full transaction form with category, amount, date, notes, and income/expense toggle

### Categorization

- **3-tier rule engine:** User rules (exact + contains match) → built-in keyword rules → fallback to "Other"
- **User learning loop:** When manually categorizing, prompts "Apply to all similar?" to create new rules and retroactively update past transactions
- **21 default categories** with Phosphor icons and customizable icon picker
- **User rules management screen** for viewing, editing, and deleting rules

### Screens

- **Dashboard:** Monthly spending summary, 7-point spending chart, top 4 categories with progress bars, recent transactions, cumulative spending pace chart with fullscreen expand
- **Transactions:** Search bar, category/source filter chips, unclassified banner, edit mode, transaction tags
- **Budgets:** Per-category budget limits, progress bars, "OVER" badge, savings goals
- **Insights:** 6-month bar chart, daily trend line chart, income vs expenses comparison, insight cards (warnings, trends, tips), category spending comparisons
- **Settings:** Profile card, dark mode toggle, auto SMS toggle, notification preferences, data management (import, scan, categories, backup), language selector

### Accounts & Cards

- **Auto-discovery:** Accounts created automatically from SMS (bank + last 4 digits)
- **Account management:** View, nickname, deactivate, soft-delete with transaction cleanup
- **Balance tracking:** Last known balance updated from SMS data

### Recurring Transactions

- **Auto-detection:** Identifies recurring patterns from transaction history
- **Management:** View, pause, resume, delete recurring entries
- **Dashboard integration:** Upcoming recurring transactions shown on home screen
- **Alerts:** Notifications for expected recurring transactions

### Currency

- **Primary:** OMR (3 decimal places)
- **Foreign currency:** Auto-detect from SMS, convert to OMR via ExchangeRate-API with retry queue for failed conversions
- **Display:** OMR primary with original currency as secondary note

### Export

- **PDF export:** Monthly/custom date range reports with native Arabic support (right-to-left layout, Arabic shaping)
- **CSV export:** Full transaction data export for spreadsheet use

### Notifications

- **Budget alerts:** Approaching limit (80%) and exceeded limit warnings
- **Recurring transaction alerts:** Reminders for expected transactions
- **Local notifications** via flutter_local_notifications
- **Push foundation:** Firebase Cloud Messaging integration

### Auth & Backup

- **Optional Google sign-in** via Firebase Auth
- **Cloud backup:** End-to-end encrypted (AES-256) backup/restore via Supabase
- **Works fully offline** without sign-in

### Localization

- **English and Arabic** with full RTL layout support
- **Localized categories:** All 21 categories translated to Arabic
- **Arabic-aware exports:** PDF reports render correctly in Arabic

### Theme & Polish

- **Light and dark mode** with system default and manual toggle
- **Accent color:** #00D09C (teal/green)
- **Custom app icon and splash screen**
- **Shimmer loading states** for async content
- **Haptic feedback** on key interactions
- **Error handling** with user-friendly messages
- **Onboarding flow** for first-time setup

### Brand

- **Name:** Qawama (قواما) — "Balance/moderation" from Al-Furqan 25:67
- **Tagline:** Balanced spending, blessed living
- **Package:** com.budgetly.budgetly (preserved for Firebase/Supabase compatibility)

---

## [Unreleased — feature/home-widgets]

### In Progress

- **Android home screen widgets:** Small (2×1) monthly summary and large (4×2) detailed summary with top categories and last transaction
- Uses `home_widget` package for Flutter ↔ native SharedPreferences bridge
- Light/dark theme support via Android resource qualifiers
- RTL support for Arabic locale
- Reactive updates on transaction/budget changes
