\# Feature 10 — Settings



\## 1. Overview



Settings provides a centralized interface for configuring application behavior, AI integration, organization preferences, monitoring, security, storage, and database maintenance.



Users can customize how FileNest operates while maintaining filesystem safety, privacy, and application stability.



\### Goals



\- Configure general application preferences.

\- Manage startup and background behavior.

\- Configure AI and model gateway integration.

\- Manage organization and rename defaults.

\- Configure filesystem monitoring.

\- Manage security and access restrictions.

\- Configure storage and database behavior.

\- View application information and perform maintenance.



\## 2. Layout



The page follows the application's main layout:



1\. Sidebar Navigation

2\. Page Header

3\. Settings Category Tabs

4\. Settings Navigation Panel

5\. Settings Content Panel

6\. Information and Maintenance Panel

7\. Save Actions



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



The Settings menu must be active.



\### Page Header



Title: `Settings`



Description: `Configure FileNest, manage features, and customize how the application works.`



\## 3. Settings Categories



Provide seven main categories:



1\. General

2\. Analysis \& AI

3\. Organization

4\. Monitoring

5\. Security \& Access

6\. Storage \& Database

7\. About



Each category contains its own settings navigation and content.



Settings must be grouped logically. Do not place unrelated configurations in the same section.



\## 4. General Settings



The General category contains:



1\. Application

2\. Startup \& Behavior

3\. User Interface

4\. Language

5\. Notifications

6\. Updates



\### 4.1 Application



Configure basic application information and paths.



Fields:



\*\*Application Name\*\*

\- Display the application name.

\- Read-only unless application renaming is explicitly supported.



\*\*Default Workspace\*\*

\- Set the application's workspace directory.

\- Use a native folder picker.



\*\*Download Location\*\*

\- Set the default location for exported reports and downloaded files.

\- Use a native folder picker.



\*\*Temp Location\*\*

\- Set the temporary processing directory.

\- Use a native folder picker.



Path validation:

\- Verify that the selected directory exists or can be created.

\- Check read and write permissions.

\- Do not allow unsafe system locations.

\- Changing a directory must not automatically move existing application data.

\- Clearly explain whether a setting requires an application restart.



\### 4.2 Startup \& Behavior



Provide:



\*\*Start on Windows Startup\*\*

\- Start FileNest when Windows starts.

\- Use Windows startup integration through Tauri.



\*\*Run in Background\*\*

\- Keep background services running when the main window is closed.



\*\*Minimize to System Tray\*\*

\- Minimize the application to the system tray instead of exiting.



\*\*Restore Last Opened Page\*\*

\- Restore the last selected application page on startup.



\*\*Ask Before Exiting\*\*

\- Display confirmation when closing the application while background jobs are running.



\*\*Start Monitoring on Launch\*\*

\- Restore eligible monitoring watchers when the application starts.



\### 4.3 User Interface



Provide:



\*\*Theme\*\*

\- Light

\- Dark

\- System Default



\*\*Sidebar Behavior\*\*

\- Expanded

\- Collapsed

\- Remember Last State



\*\*Default File View\*\*

\- List

\- Grid



\*\*Default Table Density\*\*

\- Comfortable

\- Compact



\*\*Show File Extensions\*\*

\- Show or hide file extensions in the Files interface.



\*\*Show Hidden Files\*\*

\- Configure whether hidden files are visible in the file manager.



Display preferences must not override backend access restrictions.



\### 4.4 Language



Provide:

\- Application Language

\- Date Format

\- Time Format

\- Number Format



The language selector should initially support the languages actually implemented by the application.



Do not display unsupported languages as available options.



\### 4.5 Notifications



Provide:



\*\*Desktop Notifications\*\*

\- Enable or disable Windows notifications.



\*\*Job Notifications\*\*

\- Notify when analysis jobs finish.

\- Notify when execution jobs finish.

\- Notify when jobs fail.



\*\*Monitoring Notifications\*\*

\- Notify when configured monitoring rules trigger.

\- Notify when a watcher fails.



\*\*Notification Sound\*\*

\- Enable or disable notification sounds.



\*\*Do Not Disturb\*\*

\- Configure a notification quiet period.



Notifications must not expose sensitive file content.



\### 4.6 Updates



Display:

\- Current Version

\- Installed Build

\- Update Channel

\- Last Update Check

\- Available Update



Actions:

\- Check for Updates

\- View Release Notes

\- Configure Update Channel



Only implement update installation when a trusted update mechanism is available.



Do not execute arbitrary update packages.



\## 5. Analysis \& AI Settings



The Analysis \& AI category contains:



1\. AI Provider

2\. Hermes Integration

3\. 9Router Connection

4\. Model Configuration

5\. Analysis Preferences

6\. Privacy \& Data Processing



\### 5.1 AI Provider



Display the configured AI architecture:



\- AI Orchestrator: Hermes

\- Model Gateway: 9Router



Hermes handles task orchestration.



9Router provides access to configured models.



Do not introduce alternative AI providers unless explicitly supported by the project requirements.



\### 5.2 Hermes Integration



Fields:

\- Hermes Endpoint

\- Connection Status

\- Authentication Configuration, if required

\- Request Timeout

\- Maximum Concurrent Tasks



Actions:

\- Test Connection

\- Save Configuration

\- View Integration Details



Display:

\- Connected

\- Disconnected

\- Error

\- Not Configured



Connection testing must not start filesystem operations.



Do not assume Hermes API paths or authentication formats. Verify the actual installed Hermes version and configuration.



\### 5.3 9Router Connection



Fields:

\- 9Router Endpoint

\- API Key

\- Connection Status

\- Request Timeout



The API key must be masked by default.



Actions:

\- Show / Hide API Key

\- Test Connection

\- Save Configuration



Display connection errors in a readable format.



Store credentials using Windows Credential Manager or another appropriate secure storage mechanism.



Never store API keys in plaintext SQLite records or frontend source code.



\### 5.4 Model Configuration



Allow users to configure models available through 9Router.



Fields:

\- Default Model

\- Analysis Model

\- Vision Model, if supported

\- Maximum Tokens

\- Temperature

\- Request Timeout



Model selection should be populated from available configured models where supported.



Do not invent model identifiers.



\### 5.5 Analysis Preferences



Provide:



\*\*Default Analysis Mode\*\*

\- Metadata Only

\- Deep AI Analysis



\*\*Maximum Concurrent Analysis Jobs\*\*

\- Configure the number of concurrent jobs.



\*\*Analyze File Content\*\*

\- Allow content extraction for supported file types.



\*\*Analyze Images\*\*

\- Allow visual image analysis when supported by the configured model.



\*\*Analyze Documents\*\*

\- Allow document text extraction for supported formats.



\*\*Maximum File Size\*\*

\- Configure the maximum file size eligible for content extraction.



These settings must be respected by every analysis feature.



\### 5.6 Privacy \& Data Processing



Provide:



\*\*Allow Remote AI Processing\*\*

\- Enable or disable sending eligible information to models through 9Router.



\*\*Metadata Only\*\*

\- Restrict AI processing to file names and metadata.



\*\*Content Extraction\*\*

\- Allow selective document and image content extraction.



\*\*Sensitive Folder Exclusions\*\*

\- Exclude selected Managed Folders from content processing.



\*\*Sensitive File Exclusions\*\*

\- Exclude selected file extensions or patterns.



Clearly explain which data may leave the local machine.



If remote AI processing is disabled, AI features that require remote models must be unavailable or use a supported local model configuration.



\## 6. Organization Settings



The Organization category contains:



1\. Default Strategy

2\. Folder Structure

3\. Approved Rules

4\. Conflict Handling



\### 6.1 Default Strategy



Provide:

\- Organize by File Type

\- Organize by Project Structure

\- Custom



Set the default strategy for new organization plans.



\### 6.2 Folder Structure



Configure:

\- Default Folder Naming Convention

\- Number Prefix

\- Separator

\- Capitalization

\- Default Archive Folder Name



Example:

\- `01\_Documents`

\- `02\_Images`

\- `03\_Videos`

\- `04\_Archive`



These preferences apply only to newly generated recommendations.



They must not modify existing folders automatically.



\### 6.3 Approved Rules



Display:

\- Default Execution Mode

\- Require Approval for New Rules

\- Enable Approved Rule Automation



Automation must remain restricted to each rule's previously approved scope.



Changing the execution scope requires renewed approval.



\### 6.4 Conflict Handling



Provide:

\- Detect Destination Conflicts

\- Suggest Alternative Folder

\- Add Number Sequence

\- Send Ambiguous Operations to Review Changes



Never enable silent overwrite.



\## 7. Monitoring Settings



The Monitoring category contains:



1\. General

2\. Watcher Configuration

3\. Event Processing

4\. Notifications

5\. Exclusions



\### 7.1 General



Provide:

\- Enable Monitoring

\- Start Monitoring on Application Startup

\- Run Monitoring in Background



\### 7.2 Watcher Configuration



Provide:

\- Recursive Monitoring

\- Watcher Recovery on Startup

\- Watcher Health Check Interval



These settings must respect each Managed Folder's individual configuration.



\### 7.3 Event Processing



Provide:

\- Event Debounce Interval

\- Event Deduplication

\- Maximum Event Queue Size

\- Event Processing Batch Size



Use safe defaults.



Validate all numeric values.



\### 7.4 Notifications



Provide:

\- File Created

\- File Modified

\- File Deleted

\- Folder Changed

\- Watcher Error

\- Rule Triggered



Users may configure which events generate desktop notifications.



\### 7.5 Exclusions



Allow users to configure global monitoring exclusions.



Examples:

\- Temporary file extensions.

\- Cache directories.

\- Temporary filename patterns.



Managed Folder-specific exclusions must remain configurable through Managed Folders.



Global exclusions must never expand the application's filesystem access scope.



\## 8. Security \& Access Settings



The Security \& Access category contains:



1\. Application Security

2\. Filesystem Restrictions

3\. Approval \& Automation

4\. Credential Management

5\. Privacy



\### 8.1 Application Security



Provide:

\- Require Confirmation Before Execution

\- Require Confirmation Before Removing Managed Folders

\- Lock Settings Changes

\- Automatic Lock After Inactivity, if supported



\### 8.2 Filesystem Restrictions



Display read-only security policies:



\- Only Managed Folders Are Accessible

\- Backend Path Validation

\- Protected Windows Directories

\- Symbolic Link Restrictions

\- Junction and Reparse Point Restrictions

\- Transaction Manager Required



These are mandatory security constraints.



Users must not be able to disable core filesystem safety controls through the Settings interface.



\### 8.3 Approval \& Automation



Provide:

\- Require Approval for Manual Plans

\- Enable Approved Rules

\- Require Reapproval When Rule Scope Changes

\- Require Final Confirmation Before Execution



These options must not weaken the mandatory approval rules defined by the application architecture.



\### 8.4 Credential Management



Manage stored integration credentials.



Display:

\- Credential Provider

\- Hermes Credential Status

\- 9Router Credential Status

\- Last Updated



Actions:

\- Update Credential

\- Remove Credential

\- Test Connection



Never display complete stored secrets.



\### 8.5 Privacy



Provide:

\- Remote AI Processing Consent

\- Content Extraction Consent

\- Anonymous Usage Reporting, if implemented

\- Crash Reporting, if implemented



All optional data sharing must be disabled by default unless the user explicitly enables it.



\## 9. Storage \& Database Settings



The Storage \& Database category contains:



1\. Database

2\. Application Storage

3\. Cache

4\. Maintenance

5\. Backup \& Restore



\### 9.1 Database



Display:

\- Database Engine

\- Database Location

\- Database Size

\- Database Version

\- Last Migration

\- Database Health



Actions:

\- Open Database Location

\- Check Database Integrity

\- Compact Database



Database operations must be performed through the backend.



\### 9.2 Application Storage



Display storage usage for:

\- Database

\- Cache

\- Logs

\- Temporary Files

\- Exported Reports



Display:

\- Used Space

\- Total Application Storage



Allow users to configure:

\- Workspace Location

\- Export Location

\- Temporary Directory



\### 9.3 Cache



Display:

\- Total Cache Size

\- File Scan Cache

\- Analysis Cache

\- Thumbnail Cache



Actions:

\- Clear All Cache

\- Clear Selected Cache



Clearing cache must not delete user files, Managed Folders, analysis history, or audit records.



\### 9.4 Maintenance



Provide:



\*\*Compact Database\*\*

\- Optimize SQLite database storage.

\- Require confirmation.

\- Ensure no conflicting database operations are running.



\*\*Clear Application Cache\*\*

\- Remove eligible temporary and cached data.

\- Preserve persistent application data.



\*\*Open Log Folder\*\*

\- Open the application log directory in Windows Explorer.



\*\*Check Database Integrity\*\*

\- Run an SQLite integrity check.

\- Display the result.



\*\*Run Database Migration\*\*

\- Run pending Alembic migrations through the backend.

\- Require appropriate backup and error handling.



\### 9.5 Backup \& Restore



Provide:

\- Create Backup

\- Choose Backup Location

\- Restore Backup

\- View Backup History



Backups should include the necessary application database and configuration data.



Credentials stored in Windows Credential Manager must be handled separately.



Before restoring:

\- Validate the backup format.

\- Verify application compatibility.

\- Create a safety backup of the current database.

\- Require explicit user confirmation.



Never silently overwrite current application data.



\## 10. About



The About category displays:



\### Application Information



\- Application Name

\- Version

\- Build Number

\- Release Channel

\- Build Date



\### Components



Display installed component information:

\- Tauri

\- React

\- Python Backend

\- Hermes

\- 9Router

\- SQLite



Only display actual detected versions.



\### Links



Provide:

\- Documentation

\- Release Notes

\- Support Information

\- License Information



Do not invent external support URLs.



\## 11. Save Behavior



Settings should support both immediate and deferred persistence depending on their category.



\### Save Changes



For settings that require explicit saving:

1\. User modifies values.

2\. Frontend validates input.

3\. User clicks Save Changes.

4\. Backend validates the configuration.

5\. Persist settings.

6\. Apply changes where possible.

7\. Display success or failure feedback.



\### Reset to Default



Restore default values for the current settings section.



Behavior:

\- Display confirmation.

\- Do not reset unrelated categories.

\- Show the values that will be changed.

\- Persist only after confirmation.



\### Unsaved Changes



If users navigate away with unsaved changes:

\- Display a confirmation dialog.

\- Provide Save, Discard, and Cancel actions.



\### Settings Validation



\- Validate paths.

\- Validate URLs.

\- Validate numeric ranges.

\- Validate model configuration.

\- Validate connection settings.

\- Validate conflicting options.



Never persist invalid configuration.



\## 12. API Requirements



The API must support at least the following operations.



\### Get Settings



`GET /api/settings`



Returns application settings grouped by category.



\### Update Settings



`PATCH /api/settings`



Updates supported settings.



\### Reset Settings



`POST /api/settings/reset`



Request:

\- category



Resets only the specified category.



\### Test Hermes Connection



`POST /api/settings/ai/hermes/test`



Tests the configured Hermes connection.



\### Test 9Router Connection



`POST /api/settings/ai/9router/test`



Tests the configured 9Router connection.



\### Get Available Models



`GET /api/settings/ai/models`



Returns available models from the configured gateway when supported.



\### Get Storage Information



`GET /api/settings/storage`



Returns application storage usage.



\### Check Database Integrity



`POST /api/settings/database/integrity-check`



Runs an integrity check.



\### Compact Database



`POST /api/settings/database/compact`



Starts a database maintenance job.



\### Clear Cache



`POST /api/settings/cache/clear`



Request:

\- cache\_types



Clears selected cache categories.



\### Create Backup



`POST /api/settings/backup`



Creates an application backup.



\### Restore Backup



`POST /api/settings/restore`



Starts a validated restore operation after confirmation.



These endpoints are proposed API contracts. Adapt them to the existing backend conventions.



\## 13. Data Requirements



\### Application Settings



\- id

\- category

\- setting\_key

\- setting\_value

\- updated\_at



\### AI Configuration



\- id

\- provider\_type

\- endpoint

\- model\_configuration

\- timeout

\- updated\_at



Secrets must be stored outside ordinary SQLite settings records.



\### Monitoring Configuration



\- id

\- configuration

\- updated\_at



\### Storage Configuration



\- id

\- workspace\_path

\- download\_path

\- temp\_path

\- updated\_at



\### Backup Record



\- id

\- backup\_path

\- backup\_size

\- backup\_status

\- created\_at

\- completed\_at



Store configuration values in structured formats with validation.



Do not store credentials or API keys in plaintext database fields.



\## 14. Technical Requirements



\- Use React and TypeScript for the settings interface.

\- Use FastAPI for configuration APIs.

\- Use SQLite and SQLAlchemy for persistent settings.

\- Use Alembic for database schema migrations.

\- Use Tauri 2 APIs for native folder dialogs and Windows integration.

\- Use secure credential storage for API keys.

\- Validate configuration on both frontend and backend.

\- Keep settings grouped by category.

\- Support application restart when a setting requires it.

\- Record security-relevant configuration changes in History.

\- Do not expose backend secrets to frontend logs.

\- Avoid restarting active jobs unexpectedly when applying settings.



\## 15. Safety Constraints



\- Core filesystem safety policies cannot be disabled.

\- Only registered Managed Folders may be accessed.

\- Never store API keys in plaintext SQLite records.

\- Never expose complete credentials in the UI.

\- Remote AI processing must respect privacy settings.

\- Content extraction must respect user consent and exclusions.

\- Database maintenance must protect persistent application data.

\- Cache cleanup must not remove user files or audit records.

\- Backup restoration must require explicit confirmation.

\- Configuration changes affecting approved rule scope must require renewed approval.

\- Record relevant settings changes in History.



\## 16. UI States



\### Initial State



Load the saved settings from the backend.



Do not display hardcoded values as if they were persisted configuration.



\### Loading



Display skeletons for settings panels and information cards.



\### Unsaved Changes



Display a clear indicator when configuration has been modified but not saved.



\### Saving



Disable conflicting actions while the current settings are being saved.



\### Saved



Display a success message and update the last-saved timestamp.



\### Validation Error



Display the error next to the corresponding setting.



\### Connection Error



Display connection status and a readable error message.



\### Maintenance Running



Display progress for database maintenance, cache cleanup, backup, or restore jobs.



\### Restart Required



Display a notice when an applied setting requires an application restart.



\## 17. Acceptance Criteria



\- \[ ] Settings has an active sidebar item.

\- \[ ] Seven settings categories are available.

\- \[ ] General settings can be configured.

\- \[ ] Startup and background behavior can be configured.

\- \[ ] User interface preferences are persisted.

\- \[ ] Language options reflect implemented translations.

\- \[ ] Notification preferences work.

\- \[ ] Hermes connection can be tested.

\- \[ ] 9Router connection can be tested.

\- \[ ] Available models are retrieved when supported.

\- \[ ] Analysis preferences are persisted.

\- \[ ] Privacy and content extraction settings are respected.

\- \[ ] Organization defaults can be configured.

\- \[ ] Monitoring settings are persisted.

\- \[ ] Security settings expose mandatory restrictions clearly.

\- \[ ] Credentials are stored securely.

\- \[ ] Database information is displayed accurately.

\- \[ ] Cache can be cleared safely.

\- \[ ] Database integrity checks work.

\- \[ ] Database compaction is protected against conflicting operations.

\- \[ ] Backup and restore workflows require confirmation.

\- \[ ] Settings can be reset by category.

\- \[ ] Unsaved changes are handled correctly.

\- \[ ] Invalid settings are rejected by the backend.

\- \[ ] Relevant configuration changes are recorded in History.



\## 18. Design Reference



Use `image-1` as the visual reference for the Settings page.



Requirements:

\- Maintain the visual language of previous application pages.

\- Use navy for the sidebar.

\- Use blue as the primary accent color.

\- Display category tabs near the top.

\- Use a secondary settings navigation panel on the left.

\- Place the selected settings content in the center.

\- Use a right-hand information and maintenance panel where appropriate.

\- Keep Save Changes and Reset to Default accessible.

\- Use consistent form controls, toggles, and section dividers.

\- Maintain a professional, utility-focused interface.

\- Avoid unnecessary decorative AI elements.



If the visual reference conflicts with behavioral specifications, this README is the authoritative implementation contract.

