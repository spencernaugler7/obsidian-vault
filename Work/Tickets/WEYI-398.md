---
summary: Implement Automated Cleanup for Old Report Files
created: 2026-09-29
source: https://cloudbreak.atlassian.net/browse/WEYI-398
---
## Description
We need to implement an automated cleanup process for previously generated report files under:
`C:\Work\WebSites\WEYIMobile\WEYIMgr\Report`
The cleanup should be implemented using a **PowerShell script** and scheduled through **Windows Task Scheduler**.
The purpose is to prevent old report files from accumulating and consuming unnecessary disk space.
## Requirements
- Create a PowerShell script to clean up old report files.
- Target directory: `C:\Work\WebSites\WEYIMobile\WEYIMgr\Report`
- The script should identify files based on their `CreateTime`.
- Automatically delete files that are **older than 3 days**.
- Files modified within the last 3 days must not be deleted.
- Configure the script to run automatically through **Windows Task Scheduler**.
- The cleanup should run at least once per day.
- The cleanup process should not interfere with the existing report generation process.
- The script should handle errors gracefully and provide sufficient logging for troubleshooting.
- The cleanup should only remove files from the specified Report directory and should not recursively delete files from unrelated directories.

## Acceptance Criteria
1. A PowerShell cleanup script is created and deployed to the appropriate server.
2. The script removes report files whose `CreateTime` is more than 3 days old.
3. Files less than or equal to 3 days old remain untouched.
4. A Windows Task Scheduler task is configured to execute the script automatically at least once per day.
5. The script does not interfere with report generation or access to recently generated reports.
6. Cleanup failures are logged and can be investigated if necessary.
7. The cleanup is limited to the specified `WEYIMgr\Report` directory.
8. The cleanup process is verified in the target environment with both old and recent report files.

# Questions
1. Delete files where the `CreateDate` and `LastWriteTime` is greater than or equal to three days
2. Target dir for reports. `C:\Work\WebSites\WEYIMobile\WEYIMgr\Report`
3. Where do I write log messages?
	1. We need the logs to be saved in a folder under the same path as the reports.