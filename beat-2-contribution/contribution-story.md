# Contribution: [VALIDATION] core_rus12__yearly_balance_sheet_assets and its out version

**Contribution Number:** [1]
**Student:** Addisalem Wordofa
**GitHub Username:** addisalem-aw
**Issue:** https://github.com/catalyst-cooperative/pudl/issues/5728
**Pull Request:** https://github.com/catalyst-cooperative/pudl/pull/5749

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull Request, includes a Toolkit block documenting the tools used, their outputs, difficulties, and resulting changes.

**Unit 5: Built and refined the issue-scout tool**

I installed and configured the issue-scout skill to search GitHub issues, rank potential contributions, and evaluate issues using a custom grading rubric.
My initial scans exposed weaknesses in my search strategy, including an incomplete fit profile and results that favored recently updated OpenAPI issues instead of my Java and Python backend interests.
I completed my fit profile, refined my search queries and ranking filters, and tested the rubric against OpenSearch Java issue #289.
Further evaluation showed that the issue depended on external application code and lacked recent maintainer confirmation, so I strengthened the reproducibility and newcomer-scope checks.
I then selected PUDL issue #5728 as my contribution opportunity and began preparing the repository in GitHub Codespaces.

**Unit 6: Tested a voice guard and created local PUDL repository memory**

I installed and tested the voice guard, whose logs showed that it intentionally stopped a help command with no readable body and blocked unsupported claims during both a manual test and a GitHub comment check.
I created PUDL's `CLAUDE.local.md` from the Unit 6 template, reviewed `CONTRIBUTING.rst` and the relevant RUS12 schema files manually because the `claude` command was unavailable in Codespaces, and documented the verified repository details.
I added the memory file to `.git/info/exclude` and confirmed that `git status --short` did not show it, keeping it out of the PR.

**Unit 7: Installed and configured the ship-gate for PUDL pre-PR checks**

I installed the ship-gate on Windows, configured its hook, and created a local ship manifest for `catalyst-cooperative/pudl`.
I configured four required checks: whitespace validation, dbt accounting tests, core asset validation, and output asset validation. I also documented broader test evidence, including 1,307 passing unit tests, 791 passing integration tests, and a successful documentation build.
The main difficulty was that PUDL does not support Windows (`win-64`), so the ship-gate could not execute the Pixi checks directly in my Windows clone. I used Linux GitHub Codespaces to execute the repository checks successfully.
The first ship-gate run rejected the contribution because the test evidence file did not document all the broader checks. I updated the evidence file and ran the gate again.
The final ship-gate returned **PASS**, and the PR precheck returned **accept**. I corrected the PR closing reference and reran the gate successfully before creating upstream PR #5749.

- **Tool:** Claude Code ship-gate, PR-precheck, GitHub CLI, GitHub Codespaces, and the local ship manifest.
- **What it produced:** A four-check ship manifest, documented test evidence, an accepted PR precheck, and a successful final ship-gate result.
- **Difficulties:** The Windows environment could not run PUDL's Pixi checks. The first gate run also identified missing evidence in `test_evidence.md`.
- **What changed:** I executed the checks in Codespaces, completed the evidence file, corrected the PR description, and passed the final ship-gate before submitting the upstream PR.

**Unit 8: Installed and used the PR monitor and playbook to manage PR #5749 through rebase and CI verification**

I used the PR monitor with my completed playbook to review PR #5749, checking its status, CI results, merge conflicts, and maintainer response history. The monitor drafted a suggested next move to rebase my branch onto upstream `main` and investigate the failing check. I reviewed the draft, resolved the `docs/release_notes.rst` conflict with Claude Code while preserving both upstream notes and my RUS12 entry, then continued the rebase and pushed using `--force-with-lease`. After the update, pre-commit CI passed and GitHub confirmed the PR is mergeable but awaiting maintainer review.

---

## Why I Chose This Issue

I used my issue-scout tool to search GitHub for open-source issues that matched my software development background and learning goals.
My initial scan evaluated five issues, and all five passed the required checks. The scout ranked LucasYanzy/httpeek#4 as the strongest fit because it was a Python project with offline tests and clear acceptance criteria.
However, the scan also exposed weaknesses: my fit profile was incomplete, several ranking filters could not be applied automatically, and the search favored very new issues with few comments.
I refined my search strategy and rubric and later selected PUDL issue #5728, which focuses on validating RUS-12 yearly balance-sheet assets and their output version.
I chose PUDL #5728 because it offers an opportunity to apply my programming and debugging experience while developing practical Python, data engineering, dbt, and data-validation skills. The issue has a defined validation goal and involves checking relationships between financial totals and their component values.
I also reviewed the repository's contribution guidance and AI-use policy, and the maintainer approved my request to work on the issue. I hope to learn how a large open-source data project organizes metadata, validation rules, and tests.
My scout was useful for finding and comparing opportunities, but its initial ranking did not fully reflect my fit profile. This showed me that search results and automated grades need human review.

**Claim comment:** https://github.com/catalyst-cooperative/pudl/issues/5728#issuecomment-6448160841

**Toolkit**

- **Tool:** Claude Code issue-scout skill, custom search strategy, fit profile, and grading rubric. I used them to search GitHub, compare candidate issues, and evaluate repository activity, scope, claim status, and AI policies.
- **What it produced:** Five accepted candidates in the initial scan, followed by selection of PUDL issue #5728 for my contribution.
- **Difficulties:** The initial fit profile was empty, some ranking filters could not be applied from search results, and ranking by fewest comments and recent updates favored very new repositories.
- **What changed:** I refined my search strategy and patched the scope check to better evaluate real-world issues. I also used human review and repository guidance before choosing PUDL.

## Understanding the Issue

**Problem Description**

PUDL issue #5728 requests adding accounting validation tests to `core_rus12__yearly_balance_sheet_assets` and `out_rus12__yearly_balance_sheet_assets`.
The task is to identify the financial calculations in the official USDA RUS Form 12 report, use the `is_total` metadata to identify reported totals, and add corresponding `subcomponents_sum_to_total` dbt data tests to both tables.
The objective is to improve data-quality monitoring by checking whether reported financial totals agree with their component values.

**Expected Behavior**

Both `core_rus12__yearly_balance_sheet_assets` and `out_rus12__yearly_balance_sheet_assets` should have accounting validation tests for the applicable financial calculations defined in the official USDA RUS Form 12 report.
The calculations should be identified using the Form 12 PDF and the `is_total` metadata column.
Each calculation should be implemented as a dbt `data_test` using PUDL's `subcomponents_sum_to_total` macro. The default tolerance should be 1 for most calculations and $10 for dollar values.
The corresponding human-readable schemas and generated schemas should be updated, and both tables should be validated.
When a validation test fails, the number of failing records should be identified and an `error_if` threshold configured so that an increase in failures raises an error. A high proportion of failing records should also be brought to the maintainers' attention because it may indicate a deeper data issue.
The objective is to monitor accounting inconsistencies, not to correct the underlying financial calculations as part of this issue.

**Current Behavior**

Before this contribution, the core and output RUS12 yearly balance-sheet assets tables had existing row-count and foreign-key checks, but did not have the requested accounting consistency tests.
After adding five accounting validation tests, four calculations passed, while the total other property and investments calculation reported 212 discrepancies in each table.
Further investigation confirmed that all 212 discrepancies matched the raw `NonUtilityPropertyNet` values within the $10 tolerance. The core diagnostic contained 779 borrower-year groups, so the 212 failures represent approximately 27.2% of those groups. This is a high proportion and should be highlighted to the maintainers.
The corresponding `non_utility_property_asset` category is absent from the transformed Parquet data because the existing transformer selects columns ending in `_assets`, while this column ends in singular `_asset`.
The transformer was left unchanged because correcting the transformation is outside the scope of this validation contribution.
I configured error_if: ">212" to flag increases above the 212 known discrepancies. I did not separately test the threshold-crossing behavior.

**Affected Components**

The following components were involved in the accounting validation work:

1. **Core validation schema:** `dbt/schema_inputs/rus12/core_rus12__yearly_balance_sheet_assets/schema.human.yml` — defines the five accounting validation tests for the core table.
2. **Output validation schema:** `dbt/schema_inputs/rus12/out_rus12__yearly_balance_sheet_assets/schema.human.yml` — defines the same five validation tests for the output table.
3. **Generated dbt schemas:**
   - `dbt/models/rus12/core_rus12__yearly_balance_sheet_assets/schema.yml`
   - `dbt/models/rus12/out_rus12__yearly_balance_sheet_assets/schema.yml`
   These contain the generated test definitions, including the `error_if: ">212"` threshold.
4. **Validation macro:** `dbt/macros/expect_subcomponents_sum_to_total.sql` — implements the accounting consistency checks by comparing the sum of specified components with the reported total.
5. **RUS12 transformer:** `src/pudl/transform/rus12.py` — contains `_core_rus12__yearly_balance_sheet_assets`, whose column-selection logic explains why `non_utility_property_asset` is missing.
6. **RUS12 column mapping:** `src/pudl/package_data/rus12/column_maps/balance_sheet.csv` — maps the raw `NonUtilityPropertyNet` field to `non_utility_property_asset`.
7. **RUS12 metadata:** `src/pudl/metadata/resources/rus12.py` — contains the RUS12 resource metadata, including the `is_total` field used to identify totals.

Only the four validation schema files were modified. The transformer, column mapping, metadata, and validation macro were inspected but left unchanged.

**Toolkit**

- **Tool:** GitHub Codespaces terminal, Pixi Python, pandas, Python `zipfile` and `csv` modules, grep, and dbt.
- **What it produced:** Identified the five accounting validation tests, traced the missing `non_utility_property_asset` category to the transformer logic, and verified that all 212 validation discrepancies matched the raw `NonUtilityPropertyNet` values within the $10 tolerance.
- **Difficulties:** The raw RUS12 CSV filenames changed between reporting years. My initial diagnostic found only 53 matches because it searched for the older `Form12` filename.
- **What changed:** I updated the diagnostic to search for the common `FinancialBalanceSheet.csv` filename pattern across all years. I confirmed all 212 matches and documented the transformer issue without changing the transformer code.

---

## Reproduction Process

**Environment Setup**

Repository: PUDL  
Branch: `issue-5728-rus12-assets-validation`  
Baseline commit: `b5794e99cbd95bf717d1fbb901172b6f87866b4e`  
Environment: Ubuntu 22.04 in GitHub Codespaces  
Pixi: 0.83.0  
Python: 3.14.10  
dbt: 1.12.6  
DuckDB adapter: 1.11.0  

The repository was set up in GitHub Codespaces because the PUDL development environment did not support my local Windows platform.

**Steps to Reproduce**

1. Obtain the nightly Parquet files from `s3://pudl.catalyst.coop/nightly/`.
2. Place the following files in `$PUDL_OUTPUT/parquet/`:
   - `core_rus12__yearly_balance_sheet_assets.parquet`
   - `out_rus12__yearly_balance_sheet_assets.parquet`
   - `core_rus12__entity_borrowers.parquet`
3. Run validation for the core asset:
   ```bash
   pixi run dbt_helper validate --asset-select 'key:core_rus12__yearly_balance_sheet_assets'
   ```
4. Run validation for the output asset:
   ```bash
   pixi run dbt_helper validate --asset-select 'key:out_rus12__yearly_balance_sheet_assets'
   ```

**Reproduction Evidence**

- **Commit showing reproduction:** https://github.com/catalyst-cooperative/pudl/issues/5728#issuecomment-6448160841

**My findings:**

Both validation commands completed successfully.

- Core asset: PASS=2, TOTAL=2
- Output asset: PASS=2, TOTAL=2
- Core borrower data contained 92 rows.
- Both yearly balance-sheet asset files contained 24,149 rows.

These results established the baseline validation environment. At this stage, the new `subcomponents_sum_to_total` accounting validation rules had not yet been implemented, so these baseline results did not establish whether the new accounting calculations would pass.
The initial foreign-key validation could not pass until the `core_rus12__entity_borrowers.parquet` file was added.
The repro-check skill returned an ACCEPT verdict, with all seven required rubric checks passing.

**Toolkit**

- **Tool:** repro-check skill and PUDL's `dbt_helper validate` commands.
- **What it produced:** A reproduction report for PUDL issue #5728. Both core and output asset validations passed their two existing checks.
- **Difficulties:** The initial foreign-key validation could not pass until the core borrower data was added. The exact nightly snapshot date and file-copy command were also missing from the initial report.
- **What changed:** I added the missing borrower data, reran both validations, documented the passing baseline results, and clarified that the new accounting validation rules had not yet been implemented or tested.

---

## Solution Approach

**Analysis**

The original issue is that the core and output RUS12 yearly balance-sheet assets tables were missing the requested accounting consistency validation tests.
During my investigation, I also identified a pre-existing data transformation issue that affects one of those validations.
In `src/pudl/package_data/rus12/column_maps/balance_sheet.csv`, the raw RUS12 field `NonUtilityPropertyNet` is mapped to `non_utility_property_asset`.
However, the `_core_rus12__yearly_balance_sheet_assets` function in `src/pudl/transform/rus12.py` selects columns using the regex:
```python
value_vars = list(df.filter(regex=r"_assets$").columns)
```
Because `non_utility_property_asset` ends in singular `_asset`, it is excluded from the transformation.
As a result, the `non_utility_property_asset` category is missing from the transformed balance-sheet data.
When the `subcomponents_sum_to_total` dbt macro checks `total_other_property_and_investments`, it sums the available components without this missing category, resulting in 212 validation failures in both the core and output tables.
The macro uses SQL `SUM()`, which ignores NULL values. Since the category is absent rather than represented as a component value, the sum includes the other available components but excludes non-utility property.
I investigated these discrepancies against the original RUS12 ZIP files for 2006–2021 and confirmed that all 212 differences match the corresponding raw `NonUtilityPropertyNet` values within the $10 tolerance.
The 212 failing borrower-year groups represent approximately 27.2% of the 779 borrower-year groups in the core diagnostic. This is a substantial proportion and should be explicitly disclosed to the maintainers.
Therefore, the accounting validation is working as intended and exposing a pre-existing transformation omission. Correcting the transformer is outside the scope of this validation-focused issue, so I decided to leave the transformation code unchanged and configure an error threshold to monitor future increases in failures.

**Proposed Solution**

I added five `subcomponents_sum_to_total` accounting validation tests to both the core and output RUS12 yearly balance-sheet assets schemas.
The tests validate the relationships between:
1. Total utility plant.
2. Net utility plant.
3. Total current and accrued assets.
4. Total other property and investments.
5. Total assets.

Each test groups records by `borrower_id_rus` and `report_date`, uses `asset_type` as the categorical column, and compares `ending_balance` values with a tolerance of 10 because these are dollar values.
For the total other property and investments test, I configured `error_if: ">212"` because the investigation confirmed that the 212 existing failures are caused by the missing `non_utility_property_asset` category in the transformed data.
This keeps the known discrepancies visible as warnings while raising an error if the number increases beyond 212.
I regenerated the corresponding dbt schemas and ran dbt tests for both tables to confirm that the tests were configured and executed correctly.
I deliberately did not modify the RUS12 transformer, column mapping, raw source data, or ETL pipeline. Fixing the missing transformed category is a separate issue and is outside the scope of this validation contribution.

**Implementation Plan**

1. Update `dbt/schema_inputs/rus12/core_rus12__yearly_balance_sheet_assets/schema.human.yml` to add five `subcomponents_sum_to_total` accounting validation tests for the core table.
2. Update `dbt/schema_inputs/rus12/out_rus12__yearly_balance_sheet_assets/schema.human.yml` to add the same five accounting validation tests for the output table.
3. Configure `error_if: ">212"` on the `total_other_property_and_investments` test in both schemas to account for the 212 known discrepancies.
4. Regenerate the corresponding dbt schemas under `dbt/models/rus12/` using `dbt_helper update-tables`.
5. Run dbt tests for both tables, verify the expected results, and check the final changes with `git diff --check`.

During validation, the `total_other_property_and_investments` test reported 212 failures in both tables.
I initially investigated whether these were actual source-data accounting errors. By comparing all 212 differences against the raw RUS12 ZIP files for 2006–2021, I confirmed that every difference matched the corresponding `NonUtilityPropertyNet` value within the $10 tolerance.
The initial diagnostic found only 53 matches because it searched for the older `Form12FinancialBalanceSheet.csv` filename. The naming convention changed in later years to names such as `OpRpt_PS_2016__US_aB_OpRpt_PSFinancialBalanceSheet.csv`.
I updated the diagnostic to search for the common `FinancialBalanceSheet.csv` suffix across all years. After confirming all 212 matches, I added the `error_if: ">212"` threshold to both schemas. I deliberately left the transformer and ETL pipeline unchanged because fixing the missing category is outside the scope of this validation contribution.

**Toolkit**

- **Tool:** GitHub Codespaces, VS Code, Pixi, dbt, `dbt_helper`, and Git.
- **What it produced:** Five accounting validation tests in each human-readable schema, regenerated dbt schemas for both tables, and successful execution of all 14 dbt tests.
- **Difficulties:** The total other property and investments test reported 212 failures because the transformed data was missing `non_utility_property_asset`. I investigated the raw source files to establish the cause before deciding how to configure the threshold.
- **What changed:** I added `error_if: ">212"` to the affected test in both schemas, regenerated the schemas, and verified that the known failures appeared as warnings while increases above 212 would trigger errors.

---

## Testing Strategy

I tested the accounting validation changes against both the core and output RUS12 yearly balance-sheet assets tables.

**Baseline testing before implementation**

I ran `dbt_helper validate` for each asset using the existing nightly Parquet data. Both tables passed their two existing validation checks:

- Core asset: PASS=2, TOTAL=2.
- Output asset: PASS=2, TOTAL=2.

This established the baseline before adding the accounting consistency tests.

**Validation after implementation**

I ran the following dbt command:

```bash
PUDL_OUTPUT=/workspaces/pudl-output pixi run dbt test --project-dir dbt --profiles-dir dbt --select source:pudl.core_rus12__yearly_balance_sheet_assets source:pudl.out_rus12__yearly_balance_sheet_assets
```

Results:

| Result | Count |
|---|---:|
| PASS | 12 |
| WARN | 2 |
| ERROR | 0 |
| Total | 14 |

The four accounting relationships passed for both tables. The total other property and investments test reported 212 warnings for each table, as expected with the configured `error_if: ">212"` threshold.

**Raw source verification**

I compared all 212 validation differences against the original RUS12 financial balance-sheet CSV files from 2006 through 2021.

Results:

- Raw values found: 212.
- Values matching within tolerance 10: 212.
- Mismatches: 0.
- Raw records not found: 0.
- Missing ZIP archives: 0.
- Years without a matching CSV: 0.

This confirmed that all discrepancies were explained by the missing transformed category.

**Change verification**

I regenerated both dbt schemas using:

```bash
pixi run dbt_helper update-tables --schema --no-row-counts core_rus12__yearly_balance_sheet_assets out_rus12__yearly_balance_sheet_assets
```
Both schemas were successfully generated.
I also ran:

```bash
git diff --check
git status --short
```
The whitespace check passed, and Git showed exactly four modified schema files. The transformer and ETL pipeline remained unchanged.

**Toolkit**

- **Tool:** dbt, Pixi, `dbt_helper`, pandas, Python CSV/ZIP utilities, and Git.
- **What it produced:** All 14 dbt tests completed with 12 PASS, 2 WARN, and 0 ERROR. The raw-data diagnostic confirmed that all 212 discrepancies matched the source values.
- **Difficulties:** The known discrepancy caused two warnings, but initially appeared to be a data-quality problem. The raw CSV naming changes also required an updated diagnostic.
- **What changed:** I verified all raw values, configured the warning/error threshold, regenerated the schemas, and confirmed the four-file change set with a clean whitespace check.


---

## Implementation Notes

**November 2, 2026**

I added five accounting validation tests to the core and output RUS12 yearly balance-sheet assets schemas. The tests cover total utility plant, net utility plant, total current and accrued assets, total other property and investments, and total assets.
I regenerated both generated dbt schemas successfully. The first test run identified 212 discrepancies in the total other property and investments calculation for each table.

**November 6, 2026**

I investigated the 212 discrepancies using the raw RUS12 ZIP files from 2006 through 2021. My initial diagnostic found only 53 raw matches because the CSV filename changed in later reporting years.
I updated the diagnostic to search for `FinancialBalanceSheet.csv` across all annual archives. All 212 differences then matched their raw `NonUtilityPropertyNet` values within the $10 tolerance.
I traced the missing category to the transformer's `_assets$` column-selection rule, which excludes the singular `_asset` column. I left the transformer unchanged because fixing it is outside the scope of the issue.
I configured `error_if: ">212"` in both schemas and reran the dbt tests. The final results were 12 PASS, 2 WARN, and 0 ERROR. I also confirmed that only the four intended schema files were modified.


**Toolkit**

- **Tool:** GitHub Codespaces terminal, Python, pandas, zipfile, CSV, dbt, and Git.
- **What it produced:** A reproducible record of the five validation tests, generated schemas, raw-data investigation, threshold configuration, and final dbt test results.
- **Difficulties:** The later-year CSV filenames differed from earlier years, which caused the first raw-data diagnostic to miss records.
- **What changed:** I corrected the filename matching logic, verified all 212 discrepancies, documented the root cause, and kept the implementation limited to the four schema files.


---

## Pull Request

**PR Link:** https://github.com/catalyst-cooperative/pudl/pull/5749

**PR Description:** Added dbt validation tests for `core_rus12__yearly_balance_sheet_assets` and `out_rus12__yearly_balance_sheet_assets`. The changes validate the RUS12 balance-sheet asset data against the expected source values and document the validation rules in the corresponding schema files. The PR also includes the release notes entry. AI assistance was used during development and conflict resolution, with the final changes reviewed and verified by me.
PR Title: Add RUS12 balance sheet asset validation tests
Base repository and branch: `catalyst-cooperative/pudl`
Head branch: `addisalem-aw:issue-5728-rus12-assets-validation`.

**Maintainer Feedback:**

- November 2, 2026: The maintainer approved my request to work on issue #5728 and invited me to tag them when the work was ready for review.
- November 7, 2026: I opened upstream PR #5749 after the final ship-gate returned PASS and the PR precheck returned accept.
- PR #5749 is awaiting maintainer review. No PR review feedback has been received yet.

**Status:** Awaiting review.

**Toolkit**

- **Tool:** GitHub CLI, Claude Code, ship-gate, and PR-precheck.
- **What it produced:** Upstream pull request #5749, linked to issue #5728.
- **Difficulties:** The first PR was accidentally opened in my fork instead of the upstream repository.
- **What changed:** I created the correct upstream PR targeting `catalyst-cooperative/pudl:main` and closed the accidental fork PR without deleting my contribution branch.
---

## Learnings and Reflections

**Technical Skills Gained**

My professional software development background is primarily in Java, Spring Boot, REST APIs, microservices, and SQL. Working on this PUDL contribution gave me an opportunity to step outside my familiar Java development environment and gain practical experience with Python-based data engineering tools.
I learned how PUDL uses human-readable YAML schemas to define dbt data tests and how `dbt_helper` generates the corresponding schemas. I also gained experience with the `subcomponents_sum_to_total` macro, including how it compares financial components with reported totals, how SQL `SUM()` handles missing values, and how dbt's `error_if` configuration distinguishes warnings from errors.
Although I had previous SQL experience, working with pandas, Parquet files, Python ZIP and CSV utilities, and dbt validation workflows was relatively new to me. I learned how to inspect structured financial data, trace fields from raw source files through column mappings and transformation functions, and verify accounting relationships using automated data-quality tests.
This contribution helped me expand my skills beyond enterprise Java application development and gain practical exposure to Python, data transformation, data validation, and open-source data engineering workflows.

**Challenges Overcome**

One of my biggest challenges was moving from my familiar Java and Spring Boot development environment into a large Python-based data engineering project. I had to become comfortable with PUDL's repository structure, Pixi environment management, YAML-based dbt schemas, Parquet data, and the project's validation tools.
Setting up the development environment was another major challenge. Since PUDL's development dependencies did not support my local Windows environment, I first tried to install and configure a virtual Linux environment using WSL and Ubuntu on my computer. However, Ubuntu repeatedly failed to start despite several troubleshooting attempts. Rather than stop working on the contribution, I moved to GitHub Codespaces, where I was able to use a Linux environment, install the required Pixi dependencies, and run the PUDL validation commands successfully.
Another challenge was understanding why the new accounting validation test reported 212 failures. My first diagnostic matched only 53 records because the raw CSV filenames changed in later reporting years. I inspected the 2016 archive, identified the `OpRpt_PS` naming convention, updated the file-matching logic, and eventually verified all 212 discrepancies against the raw source values.
I also had to distinguish between an accounting inconsistency and a data transformation issue. By tracing the missing category through the column mapping and transformer logic, I discovered that `non_utility_property_asset` was excluded because its name ended in singular `_asset`, while the transformer selected columns ending in `_assets`.
These experiences taught me to investigate unfamiliar technologies systematically, verify assumptions against original source data, troubleshoot development environments, and find alternative ways to continue when my initial setup did not work.

**What I'd Do Differently Next Time**

Next time, I would review the project's supported operating systems and development environment requirements before attempting a local setup. Since PUDL's dependencies did not support my Windows environment, starting with GitHub Codespaces or configuring WSL earlier would have saved troubleshooting time.
I would also inspect the raw source files and their naming conventions across all reporting years earlier in the investigation. This would have helped me avoid the initial incomplete diagnostic that matched only 53 records.
I would document baseline test results, exact commands, file locations, and environment details as soon as I reproduce an issue. This would make it easier to compare results before and after implementation.
Finally, I would spend more time understanding the project's existing transformation and validation patterns before adding new tests. This experience showed me the importance of learning an unfamiliar codebase, checking the original source data, and keeping a contribution within the scope requested by the maintainers.

---

## Resources Used

- [PUDL USDA RUS Form 12 Data Source Documentation](https://docs.catalyst.coop/pudl/en/latest/data_sources/rus12.html) — Used to understand the RUS12 dataset, its source, reporting structure, and financial data.
- [USDA RUS Form 12 Blank 2010 PDF](https://docs.catalyst.coop/pudl/en/latest/_downloads/66eb052cc3ef47c37e91d25f2071d019/rus12_blank_2010.pdf) — Used to identify the official balance-sheet accounting formulas and determine which financial totals should be compared with their components.
- [PUDL Raw RUS12 Data Archive on Zenodo](https://zenodo.org/records/18315223) — Used to inspect the original annual RUS12 financial balance-sheet CSV files and verify all 212 discrepancies against the raw NonUtilityPropertyNet values.
- [PUDL Issue #5728](https://github.com/catalyst-cooperative/pudl/issues/5728) — Used to understand the original task, expected validation tests, maintainer instructions, and contribution scope.
- [PUDL RUS12 Transformer](https://github.com/catalyst-cooperative/pudl/blob/main/src/pudl/transform/rus12.py) — Used to investigate how raw RUS12 balance-sheet columns are transformed and identify why non_utility_property_asset was excluded.
- [RUS12 Balance Sheet Column Mapping](https://github.com/catalyst-cooperative/pudl/blob/main/src/pudl/package_data/rus12/column_maps/balance_sheet.csv) — Used to trace the raw NonUtilityPropertyNet field to the canonical non_utility_property_asset column.
- [PUDL Subcomponents Sum-to-Total dbt Macro](https://github.com/catalyst-cooperative/pudl/blob/main/dbt/macros/expect_subcomponents_sum_to_total.sql) — Used to understand how the accounting validation tests compare component sums with reported totals, handle NULL values, and apply tolerance settings.
- [PUDL Contribution Guidelines](https://github.com/catalyst-cooperative/pudl/blob/main/CONTRIBUTING.rst) — Used to understand the repository's contribution practices and development requirements.
