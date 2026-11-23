## Unit 7 — Issue selection

**Issue link:** https://github.com/codepath/pathreview-ai201-fa26-howard/issues/37

**Issue title:** API reference doc is missing the POST /profiles request body schema

**Tier:** Tier 1

**Problem summary:**
The API reference in `docs/API.md` lists the profile and review endpoints, but it does not explain what data to send when creating either one. Someone using the API has to read the Python code to figure out the fields and how to format their requests. For `POST /profiles`, the documentation needs to explain the multipart form fields, including the optional resume upload, rather than show a JSON body. For `POST /reviews`, it needs to describe the JSON body containing a profile ID. A successful fix would give each field a description and an example value that matches the existing implementation.

**Branch name:** `docs/37-api-request-body-schemas`

**Setup confirmation:** The app runs locally at localhost:5173.

**Cohort ledger:** I added issue #37 to the cohort ledger.

**Selection notes and scope reasoning:**
I chose this issue because the expected result is clear and the change is limited to the API documentation. I found and reviewed the profile creation route and the review request schema. The profile route accepts multipart form fields and an optional resume upload, while the review schema requires a profile ID in JSON. This gives me a concrete reference for writing accurate field descriptions and examples.

The issue is labeled Tier 1, good first issue, enhancement, api, and docs. That fits the scope because I expect to edit only `docs/API.md`. My plan is to document each field's type, whether it is required, and an example value, then compare the examples with the existing code. I also read a related review service test to understand how review creation is tested. That test does not check request examples, so I still need to determine the appropriate validation for this documentation change.

The issue estimates 2 to 3 hours, and I have budgeted 3 to 4 hours to include verification and PR preparation. This fits my schedule before the Unit 9 deadline. I commented on the issue to claim it and checked the issue comments and ledger for other claims. I am comfortable proceeding with the number of people working on it. I also checked for blockers and dependencies and found none that would prevent me from starting.

## Unit 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/abeeralrijal/pathreview-ai201-fa26-howard/commit/5badb7d8f07ab0bc2f92a0877704725027c861ac

**Reproduction summary:**
I reproduced the documentation gap by opening the Profiles and Reviews sections in my local `docs/API.md` and comparing them with `create_profile_endpoint` and `ReviewCreate`. The guide lists both POST endpoints but omits their request fields, content types, and example values, even though the backend already defines them.

**Local reproduction steps and observations:**

1. Open `docs/API.md` and read the Profiles and Reviews sections. Both POST entries contain only a short description, with no request body table or example.
2. Open `api/routes/profiles.py` and read `create_profile_endpoint`. It accepts `github_username` and `portfolio_url` as form fields and `resume_file` as a file upload, all with defaults of `None`.
3. Read `ProfileCreate` in `api/schemas/profile.py` to confirm the optional string fields and their length limits.
4. Open `api/schemas/review.py` and read `ReviewCreate`. It requires `profile_id` as a UUID. Then read `create_review_endpoint` in `api/routes/reviews.py` to confirm that it accepts that request model.
5. Compare these definitions with the API reference. The multipart profile fields and JSON review field are absent from the written guide, which confirms issue #37 locally.

This reproduction is a comparison of the local documentation and source code. It does not depend on triggering an API error or making a live request.

**PLAN.md link:** [Solution plan](https://github.com/abeeralrijal/pathreview-ai201-fa26-howard/blob/docs/37-api-request-body-schemas/PLAN.md)

**Walkthrough video (recommended):** Not recorded.

**Blockers or open questions:**
There are no blockers to writing the documentation. The upload code accepts plain text as well as PDF and Markdown, so the guide needs to reflect the actual MIME allowlist. I will verify the examples against the route and schema definitions and avoid claiming that live requests have been tested until I run them. The plan records the validation and PDF parsing details that need care during implementation.
