# Google Workspace™ Marketplace Review - Testing Guide
## Anaplan Connector for Sheets™

**Last Updated**: November 4, 2025
**For**: Google Workspace™ Marketplace Review Team

---

## Test Account Credentials

### Anaplan Account
- **Email**: ryan.domke.anaplan@gmail.com
- **Password**: Testforgoogle444!
- **Authentication Method**: Basic Authentication (recommended for testing)
- **Region**: US (will auto-detect)

### Test Workspace & Model
- **Workspace Name**: AppFolio Training Sandbox
- **Model Name**: Time Filters

**Note**: This test account has read-only access to sample data specifically configured for Google's review process.

---

## Installation & Setup

### 1. Install the Add-on

1. Open a new Google Sheets™ spreadsheet
2. Install "Anaplan Connector for Sheets™" from your test deployment
3. Once installed, open the sidebar:
   - **Menu**: Extensions → Anaplan Connector for Sheets™ → Open Sidebar
4. The sidebar will load on the right side of your spreadsheet

**Expected Result**: ✅ Sidebar opens successfully with authentication options

---

## Testing Instructions

### Step 1: Authentication (Basic Auth)

**Why Basic Auth?**: Simpler for testing - no OAuth client setup required. The add-on supports both OAuth/SSO and Basic Auth.

1. **In the sidebar, locate the Authentication section** (collapsible menu at top)
2. **Click to expand** the authentication options
3. **Select**: "Basic Authentication" radio button
4. **Enter credentials**:
   - Email: `ryan.domke.anaplan@gmail.com`
   - Password: `Testforgoogle444!`
5. **Click "Login"** button
6. **Wait 3-5 seconds** for authentication

**Expected Result**:
- ✅ Green "Authenticated" status message appears
- ✅ User email displays in sidebar
- ✅ Workspace/Model selectors become enabled
- ✅ Navigation cards (Exports, Saved Views, Schedule, Formatting) become active

**Troubleshooting**: If login fails, verify credentials are entered exactly as shown above (case-sensitive).

---

### Step 2: Configuration (Core Feature Test)

This tests the add-on's ability to fetch available exports/views and create new sheets with data.

#### A. Select Workspace & Model

1. **Click "Configuration" tab** in sidebar (if not already visible)
2. **Workspace dropdown**: Select "AppFolio Training Sandbox"
3. **Model dropdown**: Select "Time Filters"

**Expected Result**: ✅ Both dropdowns populate and selections persist

#### B. Fetch and Run an Export

1. **Click "Exports" card** to expand it
2. **Click "Fetch Available Exports"** button
3. **Wait 3-5 seconds** for exports list to load

**Expected Result**:
- ✅ List of available exports appears in dropdown
- ✅ Progress indicator shows during fetch
- ✅ Export names populate the select dropdown

4. **Select any export** from the dropdown
5. **Click "Run Selected Export"** button
6. **Watch the progress bar** (10-30 seconds depending on data size)

**Expected Result**:
- ✅ Progress bar shows: "Executing export..." → "Downloading data..." → "Writing to sheet..."
- ✅ New sheet tab created with export name
- ✅ Sheet contains data (rows and columns)
- ✅ Timestamp appears in cell B1 showing when data was exported
- ✅ Success message: "Export completed successfully"

#### C. Fetch and Save a View

1. **Click "Saved Views" card** to expand it
2. **Click "Fetch Saved Views"** button
3. **Wait 3-5 seconds** for views list to load

**Expected Result**: ✅ List of saved views appears

4. **Select any view** from the dropdown
5. **If the view has page selectors** (dimensions):
   - You'll see dimension dropdowns appear
   - Select values from each dimension dropdown
6. **Click "Save Configuration"** button
7. **Enter a sheet name** when prompted (or use default)
8. **Wait 10-30 seconds** for data to load

**Expected Result**:
- ✅ New sheet created with specified name
- ✅ Data from the view appears in the sheet
- ✅ Page selectors are applied correctly (filtered data)
- ✅ Sheet configuration is saved for later refresh

**What is a "Saved View"?**: In Anaplan, a saved view is a pre-configured data view with specific dimensions, filters, and formatting. The add-on fetches these views and applies user-selected page selectors (dimension filters).

---

### Step 3: Refresh Sheets (Batch Update Feature)

This tests the add-on's ability to refresh multiple configured sheets at once.

1. **Navigate to Extensions menu** → Anaplan Connector for Sheets™ → **Refresh Sheets**
2. A **modal dialog** will appear showing all configured sheets
3. **Click "Refresh All Sheets"** button
4. **Watch progress indicators** for each sheet

**Expected Result**:
- ✅ Progress bars show for each sheet being refreshed
- ✅ Sheets update with latest data from Anaplan
- ✅ Timestamps update in cell B1 of each sheet
- ✅ Success summary shows: "X of Y sheets refreshed successfully"

**Note**: This feature demonstrates the add-on's value - users can update multiple Anaplan data sheets with a single click instead of manually refreshing each one.

---

### Step 4: Schedule (Automation Feature)

This tests the add-on's scheduling capability for automated refreshes.

1. **In sidebar, click "Schedule" card** to expand it
2. **Click "Refresh Schedule List"** to see any existing schedules
3. **To create a new schedule**:
   - **Click "+ New Schedule"** button
   - **Sheet dropdown**: Select a configured sheet
   - **Frequency dropdown**: Select "Daily"
   - **Time**: Select "9:00 AM"
   - **Click "Save Schedule"** button

**Expected Result**:
- ✅ Schedule is created successfully
- ✅ Schedule appears in the list with details (sheet name, frequency, next run time)
- ✅ Toggle switch is enabled (active)
- ✅ Behind the scenes: Google Apps Script time-based trigger is created

**What This Does**: The add-on creates a time-based trigger in Google Apps Script that will automatically refresh the selected sheet at the scheduled time. Users receive optional email notifications when refreshes complete.

4. **To test schedule management**:
   - **Toggle the schedule off/on** - should update status
   - **Click "Delete"** - should remove the schedule after confirmation

**Note**: Actual scheduled execution won't occur during testing, but you can verify the trigger exists by going to Apps Script Editor → Triggers (clock icon).

---

### Step 5: Sheet Formatting (Optional Feature)

This tests the one-click formatting feature.

1. **In sidebar, scroll to "Formatting" button** (full-width button near bottom)
2. **Click "🎨 Format Configured Sheets"** button
3. **Wait 2-5 seconds** for formatting to apply

**Expected Result**:
- ✅ All configured sheets receive consistent formatting:
  - **Column A**: Light gray background (#F0F0F0)
  - **Row 1**: Light blue background (#E3F2FD) + Bold text
  - **Cell B1**: Yellow background (#FFFF00) for timestamp visibility
  - **Sheet tabs**: Purple color (#9C27B0)
- ✅ Success message shows count of sheets formatted

**Purpose**: Provides consistent, professional Anaplan-style formatting across all data sheets.

---

## Expected Test Data

The test model contains:
- **Sample exports**: Pre-configured export definitions for testing
- **Sample saved views**: Views with dimensional data and page selectors
- **Time-based data**: Sample data covering multiple time periods for testing filters

**Data Volume**: Small datasets (< 1000 rows) for quick testing

---

## Feature Summary Checklist

Use this to verify all major features during testing:

- [ ] **Authentication**: Basic Auth login successful
- [ ] **Configuration**: Workspace & model selection works
- [ ] **Exports**: Fetch and run export creates new sheet with data
- [ ] **Saved Views**: Fetch and save view with page selectors works
- [ ] **Refresh Sheets**: Batch refresh updates multiple sheets
- [ ] **Scheduling**: Create, view, toggle, and delete schedules
- [ ] **Formatting**: One-click formatting applies to all sheets
- [ ] **Error Handling**: Clear error messages when issues occur
- [ ] **Progress Indicators**: Loading states and progress bars display correctly
- [ ] **Data Persistence**: Configurations save and persist across sessions

---

## Common Testing Scenarios

### Scenario 1: First-Time User Experience
1. Fresh install
2. Authenticate
3. Configure first sheet
4. Create a schedule
5. Format sheets

**Expected Time**: 5-10 minutes to complete full workflow

### Scenario 2: Multi-Sheet Management
1. Configure 3-5 different sheets from various exports/views
2. Use "Refresh All Sheets" to update all at once
3. Apply formatting to all

**Expected Time**: 10-15 minutes

### Scenario 3: Page Selectors (Advanced Filtering)
1. Select a saved view with multiple dimensions
2. Choose specific dimension values (page selectors)
3. Verify filtered data in resulting sheet
4. Change page selectors and save again
5. Compare data differences

**Expected Time**: 5-10 minutes

---

## Technical Notes for Reviewers

### OAuth Scopes Used
The add-on requests these scopes:
- `spreadsheets.currentonly` - Read/write current spreadsheet only (not all user spreadsheets)
- `script.external_request` - Call Anaplan API
- `script.container.ui` - Display sidebar interface
- `userinfo.email` - For schedule notifications (optional)
- `script.scriptapp` - Manage time-based triggers for scheduling

**Why these scopes?**: Minimal permissions principle - only access what's needed for functionality.

### Data Storage
- **Authentication tokens**: Stored in Google Properties Service (encrypted)
- **Sheet configurations**: Stored per-sheet in Document Properties
- **Schedules**: Stored in User Properties
- **No external servers**: All data remains in Google's infrastructure

### API Calls
- **Destination**: Anaplan API (auth.anaplan.com, api.anaplan.com)
- **Authentication**: Either OAuth 2.0 or Basic Auth to Anaplan
- **Rate limiting**: Built-in delays to respect Anaplan API limits
- **Parallel requests**: Optimized for batch operations

---

## Troubleshooting Guide

### Issue: Login fails
- **Check**: Credentials entered exactly (case-sensitive)
- **Check**: Internet connection active
- **Try**: Clear browser cache and reload

### Issue: No exports/views appear
- **Check**: Workspace and model selected correctly
- **Check**: Test account has access to the model
- **Wait**: Sometimes takes 5-10 seconds to load

### Issue: "Invalid page selector" error
- **Cause**: Saved view requires page selector values
- **Solution**: Select values from all dimension dropdowns before saving

### Issue: Sheet not created
- **Check**: Console logs (View → Logs in Apps Script editor)
- **Check**: API responses in execution transcript
- **Verify**: Test account has read access to selected data

---

## Support Contact

For questions or issues during review:
- **Email**: anaplansheetsconnector.help@gmail.com
- **Documentation**: https://domke012-cyber.github.io/anaplan-connector-docs/
- **Response Time**: Within 24 hours

---

## Security & Privacy

- ✅ **No data collection**: We don't collect or store user data externally
- ✅ **Limited scope**: Only accesses current spreadsheet
- ✅ **Encrypted storage**: Tokens encrypted in Google Properties Service
- ✅ **User control**: Users can revoke access anytime
- ✅ **Compliance**: Follows Google API Services User Data Policy

**Privacy Policy**: https://domke012-cyber.github.io/anaplan-connector-docs/privacy-policy
**Terms of Service**: https://domke012-cyber.github.io/anaplan-connector-docs/terms-of-service

---

## Additional Testing Resources

### Apps Script Project
- Access the code: Extensions → Apps Script
- View execution logs: View → Logs
- Check triggers: Left sidebar → Triggers (clock icon)

### Test Account Access
- The test account (ryan.domke.anaplan@gmail.com) is configured for Google reviewers
- Access is read-only to prevent accidental data changes
- Account will remain active for review period

---

**Thank you for reviewing Anaplan Connector for Sheets™!**

If you encounter any issues or need clarification, please don't hesitate to reach out to our support email.
