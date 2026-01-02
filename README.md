# 🔥 Shared Firebase Rules - Source of Truth

## ⚠️ CRITICAL: This is the SOURCE OF TRUTH for Firestore Security Rules

**ALL Firestore rule updates MUST be made in this file first:**
- **File**: `shared-firebase-rules/firestore.rules`
- **Location**: `/Users/chebrooks/Documents/IDE_Project/BACKBONE ALL 4 APP Master/shared-firebase-rules/firestore.rules`

## 📋 Rules Coordination

### Source of Truth
- **Primary File**: `shared-firebase-rules/firestore.rules` (THIS FILE)
- **Purpose**: Single source of truth for all Firebase projects
- **Size**: ~206KB, ~4290 lines
- **Used By**: All projects (Dashboard, Licensing, Call Sheet, EDL, Parser Brain, Clip Show Pro)

### Project-Specific Files
- **Dashboard Local File**: `_backbone.Pro.Full-v1.0/firestore.rules.local`
- **Purpose**: Active file used by Dashboard's `firebase.json`
- **Sync Process**: Automatically synced from shared file during deployment

## 🔧 How to Update Rules

### ✅ CORRECT Workflow:
1. **Edit**: `shared-firebase-rules/firestore.rules` (THIS FILE)
2. **Sync**: Run `cp ../shared-firebase-rules/firestore.rules ./firestore.rules.local` from dashboard directory
3. **Deploy**: Rules are automatically synced during `deploy-dashboard.sh`

### ❌ INCORRECT Workflow:
- ❌ Editing `firestore.rules.local` directly (will be overwritten)
- ❌ Editing rules in project-specific folders without updating shared file
- ❌ Creating duplicate rules in multiple files

## 📝 For AI Assistants (LLMs/Cursor)

When updating Firestore security rules:

1. **ALWAYS** edit `shared-firebase-rules/firestore.rules` first
2. **NEVER** edit `_backbone.Pro.Full-v1.0/firestore.rules.local` directly
3. **AFTER** editing shared file, sync to local: 
   ```bash
   cd "_backbone.Pro.Full-v1.0"
   cp ../shared-firebase-rules/firestore.rules ./firestore.rules.local
   ```
4. **THEN** deploy: `firebase deploy --only firestore:rules`

## 🎯 Key Collections

Common collections that may need rule updates:
- `workflow-templates` - Workflow template storage
- `workflow-instances` - Workflow instance storage  
- `workflowInstances` - Alternative camelCase collection
- `organizations/{orgId}/slackConnections` - Slack integration connections
- `networkDeliveryBibles` - Network delivery bible storage
- `sessions` - Production sessions
- `projects` - Project data
- `users` - User data
- `teamMembers` - Team member data

## 📚 Related Files

- **Storage Rules**: `shared-firebase-rules/storage.rules`
- **Firestore Indexes**: `shared-firebase-config/firestore.indexes.json`
- **Dashboard Config**: `_backbone.Pro.Full-v1.0/firebase.json`

## 🚀 Deployment

Rules are deployed automatically during:
- `deploy-dashboard.sh` - Syncs and deploys rules
- Manual: `firebase deploy --only firestore:rules --project backbone-logic`

### Deployment Steps

1. **Update Rules**: Edit `shared-firebase-rules/firestore.rules`
2. **Sync to Projects**: Copy to project-specific locations if needed
3. **Deploy**: Run `firebase deploy --only firestore:rules --project backbone-logic`
4. **Verify**: Check Firebase Console to confirm rules are active

### Storage Rules

Storage rules are in `shared-firebase-rules/storage.rules` and deployed with:
```bash
firebase deploy --only storage --project backbone-logic
```

---

**Last Updated**: Rules coordination established - shared file is source of truth

