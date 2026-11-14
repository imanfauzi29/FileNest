# Feature 08 — History

## 1. Overview

History provides a centralized audit log of all activities performed by the application.

It records filesystem events, analysis activities, plans, approvals, executions, monitoring events, rule changes, and system events.

Users can search, filter, inspect, and export historical activity records.

History is an audit interface. It must not directly modify filesystem contents.

### Goals

- Centralize application activity records.
- Track filesystem changes.
- Track AI analysis and generated plans.
- Track user approvals and rejections.
- Track Transaction Manager executions.
- Track monitoring activities.
- Track rule and settings changes.
- Provide detailed audit information.
- Support activity filtering and export.

## 2. Layout

The page follows the application's main layout:

1. Sidebar Navigation
2. Page Header
3. Activity Tabs
4. Summary Cards
5. Activity Charts
6. Activity Logs
7. Activity Details Panel

### Sidebar

Menu:
- Overview
- Files
- Storage
- Organization
- Smart Rename
- Review Changes
- Monitoring
- History
- Managed Folders
- Settings

The History menu must be active.

### Page Header

Title: `History`

Description: `View and audit all activities, changes, approvals, executions, and system events.`

Components:
- Total Records
- Refresh
- Export History
- Export Dropdown

Refresh retrieves existing records from the database. It must not trigger filesystem scanning or analysis.

Export History exports records according to the currently selected filters.

Dropdown options:
- Export CSV
- Export JSON

## 3. Activity Tabs

Provide seven tabs:

1. All Activities
2. File Changes
3. Plans & Approvals
4. Executions
5. Monitoring
6. Rules
7. System

### All Activities

Displays all activity categories in chronological order.

### File Changes

Displays filesystem-related events:
- File Created
- File Modified
- File Renamed
- File Moved
- File Copied
- File Deleted
- Folder Created
- Folder Renamed
- Folder Moved
- Folder Deleted

### Plans & Approvals

Displays:
- Analysis Started
- Analysis Completed
- Plan Created
- Plan Updated
- Plan Saved
- Plan Approved
- Plan Rejected
- Plan Cancelled

### Executions

Displays Transaction Manager activity:
- Execution Started
- Operation Started
- Operation Completed
- Operation Failed
- Execution Completed
- Execution Partially Completed
- Execution Cancelled
- Rollback Started
- Rollback Completed
- Rollback Failed

### Monitoring

Displays:
- Monitoring Started
- Monitoring Paused
- Monitoring Resumed
- Monitoring Stopped
- Watcher Created
- Watcher Removed
- Monitoring Event Detected
- Monitoring Error

### Rules

Displays:
- Rule Created
- Rule Updated
- Rule Approved
- Rule Paused
- Rule Enabled
- Rule Disabled
- Rule Deleted
- Rule Executed

### System

Displays:
- Application Started
- Application Stopped
- Background Job Started
- Background Job Completed
- Background Job Failed
- Database Migration
- Configuration Updated
- Service Error

## 4. Summary Cards

Display six summary cards.

### Total Activities

Displays the total number of recorded activities.

### Completed

Displays the number of successfully completed activities or operations.

### Executing

Displays the number of currently running executions.

### Failed

Displays the number of failed activities or operations.

### File Changes

Displays the number of recorded filesystem change events.

### Last 24 Hours

Displays the total number of activities recorded within the last 24 hours.

All values must come from actual database records.

Clicking a summary card should apply its corresponding filter.

Do not combine activity records and individual operation records in a way that produces misleading counts. Clearly define whether each metric counts jobs, activities, or operations.

## 5. Activity Trend

Display a line chart showing activity volume over time.

### Time Range

Provide:
- Last 24 Hours
- Last 7 Days
- Last 30 Days
- Last 90 Days
- All Time

### Chart Behavior

- Display activity counts on the vertical axis.
- Display time intervals on the horizontal axis.
- Show detailed counts on hover.
- Update the chart when the time range changes.
- Support empty and loading states.

Use persisted activity records.

Do not generate historical data that does not exist.

## 6. Activity by Type

Display a donut chart showing activity distribution.

Categories:
- File Change
- Plan & Approval
- Execution
- Monitoring
- System

Display:
- Category Name
- Activity Count
- Percentage
- Total Activities

Hovering over a category displays its detailed count and percentage.

Clicking a category filters Activity Logs.

## 7. Activity Logs

Activity Logs is the main working area of the History page.

### Search

Provide search by:
- File name
- Folder path
- Activity description
- Activity ID
- Plan ID
- Execution Batch ID

### Filters

Provide:
- All Types
- All Sources
- All Status

Activity type filters:
- File Changes
- Plans & Approvals
- Executions
- Monitoring
- Rules
- System

Time filters:
- Last Hour
- Last 24 Hours
- Last 7 Days
- Last 30 Days
- Custom Range

Status filters:
- Completed
- Executing
- Failed
- Rejected
- Cancelled
- Partially Completed

Source filters:
- Files
- Storage
- Organization
- Smart Rename
- Review Changes
- Monitoring
- Settings
- System

### Table Columns

- Number
- Time
- Activity
- Description
- Source
- User
- Status

### Activity Description

Examples:
- `login-screen.jpg` created.
- `IMG_001.JPG` renamed to `login-screen.jpg`.
- Execution started for plan `RP-2025-001`.
- Rename plan approved.
- Monitoring started for a Managed Folder.
- Organization rule updated.

Descriptions should be concise and understandable.

### User

Display the actor responsible for the activity.

Possible values:
- User account identifier
- System
- Background Worker
- Rule Engine

Do not expose sensitive credentials or personal secrets.

### Status

Supported statuses:
- Completed
- Executing
- Failed
- Rejected
- Cancelled
- Partially Completed
- Information

Use consistent status indicators.

### Pagination

Provide:
- Rows per page: 10, 25, 50, 100
- First Page
- Previous Page
- Next Page
- Last Page

Display the current range and total record count.

Use server-side pagination for large activity datasets.

## 8. Activity Details Panel

When a user selects an activity, display its complete details in the right-hand panel.

### General Information

- Activity ID
- Activity Type
- Source
- User
- Timestamp
- Status
- Description

### Related Information

Depending on the activity type, display:
- Managed Folder ID
- File ID
- Plan ID
- Execution Batch ID
- Watcher ID
- Rule ID
- Related Change IDs

Hide fields that are not relevant to the selected activity.

### Execution Details

For execution-related activities, display:
- Execution Batch ID
- Total Operations
- Completed Operations
- Failed Operations
- Skipped Operations
- Progress
- Start Time
- Completion Time

### Related Files

Provide a link to view related operations or files when available.

Do not assume a file still exists when viewing historical records.

### Actions

Provide contextual actions:
- View Plan
- View Related Changes
- View Execution
- View Monitoring Event
- Open File Location

Only display actions supported by the selected record.

For deleted or unavailable files, Open File Location must be disabled.

History actions must never modify the underlying filesystem.

## 9. Execution Log

For activities associated with execution batches, provide a detailed execution timeline.

Example stages:
1. Validate Plan
2. Execute Operations
3. Finalize and Update History

Each stage displays:
- Stage Name
- Status
- Started At
- Completed At
- Error Details

Individual operations should be accessible from View Operations.

### Operation Status

- Pending
- Running
- Completed
- Failed
- Skipped
- Rolled Back

The execution timeline must reflect actual Transaction Manager records.

Do not display estimated completion stages as completed.

## 10. Export History

Export History allows users to export historical records.

### Export Formats

- CSV
- JSON

### Export Scope

Export based on:
- Selected Activity Tab
- Current Search
- Current Filters
- Selected Date Range

### Export Behavior

- CSV must contain readable tabular records.
- JSON must preserve structured activity information.
- Use UTF-8 encoding.
- Include timestamps in a consistent format.
- Do not export credentials, secrets, or sensitive configuration values.
- Display export progress for large datasets.

Exporting history must not modify or delete stored records.

## 11. Activity Retention

History records must be retained according to application retention settings.

Requirements:
- Do not automatically remove recent audit records.
- Retention policy must be configurable.
- Preserve execution and approval audit records according to the configured policy.
- Any cleanup operation must be explicitly configured and recorded.
- Do not allow ordinary activity filtering to delete records.

## 12. API Requirements

The API must support at least the following operations.

### Get Activities

`GET /api/history/activities`

Query parameters:
- activity_type
- source
- status
- search
- start_date
- end_date
- page
- page_size

Returns paginated activity records.

### Get Activity Details

`GET /api/history/activities/{activity_id}`

Returns full activity details and related record references.

### Get History Summary

`GET /api/history/summary`

Returns activity summary metrics.

### Get Activity Trend

`GET /api/history/trend`

Query parameters:
- range
- interval

Returns activity counts grouped by time interval.

### Get Activity Distribution

`GET /api/history/distribution`

Returns activity counts grouped by category.

### Get Execution Details

`GET /api/history/executions/{batch_id}`

Returns execution details and timeline.

### Get Related Operations

`GET /api/history/executions/{batch_id}/operations`

Returns individual operation records.

### Export History

`POST /api/history/export`

Request:
- format
- filters
- date_range

Returns an export job or generated file reference.

These endpoints are proposed API contracts. Adapt them to the existing backend conventions.

## 13. Data Requirements

### Activity Log

- id
- activity_type
- source
- actor_type
- actor_id
- description
- status
- managed_folder_id
- related_entity_type
- related_entity_id
- metadata
- occurred_at
- created_at

### Activity Relation

- id
- activity_id
- related_type
- related_id

### Execution Log

- id
- batch_id
- stage
- status
- message
- error_details
- started_at
- completed_at

### Export Job

- id
- export_format
- filter_configuration
- status
- file_reference
- created_at
- completed_at

Use structured metadata where appropriate.

Avoid storing duplicate copies of large file content or sensitive information in activity records.

## 14. Technical Requirements

- Use SQLite for persistent activity records.
- Use SQLAlchemy for database access.
- Use Alembic for schema migrations.
- Record activities through a centralized backend audit service.
- Ensure filesystem operations generate corresponding audit records.
- Record approval and rejection actions.
- Record Transaction Manager execution results.
- Record monitoring events and configuration changes.
- Use server-side filtering and pagination.
- Use background jobs for large exports.
- Use consistent timestamps and timezone handling.
- Ensure audit records remain readable even when related files or plans are no longer available.

### Audit Consistency

For critical operations, audit records must be persisted reliably.

Where possible, record business state changes and their corresponding audit events in the same database transaction.

For filesystem operations, record the operation lifecycle and final result. Handle crashes or partial execution without incorrectly marking operations as completed.

## 15. Safety Constraints

- History is read-only.
- Do not modify filesystem contents from History.
- Do not delete audit records through ordinary UI actions.
- Do not expose secrets or credentials.
- Validate access to related records.
- Do not assume historical file paths still exist.
- Preserve the original event timestamp.
- Never fabricate execution status.
- Do not mark an operation completed unless its result has been verified.
- Record audit failures and handle them explicitly.

## 16. UI States

### Initial State

If no activities exist:
- Display an empty state.
- Explain that activities will appear as the application is used.
- Do not show dummy data.

### Loading

Display skeletons for:
- Summary Cards
- Activity Charts
- Activity Logs
- Activity Details

### No Results

When filters return no results:
- Display an appropriate message.
- Provide Clear Filters.

### Selected Activity

Display the selected record in the right-hand details panel.

### Executing

Show the current execution status and progress.

### Failed

Display the failure status and available error details.

### Exporting

Display export progress and the current export status.

### Error

Display an understandable error message and retry option where safe.

## 17. Acceptance Criteria

- [ ] History has an active sidebar item.
- [ ] Seven activity tabs are available.
- [ ] Summary Cards display actual records.
- [ ] Activity Trend supports different time ranges.
- [ ] Activity by Type displays actual category counts.
- [ ] Activity Logs supports search and filtering.
- [ ] Pagination works for large datasets.
- [ ] Activity Details displays relevant information.
- [ ] Related plans and executions can be opened.
- [ ] Execution Log displays actual execution stages.
- [ ] CSV export works.
- [ ] JSON export works.
- [ ] Export respects active filters.
- [ ] Activity records are persisted in SQLite.
- [ ] Filesystem operations generate audit records.
- [ ] Approval and rejection actions are recorded.
- [ ] Transaction Manager results are recorded.
- [ ] Monitoring events are recorded.
- [ ] Failed and partial executions are represented correctly.
- [ ] History cannot directly modify filesystem contents.
- [ ] Sensitive information is excluded from audit records and exports.

## 18. Design Reference

Use `image-1` as the visual reference for the History page.

Requirements:
- Maintain the visual language of previous application pages.
- Use navy for the sidebar.
- Use blue as the primary accent color.
- Display summary cards near the top.
- Place Activity Trend and Activity by Type above Activity Logs.
- Place Activity Details in the right-hand panel.
- Display execution timelines for execution-related records.
- Use clear status indicators.
- Maintain a professional, audit-focused interface.
- Avoid unnecessary decorative AI elements.

If the visual reference conflicts with behavioral specifications, this README is the authoritative implementation contract.