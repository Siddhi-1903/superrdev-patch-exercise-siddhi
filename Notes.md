# Patch Notes

## Summary

I focused on high-impact issues affecting correctness, performance,
error handling, and user experience.

## Fixes

### 1. Search/Status/Archived Filtering
Fixed incorrect AND/OR precedence in task search filtering.
Search now correctly applies archived, title/description, and
status conditions. Updated the Spring Data repository, H2 SQL
reference, and Oracle reference query.

### 2. Artificial API Delay
Removed the artificial `Thread.sleep()` delay and unused
`complexityScore` calculation from `TaskController`. This prevents
unnecessary blocking of the HTTP request thread.

### 3. Frontend Loading State
Fixed the loading state after API failures. The request now uses
`finally()` to ensure loading is reset whether the request succeeds
or fails, allowing the error message to be displayed.

### 4. Pagination Reset
Reset pagination to page 1 whenever the search query or status
filter changes. This prevents stale page numbers from producing
empty results.

### 5. Invalid Status Handling
Handled invalid status values using `try/catch`. Invalid values now
return HTTP 400 Bad Request with a message describing the allowed
statuses instead of causing an unhandled exception.

## Remaining Risk

Pagination is currently performed in memory after retrieving all
matching records. Database-level pagination would scale better for
large datasets. I left this unchanged within the exercise timebox
because it would require a broader repository/pagination redesign.

## Validation

Tested search, status filtering, combined filtering, pagination,
filter pagination reset, invalid status handling, and API failure
handling.

## AI Usage

Used GenAI for code inspection, debugging ideas, and reviewing
potential fixes. I verified the changes through code inspection
and manual testing.