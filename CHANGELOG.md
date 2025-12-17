# 🔥 Shared Firebase Rules - Changelog

## [2025-12-16] - PageInfo Collection - Public Read Access

### Changed
- **`pageInfo` collection rules** - Made publicly readable (no authentication required)

### Rationale
- `pageInfo` contains only help/documentation content (page descriptions, tips, workflows)
- No sensitive or user-specific data (similar to public documentation)
- Allows apps to load page info during initialization without waiting for auth
- Write access still protected (admin only)

### Fixed
- ❌ "Permission denied for pageInfo collection (user may not be authenticated)" in PageInfoService
- ❌ "Permission denied for indexed-files (user may not be authenticated)" in PageInfoService

### Rule Changes
```
Before:
  match /pageInfo/{pageId} {
    allow read: if isAuthenticated();
    allow write: if isAuthenticated() && isOwnerOrAdmin();
  }

After:
  match /pageInfo/{pageId} {
    allow read: if true; // Public read access for page info/help content
    allow write: if isAuthenticated() && isOwnerOrAdmin();
  }
```

### Deployment
- Deployed to: `backbone-logic` (Production)
- Date: December 16, 2025
- Status: ✅ Complete
- Command: `firebase deploy --only firestore:rules`

### Apps Affected
- ✅ Clip Show Pro (_clip_show_pro_-v1.0) - Primary fix
- ✅ All apps using PageInfoService

---

## [2025-12-16] - Inventory Schemas Collection Added

### Added
- **`inventorySchemas` collection rules** - Inventory schema definitions (Dashboard)

### Fixed
- ❌ "[firestoreInventoryService] Permission error accessing inventorySchemas collection"

### Collections Affected
```
NEW:
- inventorySchemas
```

### Apps Synced
- ✅ Dashboard (_backbone.Pro.Full-v1.0)

---

## [2025-12-16] - IWM Collections Added

### Added
- **`contacts` collection rules** - Contact management for organizations
- **`schemas` collection rules** - Custom inventory schemas
- **`networks` collection rules** - Network configurations for IP management  
- **`savedContainers` collection rules** - Studio assemblies/saved containers

### Fixed
- ❌ "Missing or insufficient permissions" in FirebaseContactsService
- ❌ "Missing or insufficient permissions" in schemaService
- ❌ "Missing or insufficient permissions" in networkIPService
- ❌ "Missing or insufficient permissions" in studioService

### Collections Affected
```
NEW:
- contacts
- schemas
- networks
- savedContainers

USER-ADDED (Manual):
- reviewSessions
- postProductionTasks
- sessionAssignments
- workflowDiagrams
```

### Apps Synced
- ✅ Dashboard (_backbone.Pro.Full-v1.0)
- ✅ IWM (_backbone-iwm-v1.0)

---

## [2025-12-16] - Workflow & Network Delivery Permissions Fix

### Added
- **`user-workflows` collection rules** - User-created workflows with ownership validation
- **`workflow-templates` (hyphenated) collection rules** - User-created templates with public support
- **`workflow-instances` (hyphenated) collection rules** - Alternative naming for workflow instances
- **`networkDeliveryBibles` collection rules** - Network delivery bible documents
- **`networkDeliveryBibles/{id}/deliverables` subcollection rules** - Deliverables with parent validation
- **`networkDeliveryDeliverables` collection rules** - Top-level deliverables

### Changed
- Enhanced `workflowInstances` rules documentation (now "camelCase - legacy")
- Enhanced `workflowTemplates` rules documentation (now "camelCase - legacy")

### Security Features
- ✅ Organization-based isolation for all new collections
- ✅ Ownership validation for user-created content
- ✅ Public template support via `isPublic` flag
- ✅ Subcollection parent validation for deliverables
- ✅ Role-based access control (Admin elevation)

### Fixed
- ❌ "Missing or insufficient permissions" in Workflow Designer
- ❌ "Missing or insufficient permissions" in WorkflowTab
- ❌ "Missing or insufficient permissions" in Network Delivery Service
- ❌ 400 Bad Request errors in SlackContext

### Deployment
- Deployed to: `backbone-logic` (Production)
- Date: December 16, 2025
- Status: ✅ Complete
- Console: https://console.firebase.google.com/project/backbone-logic/firestore/rules

### Collections Affected
```
NEW:
- user-workflows
- workflow-templates (hyphenated)
- workflow-instances (hyphenated)
- networkDeliveryBibles
- networkDeliveryBibles/{id}/deliverables
- networkDeliveryDeliverables

EXISTING (Enhanced):
- workflowInstances (camelCase)
- workflowTemplates (camelCase)
```

### Files Synced
- `_backbone.Pro.Full-v1.0/firestore.rules` ✅
- Other projects will sync on next deployment

---

## Update Process Used

1. ✅ Edited `shared-firebase-rules/firestore.rules` (Source of Truth)
2. ✅ Synced to Dashboard: `cp ../shared-firebase-rules/firestore.rules _backbone.Pro.Full-v1.0/firestore.rules`
3. ✅ Deployed: `firebase deploy --only firestore:rules --project backbone-logic`
4. ✅ Verified: Rules compiled successfully

---

## Next Steps for Other Projects

When other projects (Licensing, Call Sheet, EDL, Clip Show Pro) need these rules:

1. Run their deployment script (auto-syncs from shared rules)
2. Or manually: `cp shared-firebase-rules/firestore.rules <project>/firestore.rules`
3. Deploy: `firebase deploy --only firestore:rules --project <project-id>`

---

**Maintainer Note:** This shared rules file is the SOURCE OF TRUTH. Always edit this file first, then sync to projects.

