# Adding Accounting Validation Tests for RUS12 Yearly Balance Sheet Assets in PUDL

## Overview

PUDL (Public Utility Data Liberation) is an open-source project that makes energy data easier to access and use. I contributed to issue #5728, which focused on adding accounting validation tests for the RUS12 yearly balance sheet assets tables.

These tables needed additional checks to verify that their balance sheet components add up to their reported totals. I added dbt validation tests for both the core and output tables. During testing, I identified and corrected a component-name mismatch in the validation schemas. I then verified that all 14 targeted tests passed with no warnings or errors. I submitted my work in PR #5749, addressed a reviewer request, and pushed the update. The PR is currently awaiting further maintainer review

## What happened

After selecting issue #5728, I began setting up my development environment. My local Windows/WSL environment was unreliable, so I initially used GitHub Codespaces. Later, when a billing issue prevented me from starting another Codespace, I used GitHub Actions to run the validation workflow.

I investigated the issue by reviewing the existing PUDL schemas, documentation, and RUS12 data. I added dbt accounting validation tests for the core and output versions of the yearly balance sheet assets tables.

During an initial test run, the total_other_property_and_investments test reported 212 warnings. Rather than ignoring the warnings, I investigated the component names used in the dbt schemas and compared them with the transformed RUS12 data.

I found a naming mismatch: the validation schemas used non_utility_property_asset, while the transformed data used non_utility_property. I corrected the name in both dbt schema files and their corresponding human-readable schema input files. This aligned the validation definitions with the available transformed data.

After the correction, I reran the targeted validation tests against the published nightly Parquet data. The final GitHub Actions run reported:

Core table: 7 of 7 tests passed.
Output table: 7 of 7 tests passed.
Total: 14 passed, 0 warnings, 0 errors.

### Evidence 1: Schema correction and Validation tests code

Schema correction showing the component name change

evidence/schema-correction.PNG

Validation test code for RUS12 balance-sheet-asset 

evidence/RUS12-balance-sheet-asset-validation-tests.PNG

### Evidence 2: Successful dbt validation

I ran the RUS12 validation tests against the published nightly Parquet data using GitHub Actions.

- Core table: 7/7 tests passed
- Output table: 7/7 tests passed
- Total: **14 passed, 0 warnings, 0 errors**

**GitHub Actions run:** https://github.com/addisalem-aw/pudl/actions/runs/43806258098/job/133097623994#step:25:2

The workflow checked out the PR branch read-only. No changes were committed to the PR branch during testing.

## Limitations and what's next

My contribution focused on the accounting validation requested in issue #5728. I added checks for component totals, borrower foreign-key relationships, and row counts across reporting-year partitions. I verified the targeted tests against the published nightly Parquet data, but this result should not be interpreted as proof that the entire PUDL test suite passed.

The pull request is still awaiting maintainer review and approval. During the review process, I received a minor request and addressed it in an update to my PR.

This experience helped me improve my understanding of dbt tests, data validation, schema definitions, and debugging data-quality issues. I learned how important it is to investigate warnings, compare validation rules with actual data, and verify results instead of simply accepting the initial test output. I also gained practical experience working with an open-source project, responding to reviewer feedback, and maintaining a clear testing process.

During the review process, the reviewer encouraged me to contribute to another open issue as well. I appreciated this encouragement because it gave me confidence to continue participating in the PUDL community and expand my contributions beyond this issue. My next steps are to complete the review process for PR #5749 and, if time permits, select another suitable open issue, investigate it, and contribute a solution. I hope to continue learning from maintainers and other contributors while improving my technical skills through real-world open-source work.


