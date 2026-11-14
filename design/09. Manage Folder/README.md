\# Feature 09 — Managed Folders



\## 1. Overview



Managed Folders is the central management interface for folders registered and authorized by the user.



Only folders registered through this feature may be accessed by the application's scanning, analysis, organization, renaming, and monitoring capabilities.



Users can register folders, configure feature permissions, manage exclusions, define folder-specific rules, and inspect folder health.



\### Goals



\- Register folders that the application is allowed to access.

\- Manage registered folder configurations.

\- Control which application features can access each folder.

\- Configure folder-specific organization and rename rules.

\- Configure monitoring settings.

\- Manage excluded files and subdirectories.

\- Monitor folder accessibility and health.

\- Remove folder registrations without deleting physical files.



\## 2. Layout



The page follows the application's main layout:



1\. Sidebar Navigation

2\. Page Header

3\. Managed Folder Tabs

4\. Summary Cards

5\. Managed Folder List

6\. Folder Details Panel



\### Sidebar



Menu:

\- Overview

\- Files

\- Storage

\- Organization

\- Smart Rename

\- Review Changes

\- Monitoring

\- History

\- Managed Folders

\- Settings



The Managed Folders menu must be active.



\### Page Header



Title: `Managed Folders`



Description: `Manage folders that are allowed and used by FileNest for analysis, organization, monitoring, and automation.`



Components:

\- Total Folders

\- Refresh

\- Add Managed Folder

\- Add Managed Folder Dropdown



Refresh only retrieves registered folder information from the database. It must not trigger a filesystem scan.



Add Managed Folder opens the native Windows folder picker through Tauri.



Dropdown options:

\- Add Folder

\- Add Multiple Folders



\## 3. Managed Folder Tabs



Provide five tabs:



1\. Folders

2\. Access \& Scope

3\. Folder Rules

4\. Exclusions

5\. Health



\### Folders



Displays all registered Managed Folders and their configurations.



\### Access \& Scope



Manages which application capabilities are allowed to access each folder.



\### Folder Rules



Manages organization and rename rules associated with a folder.



\### Exclusions



Manages files, directories, and patterns excluded from application processing.



\### Health



Displays folder accessibility, permissions, watcher status, and recent errors.



\## 4. Summary Cards



Display six summary cards.



\### Managed Folders



Displays:

\- Total registered folders.

\- Number of active registrations.



\### Total Size



Displays the combined size of accessible Managed Folders based on available analysis metadata.



\### Total Files



Displays the total number of files recorded in the latest available scan.



\### Active Rules



Displays the number of active folder-specific rules.



\### Monitored



Displays the number of folders with active monitoring watchers.



\### Health



Displays the overall accessibility status of registered folders.



Possible statuses:

\- Healthy

\- Warning

\- Error



All values must come from actual backend records.



\## 5. Managed Folder List



Display all registered folders in a searchable and filterable table.



\### Search



Search by:

\- Folder Name

\- Folder Path



\### Filters



Provide:

\- All Status

\- Active

\- Paused

\- Inaccessible

\- Error



Capability filters:

\- Organization

\- Smart Rename

\- Monitoring

\- Analysis



\### Table Columns



\- Number

\- Folder Name

\- Path

\- Size

\- Files

\- Capabilities

\- Status

\- Last Scanned

\- Actions



\### Folder Information



Each row must display:

\- Folder Name

\- Folder Description

\- Full or abbreviated Path

\- Last Known Size

\- Last Known File Count

\- Enabled Capabilities

\- Registration Status

\- Last Scan Timestamp



Use tooltips for paths that are too long.



\### Selection



Selecting a folder displays its details in the right-hand panel.



\### Context Menu



Provide:

\- Open Folder

\- Scan Now

\- View Analysis

\- View Activity

\- Edit Settings

\- Pause Folder

\- Remove from Managed Folders



Remove from Managed Folders must never delete physical files.



\## 6. Add Managed Folder



The Add Managed Folder action opens a native Windows folder picker.



\### Registration Workflow



1\. User clicks Add Managed Folder.

2\. Native folder picker opens.

3\. User selects a folder.

4\. Backend validates the selected path.

5\. Application checks whether the folder is already registered.

6\. Application checks accessibility and permissions.

7\. Display the folder registration configuration.

8\. User confirms registration.

9\. Save the Managed Folder record.

10\. Refresh the Managed Folder List.



\### Registration Validation



Validate:

\- Path exists.

\- Path is accessible.

\- Path is a directory.

\- Path is not already registered.

\- Path is not a protected Windows system directory.

\- Path is not an unsupported or unsafe location.

\- The selected path does not violate application scope restrictions.



Do not recursively scan the folder during registration unless explicitly requested.



\### Initial Configuration



After selecting a folder, allow users to configure:



\- Folder Name

\- Description

\- Organization

\- Smart Rename

\- Monitoring

\- Include in Analysis



All capabilities should be explicitly configurable.



Registration itself must not automatically enable destructive or modifying operations.



\## 7. Folder Details Panel



When a folder is selected, display its information in the right-hand panel.



\### General Information



\- Folder Name

\- Description

\- Full Path

\- Registration Status

\- Created At

\- Last Scanned



Provide an Edit action.



\### Folder Capabilities



Display individual capability toggles.



\*\*Organization\*\*

\- Allows Organization to analyze and create plans for this folder.

\- Does not grant automatic execution permission.



\*\*Smart Rename\*\*

\- Allows Smart Rename to analyze files and generate rename plans.



\*\*Monitoring\*\*

\- Enables filesystem monitoring for this folder.

\- Requires an active watcher.



\*\*Include in Analysis\*\*

\- Allows Storage Analyzer and other applicable analysis features to include this folder.



\### Capability Behavior



\- Disabling a capability prevents new operations from using that capability.

\- Existing plans must be revalidated before execution.

\- Disabling Monitoring must stop or pause the corresponding watcher.

\- Disabling a capability must not delete its historical records.

\- Capability permissions do not replace approval requirements.



\## 8. Folder Usage



Display the folder's latest known storage usage.



Information:

\- Total Size

\- Total Files

\- Usage Percentage

\- Last Analyzed



If a folder storage limit is configured, display usage against that limit.



Example:



`78.4 GB / 120 GB (65%)`



If no limit is configured, display total usage without a percentage.



Do not perform a new scan merely to render this panel.



\## 9. Access \& Scope Tab



This tab manages application access to registered folders.



\### Access Configuration



For each Managed Folder, display whether the following capabilities are allowed:



\- Storage Analysis

\- Organization

\- Smart Rename

\- Monitoring

\- File Metadata Access

\- Content Extraction



\### Scope Rules



\- Only registered Managed Folders are accessible.

\- Access is restricted to the registered root path.

\- Subfolder access follows the folder's recursive scope configuration.

\- Symbolic links, junctions, and reparse points are not followed by default.

\- Path validation must be performed by the backend.

\- A frontend capability toggle must never be treated as the sole security control.



\### Content Extraction



Content extraction should be separately configurable.



Users must be able to restrict content processing for sensitive folders or file types.



Sending extracted content to a remote AI model through 9Router must follow explicit privacy settings.



\## 10. Folder Rules Tab



Display folder-specific automation rules.



\### Rule Information



\- Rule Name

\- Rule Type

\- Managed Folder

\- Scope

\- Status

\- Last Executed



Rule types:

\- Organization Rule

\- Rename Rule

\- Monitoring Rule



\### Rule Actions



\- View Details

\- Edit Rule

\- Enable Rule

\- Pause Rule

\- Delete Rule



\### Approval Scope



Approved rules may execute automatically only within their previously approved scope.



Changes to:

\- Managed Folder

\- File patterns

\- Destination paths

\- Operation types

\- Execution conditions



must trigger renewed approval when they materially change the approved scope.



\## 11. Exclusions Tab



Allow users to exclude specific content from scanning, analysis, and monitoring.



\### Exclusion Types



\*\*Excluded Directories\*\*

\- Exclude specific subdirectories within a Managed Folder.



\*\*Excluded File Extensions\*\*

\- Exclude selected file types.



\*\*Excluded Filename Patterns\*\*

\- Exclude files matching a specified pattern.



\*\*Excluded Files\*\*

\- Exclude explicitly selected files.



\### Exclusion Information



\- Exclusion Type

\- Pattern or Path

\- Reason

\- Created At

\- Status



\### Actions



\- Add Exclusion

\- Edit Exclusion

\- Enable

\- Disable

\- Remove



\### Exclusion Behavior



\- Exclusions apply only within the associated Managed Folder.

\- Exclusions must be validated by the backend.

\- Exclusions must not expand the application's access scope.

\- Display excluded items clearly in folder configuration.

\- Existing approved operations must be revalidated if their files become excluded.



Exclusions should be applied consistently across relevant scanning, analysis, and monitoring services.



\## 12. Health Tab



Display accessibility and operational health information for all Managed Folders.



\### Health Status



Supported statuses:

\- Healthy

\- Warning

\- Inaccessible

\- Permission Denied

\- Error



\### Health Information



Display:

\- Folder Path

\- Accessibility

\- Read Permission

\- Write Permission

\- Last Successful Access

\- Last Scan

\- Watcher Status

\- Last Error



\### Health Actions



\- Check Accessibility

\- Retry Access

\- Open Folder

\- View Error Details



Health checks must not trigger a full recursive scan.



\### Error Handling



If a folder becomes inaccessible:

\- Display a warning.

\- Preserve its registration.

\- Pause affected operations where appropriate.

\- Do not delete its stored analysis history.

\- Require revalidation before executing pending operations.



\## 13. Folder Settings



Provide a dedicated configuration dialog or page.



Settings may include:



\### General



\- Folder Name

\- Description

\- Recursive Scope

\- Registration Status



\### Analysis



\- Include in Storage Analysis

\- Metadata Collection

\- Content Extraction

\- Analysis Exclusions



\### Organization



\- Allow Organization Analysis

\- Default Organization Strategy

\- Approved Organization Rules



\### Smart Rename



\- Allow Rename Analysis

\- Default Naming Strategy

\- Approved Rename Rules



\### Monitoring



\- Enable Monitoring

\- Recursive Monitoring

\- Monitoring Exclusions



Settings must be persisted and reflected in the corresponding backend services.



\## 14. Remove from Managed Folders



Removing a folder unregisters it from the application.



\### Confirmation Dialog



Display:

\- Folder Name

\- Full Path

\- Current Capabilities

\- Active Watchers

\- Pending Plans

\- Warning that the folder will no longer be managed.



\### Removal Behavior



1\. Request user confirmation.

2\. Check active watchers.

3\. Check pending operations and plans.

4\. Stop associated watchers.

5\. Prevent new operations from using the folder.

6\. Preserve historical audit records.

7\. Remove the Managed Folder registration.



Important:

\- Never delete the physical folder.

\- Never delete its files.

\- Do not silently discard pending plans.

\- Pending operations must be invalidated or blocked until explicitly handled.



\## 15. API Requirements



The API must support at least the following operations.



\### Get Managed Folders



`GET /api/managed-folders`



Query parameters:

\- status

\- capability

\- search

\- page

\- page\_size



Returns registered folders.



\### Get Folder Details



`GET /api/managed-folders/{folder\_id}`



Returns complete folder information.



\### Register Folder



`POST /api/managed-folders`



Request:

\- path

\- name

\- description

\- capabilities

\- configuration



Registers a folder after backend validation.



\### Update Folder



`PATCH /api/managed-folders/{folder\_id}`



Updates folder information and configuration.



\### Remove Folder



`DELETE /api/managed-folders/{folder\_id}`



Removes the registration without deleting physical files.



\### Check Folder Health



`POST /api/managed-folders/{folder\_id}/health-check`



Checks folder accessibility and permissions.



\### Get Folder Rules



`GET /api/managed-folders/{folder\_id}/rules`



Returns associated rules.



\### Get Folder Exclusions



`GET /api/managed-folders/{folder\_id}/exclusions`



Returns exclusions.



\### Create Exclusion



`POST /api/managed-folders/{folder\_id}/exclusions`



Creates a folder exclusion.



\### Update Exclusion



`PATCH /api/managed-folders/{folder\_id}/exclusions/{exclusion\_id}`



Updates an exclusion.



\### Remove Exclusion



`DELETE /api/managed-folders/{folder\_id}/exclusions/{exclusion\_id}`



Removes an exclusion.



These endpoints are proposed API contracts. Adapt them to the existing backend conventions.



\## 16. Data Requirements



\### Managed Folder



\- id

\- path

\- canonical\_path

\- name

\- description

\- status

\- recursive\_scope

\- registered\_at

\- updated\_at

\- last\_scanned\_at

\- last\_accessed\_at



\### Folder Capability



\- id

\- managed\_folder\_id

\- capability\_type

\- enabled

\- configuration

\- updated\_at



\### Folder Exclusion



\- id

\- managed\_folder\_id

\- exclusion\_type

\- pattern

\- reason

\- enabled

\- created\_at

\- updated\_at



\### Folder Health



\- id

\- managed\_folder\_id

\- accessibility\_status

\- read\_permission

\- write\_permission

\- watcher\_status

\- last\_successful\_access

\- last\_error

\- checked\_at



\### Folder Rule Association



\- id

\- managed\_folder\_id

\- rule\_id

\- rule\_type

\- enabled

\- created\_at



Use SQLAlchemy models and Alembic migrations.



\## 17. Technical Requirements



\- Use Python backend for filesystem validation.

\- Use Tauri native folder picker for folder selection.

\- Persist Managed Folder registrations in SQLite.

\- Use canonical paths for access validation.

\- Validate paths before every filesystem operation.

\- Prevent duplicate folder registrations.

\- Prevent access outside registered folder boundaries.

\- Do not follow symbolic links, junctions, or reparse points by default.

\- Keep capability configuration separate from registration data.

\- Preserve historical records when a folder is unregistered.

\- Synchronize capability changes with relevant backend services.

\- Record registration and configuration changes in History.



\## 18. Safety Constraints



\- Only manually registered folders are allowed.

\- Never scan entire disks automatically.

\- Never allow the frontend to bypass backend path validation.

\- Never follow symbolic links, junctions, or reparse points by default.

\- Protect Windows system directories.

\- Registration must not imply permission for every application capability.

\- Disabling a capability must block new operations.

\- Pending plans must be revalidated when folder scope changes.

\- Removing a Managed Folder must not delete physical files.

\- Removing a registration must not erase historical audit records.

\- All filesystem mutations must pass through the Transaction Manager.



\## 19. UI States



\### Empty State



When no Managed Folders exist:

\- Display an explanation that folders must be registered first.

\- Provide Add Managed Folder.

\- Do not display dummy folder data.



\### Loading



Display skeletons for:

\- Summary Cards

\- Folder List

\- Folder Details



\### Selected Folder



Display the selected folder's details in the right-hand panel.



\### Inaccessible



Display the folder's last known metadata and accessibility warning.



\### No Results



When filters return no folders:

\- Display a message.

\- Provide Clear Filters.



\### Error



Display a readable error message and retry option.



\## 20. Acceptance Criteria



\- \[ ] Managed Folders has an active sidebar item.

\- \[ ] Users can register folders using the native folder picker.

\- \[ ] Backend validates every registered path.

\- \[ ] Duplicate registrations are prevented.

\- \[ ] Registration does not automatically trigger a full scan.

\- \[ ] Summary Cards display actual data.

\- \[ ] Folder List supports search and filtering.

\- \[ ] Folder Details displays actual metadata.

\- \[ ] Capabilities can be independently enabled or disabled.

\- \[ ] Capability changes synchronize with backend services.

\- \[ ] Folder Rules can be managed.

\- \[ ] Exclusions can be created and managed.

\- \[ ] Health checks work without triggering full scans.

\- \[ ] Inaccessible folders retain their registration and history.

\- \[ ] Folder removal requires confirmation.

\- \[ ] Removing a registration never deletes physical files.

\- \[ ] Pending operations are handled safely.

\- \[ ] All registration and configuration changes are recorded in History.

\- \[ ] All filesystem access is restricted to registered Managed Folders.



\## 21. Design Reference



Use `image-1` as the visual reference for the Managed Folders page.



Requirements:

\- Maintain the visual language of previous application pages.

\- Use navy for the sidebar.

\- Use blue as the primary accent color.

\- Display summary cards near the top.

\- Place the Managed Folder List in the main content area.

\- Place Folder Details in a right-hand panel.

\- Display capabilities as clear individual toggles.

\- Display folder usage with a progress indicator when a limit exists.

\- Keep Add Managed Folder visible in the page header.

\- Maintain a professional, utility-focused interface.

\- Avoid unnecessary decorative AI elements.



If the visual reference conflicts with behavioral specifications, this README is the authoritative implementation contract.

