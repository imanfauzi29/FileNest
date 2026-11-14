\# Feature 05 — Smart Rename



\## 1. Overview



Smart Rename analyzes and generates consistent, descriptive, and organized file names using AI assistance.



Users can select a folder or multiple files, choose a naming strategy, and run an analysis to generate proposed file names.



All file renaming operations must be presented as a Rename Plan and approved through Review Changes before execution.



\### Goals



\- Standardize file naming conventions.

\- Generate more descriptive file names.

\- Remove inconsistent naming patterns and unnecessary characters.

\- Apply custom naming patterns.

\- Group file names based on context or content.

\- Prevent file name collisions.



AI is responsible only for generating recommendations. It must never rename files directly.



\## 2. Layout



The page follows the application's main layout:



1\. Sidebar Navigation

2\. Page Header

3\. Rename Tabs

4\. Configuration Panel

5\. Analysis Result

6\. Rename Preview

7\. Plan Actions



\### Sidebar



Menu:

\- Overview

\- Files

\- Storage

\- Organization

\- Smart Rename

\- Monitoring

\- History

\- Managed Folders

\- Settings



The Smart Rename menu must be active.



\### Page Header



Title: `Smart Rename`



Description: `Analyze and generate consistent, descriptive, and organized file names using AI.`



Components:

\- Last Analysis

\- Refresh

\- Generate Rename Plan

\- Generate Rename Plan Dropdown



Refresh only retrieves existing data from the database.



Generate Rename Plan starts the analysis and generates proposed file names.



\## 3. Rename Tabs



Provide four tabs:



1\. Create Plan

2\. Review Plan

3\. Rename Rules

4\. History



\### Create Plan



Allows users to select files or folders, configure naming strategies, and generate rename previews.



\### Review Plan



Displays all previously created Rename Plans.



\### Rename Rules



Displays saved naming rules approved by the user.



\### History



Displays analysis and rename execution history.



\## 4. Create Plan



Create Plan consists of two main areas:



\- Configuration Panel on the left.

\- Analysis Result and Rename Preview on the right.



\### 4.1 Select Files or Folder



Users can select files or folders to analyze.



Provide two selection options:



\*\*Select Folder\*\*

\- Select one Managed Folder or a subfolder within it.

\- When a folder is selected, analyze its files according to the configured options.

\- Display the selected folder path.



\*\*Select Files\*\*

\- Select multiple files manually.

\- All selected files must belong to registered Managed Folders.

\- Use the native file picker through Tauri.

\- Validate selected file locations again in the backend.



Do not allow selecting files outside Managed Folders.



\### 4.2 Rename Strategy



Provide three naming strategies.



\*\*Make Consistent\*\*



Standardize file naming conventions.



Examples:

\- `My File FINAL.PDF` → `my-file-final.pdf`

\- `IMG\_001.JPG` → `img-001.jpg`

\- `Banner New App.PNG` → `banner-new-app.png`



Supported transformations may include:

\- Lowercase or uppercase conversion.

\- Space replacement.

\- Invalid character removal.

\- Separator standardization.



\*\*Add Meaningful Names\*\*



Generate more descriptive file names based on file context.



Examples:

\- `IMG\_001.JPG` → `login-screen.jpg`

\- `IMG\_002.JPG` → `register-screen.jpg`

\- `screenshot 2025-01-20.png` → `dashboard-overview.png`



AI may use:

\- Current file name.

\- File metadata.

\- Folder structure.

\- File content, if explicitly permitted by the user.



For images, AI may use visual analysis if supported by the configured model.



For documents, content extraction must be selective and follow privacy settings.



\*\*Organize with Pattern\*\*



Apply a user-defined naming pattern.



Example:



`{project}-{type}-{number}`



Available variables:

\- `{name}`

\- `{project}`

\- `{type}`

\- `{date}`

\- `{number}`



Provide:

\- Pattern input

\- Available variables reference

\- Pattern preview

\- Pattern validation



If a variable has no available value, display a warning and do not generate an invalid name.



\### 4.3 Options



Provide the following options:



\*\*Use AI to understand file content\*\*

\- Allows AI to analyze file content when necessary.

\- When disabled, use file names and metadata only.

\- Content sent to the model must follow privacy settings.



\*\*Keep file extension\*\*

\- Preserve the original file extension.

\- Enabled by default.



\*\*Convert to lowercase\*\*

\- Convert file names to lowercase.

\- Do not unintentionally modify the extension when Keep file extension is enabled.



\*\*Replace spaces with underscore (\_)\*\*

\- Replace spaces with underscores.



\*\*Add number sequence if needed\*\*

\- Append a sequence number when a naming collision occurs.



\*\*Skip files that already follow the rule\*\*

\- Skip files that already comply with the selected naming strategy.



Conflicting options must be validated before analysis.



\### 4.4 Analyze \& Preview Rename



The primary action for starting the analysis.



Workflow:

1\. Validate selected files or folder.

2\. Validate the naming strategy and options.

3\. Send the analysis request to the backend.

4\. Backend creates an analysis job.

5\. Hermes performs the analysis when required.

6\. AI generates proposed file names.

7\. Backend validates the proposed names.

8\. Backend generates the Rename Preview.

9\. Display the results in Rename Preview.



No filesystem rename operation is allowed at this stage.



\## 5. Analysis Result



Display four summary cards.



\### Files Analyzed



The number of successfully analyzed files.



\### Files to Rename



The number of files with proposed names different from their current names.



\### No Change



The number of files that do not require renaming.



\### Total Size



The total size of all analyzed files.



All values must come from actual analysis results.



\### Re-analyze



Run the analysis again using the same configuration.



Previous analysis results must remain available in history.



\## 6. Rename Preview



Rename Preview is the main section of the Smart Rename page.



Display all proposed file names before creating a Rename Plan.



\### Table Columns



\- Checkbox

\- File Icon

\- Current Name

\- Proposed Name

\- Reason

\- Status



\### Current Name



Displays the current file name.



\### Proposed Name



Displays the recommended new file name.



Users must be able to manually edit the proposed name before saving the plan.



\### Reason



Explains why a file name was changed.



Examples:

\- Describe content (AI)

\- Make consistent

\- Remove number + describe

\- Apply naming pattern

\- Already consistent



\### Status



Supported statuses:

\- Rename

\- No Change

\- Conflict

\- Invalid Name

\- Needs Review

\- Skipped



Use consistent visual indicators for each status.



\### Selection



\- Each row must have a checkbox.

\- The header checkbox selects all files on the current page.

\- Display the number of selected files.

\- Display the number of files that will be renamed.

\- Users can deselect individual files.



\### Search and Filter



Provide:

\- Search file name

\- Filter by status

\- View All Files

\- View Rename Only

\- View No Change

\- View Conflicts



\### Pagination



Provide:

\- Rows per page: 10, 25, 50, 100

\- Previous Page

\- Next Page

\- First Page

\- Last Page



Display the total result count and current page range.



\## 7. Rename Validation



Before a plan is created, the backend must validate every proposed name.



Validation must include:



\- Name must not be empty.

\- Name must not contain illegal Windows filename characters.

\- Name must not use reserved Windows device names.

\- Name must not exceed supported filesystem name length limits.

\- File extension must be preserved according to configuration.

\- Destination name must not conflict with an existing file.

\- No duplicate proposed names within the same destination folder.

\- No path traversal.

\- The resulting path must remain within the approved Managed Folder.



\### Conflict Handling



When a proposed name already exists:



1\. Mark the item as Conflict.

2\. Display the conflicting file name.

3\. Offer alternative names.

4\. If Add number sequence is enabled, generate numbered alternatives.

5\. Validate all generated alternatives again.



Never overwrite existing files.



\## 8. Rename Plan



After preview generation, users can create a Rename Plan.



\### Save Plan



Save the result as a draft.



This action must not modify the filesystem.



\### Review Changes



Open the Review Changes page with the selected rename operations.



\### Rename Plan Details



Each operation must contain:

\- Source Path

\- Current Name

\- Proposed Name

\- Destination Path

\- Validation Status

\- Reason

\- Selected Status



Items with Conflict or Invalid Name status must not be executable until resolved.



\## 9. Review Plan Tab



Display all Rename Plans.



\### Table Columns



\- Plan Name

\- Managed Folder

\- Files Analyzed

\- Files to Rename

\- Created At

\- Status

\- Actions



Supported statuses:

\- Draft

\- Pending Review

\- Approved

\- Executing

\- Completed

\- Failed

\- Rejected

\- Cancelled



\### Actions



\- View Plan

\- Continue Review

\- Duplicate Plan

\- Delete Draft



Delete Draft only removes plan data that has not been executed. It must never delete or modify physical files.



\## 10. Rename Rules Tab



Display saved naming rules.



\### Rule Information



Each rule must display:

\- Rule Name

\- Managed Folder Scope

\- Naming Strategy

\- Pattern

\- Options

\- Created At

\- Last Executed

\- Status



Supported statuses:

\- Active

\- Paused

\- Disabled



\### Rule Actions



\- View Details

\- Edit Rule

\- Pause Rule

\- Enable Rule

\- Delete Rule



Changes affecting the scope, pattern, or operation type must require renewed user approval.



\### Approved Rules



Previously approved rules may execute automatically only within their approved scope.



Restrictions:

\- Approved Managed Folder.

\- Approved naming pattern.

\- Approved file types.

\- Approved options.

\- Previously defined execution conditions.



If a conflict or out-of-scope condition is detected, the operation must be sent to Review Changes.



\## 11. History Tab



Display Smart Rename activity history.



Information:

\- Timestamp

\- Managed Folder

\- File Count

\- Action

\- Status

\- Executed By



Activity types:

\- Analysis started

\- Analysis completed

\- Rename plan created

\- Rename plan saved

\- Rename approved

\- Rename executed

\- Rename completed

\- Rename failed

\- Rule created

\- Rule executed



Clicking an activity opens its details.



\## 12. Background Job



Rename analysis must run as a background job.



Information:

\- Job ID

\- Managed Folder

\- Status

\- Progress

\- Files Processed

\- Total Files

\- Started At

\- Completed At

\- Error Details



Supported statuses:

\- Queued

\- Running

\- Completed

\- Failed

\- Cancelled



Users may navigate to other pages without cancelling the job.



\## 13. API Requirements



The API must support at least the following operations.



\### Create Rename Analysis



`POST /api/smart-rename/analyze`



Request:

\- managed\_folder\_id or selected\_file\_ids

\- rename\_strategy

\- custom\_pattern

\- options



Response:

\- job\_id

\- status



\### Get Job Status



`GET /api/smart-rename/jobs/{job\_id}`



Returns analysis progress and job status.



\### Get Rename Preview



`GET /api/smart-rename/analyses/{analysis\_id}/preview`



Returns current and proposed file names.



\### Update Proposed Name



`PATCH /api/smart-rename/preview/{item\_id}`



Updates a proposed name manually.



\### Create Rename Plan



`POST /api/smart-rename/plans`



Creates a Rename Plan based on selected preview items.



\### Get Rename Plans



`GET /api/smart-rename/plans`



Returns all Rename Plans.



\### Get Rename Plan Details



`GET /api/smart-rename/plans/{plan\_id}`



Returns operation details.



\### Get Rename Rules



`GET /api/smart-rename/rules`



Returns all naming rules.



\### Create Rename Rule



`POST /api/smart-rename/rules`



Creates a naming rule that can be saved after user approval.



These endpoints are proposed API contracts. Adapt them to the existing backend conventions.



\## 14. Data Requirements



\### Rename Analysis



\- id

\- managed\_folder\_id

\- strategy

\- configuration

\- status

\- files\_analyzed

\- created\_at

\- completed\_at



\### Rename Preview Item



\- id

\- analysis\_id

\- file\_id

\- source\_path

\- current\_name

\- proposed\_name

\- reason

\- validation\_status

\- selected

\- created\_at



\### Rename Plan



\- id

\- analysis\_id

\- managed\_folder\_id

\- plan\_name

\- status

\- total\_operations

\- created\_at

\- updated\_at



\### Rename Operation



\- id

\- plan\_id

\- file\_id

\- source\_path

\- proposed\_name

\- destination\_path

\- validation\_status

\- execution\_status



\### Rename Rule



\- id

\- name

\- managed\_folder\_id

\- strategy

\- pattern

\- options

\- approved\_scope

\- status

\- created\_at

\- updated\_at

\- last\_executed\_at



Use consistent database relationships and manage schema changes through Alembic migrations.



\## 15. AI and Backend Requirements



\- Hermes acts as the AI orchestrator.

\- 9Router acts as the model gateway.

\- AI only generates structured naming recommendations.

\- Backend validates every generated name.

\- AI must never rename files directly.

\- Never execute raw AI output as a filesystem command.

\- Never send file content to a model without the appropriate user permission and privacy settings.

\- For files that do not require content understanding, prioritize file names and metadata.



Example structured output:



\- file\_id

\- current\_name

\- proposed\_name

\- reason

\- confidence



Confidence may be used as a review indicator, but it must never replace backend validation.



\## 16. Safety Constraints



\- No renaming before approval.

\- Never unintentionally change file extensions.

\- Never overwrite existing files.

\- Never access files outside Managed Folders.

\- Never trust AI-generated paths without backend validation.

\- Revalidate source and destination immediately before execution.

\- Ensure files have not changed since analysis.

\- All rename operations must pass through the Transaction Manager.

\- Record all operations in History.

\- Implement best-effort rollback when an operation fails.



\## 17. UI States



\### Initial State



When no analysis exists:

\- Display the file or folder selection form.

\- Display naming strategies.

\- Do not show dummy data.



\### Analyzing



Display job progress and the number of files analyzed.



\### Analysis Completed



Display summary cards and Rename Preview.



\### No Changes



If all files already comply with the selected rules, display a message indicating that no renaming is required.



\### Conflict



Display conflicting files and provide resolution options.



\### Error



Display an understandable error message and retry option.



\### Partial Failure



Display successfully analyzed files separately from files that failed processing.



\## 18. Acceptance Criteria



\- \[ ] Smart Rename sidebar item is active.

\- \[ ] Users can select a folder or individual files.

\- \[ ] File selection is restricted to Managed Folders.

\- \[ ] Three naming strategies are available.

\- \[ ] Custom patterns support variables.

\- \[ ] All options work according to their configuration.

\- \[ ] Analyze \& Preview Rename creates a background job.

\- \[ ] Summary Cards use actual analysis data.

\- \[ ] Rename Preview displays current and proposed names.

\- \[ ] Users can edit proposed names.

\- \[ ] Search, filters, and pagination work.

\- \[ ] Checkboxes support file selection.

\- \[ ] Backend validates names and collisions.

\- \[ ] Save Plan only saves a draft.

\- \[ ] Review Changes opens the approval workflow.

\- \[ ] Rename Rules can be managed.

\- \[ ] Approved Rules operate only within their approved scope.

\- \[ ] History records all activities.

\- \[ ] All renaming operations pass through the Transaction Manager.

\- \[ ] No overwrite or direct AI-driven rename is possible.



\## 19. Design Reference



Use `image-1` as the visual reference for the Smart Rename page.



Requirements:

\- Maintain the visual language of previous pages.

\- Use navy for the sidebar.

\- Use blue as the primary accent color.

\- Place the configuration panel on the left.

\- Place Analysis Result and Rename Preview on the right.

\- The table must display current name, proposed name, reason, and status.

\- Use visual indicators for Rename, No Change, and Conflict.

\- Maintain a professional, utility-focused appearance.

\- Do not make a chatbot the primary interface.



If the visual reference conflicts with behavioral specifications, this README is the authoritative implementation contract.

