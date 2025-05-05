This document provides a modular breakdown of the loyalty platform, including key responsibilities, architecture suggestions, and how to apply SOLID and GRASP principles.

---
## 👤 1. User & Role Management Module

### Purpose:
Manages users, roles, and segmentation info (tier, region, area, chain).
### Segmentation:
- `User`: stores metadata and segmentation.
- `Role`: defines system access.
- `UserSegmentService`: filters users by region, tier, etc.
### Notes:
- Segment filters are reusable across modules.
---
## 🎯 2. Objectives & Points Module
### Purpose:
Assigns objectives and rewards points on completion.
### Segmentation:
- `Objective`, `UserObjective`: store metadata and assignments.
- `PointManager`: handles point adjustments and logging.
- `ObjectiveEvaluator`: separate evaluators (e.g., ExcelEvaluator).
- `PointLog`: audit trail of point transactions.
### Notes:
- Strategy pattern for evaluators.
- SRP ensures clean separation of evaluation and point logic.
---
## 📊 3. Excel Sales Input Integration
### Purpose:
Processes Excel data to complete objectives.
### Segmentation:
- `ExcelReader`: parses files.
- `SalesMapper`: maps data to objectives.
- `SalesObjectiveUpdater`: updates objective progress.
### Notes:
- Abstract parser logic for future formats.
- Clear separation of read vs. apply logic.
---
## 🎁 4. Prize Redemption Module
### Purpose:
Handles redemption of physical and digital prizes.
### Segmentation:
- `Prize`, `UserRedemption`: prize info and redemptions.
- `RedemptionService`: main logic for redeeming.
- `PrizeRedemptionStrategy`: interface for prize types.
- `DigitalCodeService`: handles code pools.
- `AdminPrizeTracker`: tracks fulfillment.
### Notes:
- Follows Open/Closed via strategy pattern.
- WhatsApp delivery via injected service.
---
## 🎬 5. Communication Videos / Academia
### Purpose:
Delivers videos with quizzes to earn points.
### Segmentation:
- `CommunicationVideo`: video content with metadata.
- `VideoQuestionnaire`: quiz content.
- `UserVideoResponse`: stores answers and scores.
- `VideoSegmentFilter`: filters by segment/tier.
### Notes:
- Cohesive module for content + response evaluation.
---
## ⚡ 6. Flash Events / Campaign Module
### Purpose:
Temporary or one-off point-granting interactions.
### Segmentation:
- `FlashEvent`: metadata and type.
- `EventActionHandler`: logic to process event actions.
- `UserEventParticipation`: tracks completions.
### Notes:
- Strategy-style event handlers.
- Could evolve into generic dynamic objective system.
---
## 🛠️ 7. Admin Dashboard
### Purpose:
Internal tool to manage all system content.
### Segmentation:
- `AdminContentManager`: creates events, videos, etc.
- `AdminPrizeManager`: manages prize inventory.
- `AdminReportService`: downloads/export reports.
- `AdminSegmentSelector`: sets visibility filters.
### Notes:
- Use frontend composition: admin UI calls APIs only.
- Clear separation of permissions per function.
---
## 💬 8. WhatsApp Chatbot
### Purpose:
User interaction via messaging: updates, redemptions, events.
### Segmentation:
- `BotCommandRouter`: routes incoming messages.
- `UserSummaryResponder`: formats user stats.
- `CodeDeliveryResponder`: sends codes via WhatsApp.
- `EventReminderResponder`: notifies about goals/events.
### Notes:
- Follows Low Coupling by depending on API/service layers.
- Testable logic separate from WhatsApp SDK.
---
## 🔐 9. Audit Logs
### Purpose:
Track system usage, redemptions, and changes.
### Segmentation:
- `AuditLogger`: core logger.
- `LogFormatter`: formats for DB, file, or analytics.
- Decorators or middleware: used to automatically log actions.
### Notes:
- Use `@loggable` decorators.
- Apply Indirection to reduce system coupling.
---
## ✅ Cross-Cutting Suggestions
- Use service layers and handlers, not fat controllers/models.
- DTOs to isolate internal structure from frontend/WhatsApp.
- Dependency injection for notifier, evaluators, filters.
- Segment logic should be reusable and centralized.
