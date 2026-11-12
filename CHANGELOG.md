## [2.0.0] - 2026-11-11

### 💥 Breaking Changes
- **Notification Selector Update:** Migrated the notification input selector from device IDs (`integration: mobile_app`) to direct entity services (`domain: notify`). This significantly improves reliability and eliminates issues with device naming slugs. 
  - **Action Required:** If you are updating from v1.x, you will need to open your existing automations based on this blueprint, re-select your notification services in the dropdown, and save.

### ✨ Improvements
- Streamlined notification calls by looping directly over target entity IDs (`notify.xxx`), making execution cleaner and less prone to service-not-found errors.
