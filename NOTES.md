# Technical Exercise Notes

## Summary of Changes

### 1. Fixed SQL filter precedence
Updated `TaskRepository.java` so archived, search-term, and status filters are applied consistently. The title/description `OR` condition was missing grouping, which could cause incorrect results when filters were combined.

### 2. Removed artificial API delay
Updated `TaskController.java` to remove a query-length-based `Thread.sleep()`. The delay added unnecessary latency and blocked the request thread before the database query.

### 3. Added pagination input validation
Updated `TaskController.java` to reject invalid `page` and `pageSize` values below 1. Invalid pagination requests now return HTTP 400 instead of causing invalid list operations.

### 4. Fixed frontend loading and stale request handling
Updated `useTasks.js` so loading is cleared when an API request fails and older requests cannot overwrite newer results. Added cleanup checks and `finally` for reliable request state handling.

### 5. Added invalid status handling
Updated `TaskController.java` to handle invalid status values instead of allowing `TaskStatus.valueOf()` to throw an unhandled exception. Invalid values now return HTTP 400 with a clear error message.

### 6. Reset pagination when filters change
Updated `App.jsx` so changing the search term or status resets pagination to page 1. This prevents empty results when filtering from a later page. Verified by navigating to page 4 and then searching for `api`.

## What I Chose Not to Change

I avoided unrelated dependency, configuration, cosmetic, and architectural changes to keep the patch focused within the exercise timebox.

## Biggest Remaining Risk

The application has limited automated test coverage, so additional edge-case testing would be useful.

## Tools / AI Used

Used ChatGPT to inspect the code, identify potential issues, and reason about root causes. I reviewed and understood the suggested changes before applying and testing them.