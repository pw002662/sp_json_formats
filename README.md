# SharePoint Column Formatting - Installation Guide

## ⚠️ CRITICAL WARNING

**JSON Column Formatting provides ONLY visual/UI-level protection.**

### What it DOES:
✅ Makes fields appear gray and read-only in the standard edit form
✅ Shows "🔒 Finance only" indicator
✅ Displays tooltip warning when hovering

### What it DOES NOT DO:
❌ Does NOT block Quick Edit (Grid View)
❌ Does NOT block API/Power Automate access
❌ Does NOT block copy/paste operations
❌ Does NOT provide technical enforcement

**At 12 projects/year with trusted PM team, this may be sufficient. For absolute protection, use Power Automate Flow instead.**

---

## Installation Steps

### For Each Field (StartDate, TargetEndDate, ContractValue, Project Name)

1. **Navigate to List Settings**
   - Go to your SharePoint list
   - Click Settings gear → List settings

2. **Open Column Settings**
   - Under "Columns" section, click on the field name (e.g., "StartDate")
   - Scroll down to "Column Settings"

3. **Apply JSON Formatting**
   - Click "Format this column"
   - Select "Advanced mode" at the bottom
   - Copy the entire content from the corresponding .json file
   - Paste into the JSON editor
   - Click "Save"

4. **Repeat for all 4 fields:**
   - StartDate → Use `StartDate_ReadOnly.json`
   - TargetEndDate → Use `TargetEndDate_ReadOnly.json`
   - ContractValue → Use `ContractValue_ReadOnly.json`
   - Project Name → Use `ProjectName_ReadOnly.json`

---

## Testing the Formatting

### Expected Behavior:

**In Edit Form:**
- Fields appear with gray background
- Text is italic and gray-colored
- "🔒 Finance only" indicator visible
- Tooltip shows: "This baseline field is managed by Finance only"
- Cursor changes to "not-allowed" symbol

**In Quick Edit (Grid View):**
⚠️ **Formatting does NOT apply** - fields remain fully editable

---

## Recommended Additional Measures

Since JSON formatting is only cosmetic:

### 1. Hide Fields in PM Dashboard View
- Create custom view for PMs
- Remove all baseline fields from view columns
- Set as default view for PM group
- Reduces accidental edit likelihood by 90%

### 2. Quarterly Audit
Run this audit query every quarter:

**Filter:** Modified By ≠ Finance Group AND Modified Date > Last Audit Date

Check if any baseline fields were changed, correct manually if needed.

### 3. PM Training
Brief PM team once:
- "Gray fields with 🔒 are Finance-only"
- "If you need a baseline change, email Finance"
- "Don't use Quick Edit for project updates"

---

## Removing Formatting (If Needed)

1. List Settings → Column → Format this column
2. Click "Clear formatting"
3. Save

---

## Alternative: Power Automate Flow

If you need stronger protection, create a Flow:

**Trigger:** When item modified
**Condition:** Modified By NOT IN Finance Group
**Action:** Check if baseline fields changed → Revert + Send notification

**Effort:** 15 minutes
**Protection:** Strong (works for all access methods)

---

## File Manifest

- `StartDate_ReadOnly.json` - Formatting for StartDate field
- `TargetEndDate_ReadOnly.json` - Formatting for TargetEndDate field
- `ContractValue_ReadOnly.json` - Formatting for ContractValue field
- `ProjectName_ReadOnly.json` - Formatting for Project Name field
- `INSTALLATION_GUIDE.txt` - This file

---

## Support

Questions or issues? Contact SharePoint Admin or Finance Lead.

**Note:** This is a UI-layer solution. For compliance-critical environments, consider Power Automate enforcement instead.
