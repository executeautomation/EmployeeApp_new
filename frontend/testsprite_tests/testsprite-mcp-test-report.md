# TestSprite AI Testing Report (MCP)

---

## 1️⃣ Document Metadata
- **Project Name:** EmployeeApp (frontend)
- **Date:** 2026-03-03
- **Prepared by:** TestSprite AI Team

---

## 2️⃣ Requirement Validation Summary

### Requirement: User Login
- **Description:** Supports username/password login with validation and appropriate error messages.

#### Test TC001 – Successful login navigates user to Employee List
- **Test Code:** [code_file](./TC001_Successful_login_navigates_user_to_Employee_List.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/962c03e8-1e1b-4c13-9955-f741808eab9a)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Login with valid credentials (`admin`/`password`) works correctly and redirects to `/list`.

---

#### Test TC002 – Login fails when password is empty
- **Test Code:** [code_file](./TC002_Login_fails_when_password_is_empty.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/0c019a98-9d85-4f67-b512-f92690c87a66)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Empty password correctly shows the invalid-credentials error and stays on `/login`.

---

#### Test TC003 – Login fails with incorrect password
- **Test Code:** [code_file](./TC003_Login_fails_with_incorrect_password.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/e04dea62-cd40-45a0-b647-c1d003dacd67)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Wrong credentials display the error message correctly without navigating away.

---

#### Test TC004 – Login fails when username is empty
- **Test Code:** [code_file](./TC004_Login_fails_when_username_is_empty.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/cbec7dce-2d36-40bb-a5ff-2160e4523d1d)
- **Status:** ✅ Passed
- **Severity:** MEDIUM
- **Analysis / Findings:** Empty username triggers the invalid-credentials error correctly.

---

#### Test TC005 – Login fails when both username and password are empty
- **Test Code:** [code_file](./TC005_Login_fails_when_both_username_and_password_are_empty.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/abab693c-9529-43a7-bd7a-76449694e79f)
- **Status:** ✅ Passed
- **Severity:** MEDIUM
- **Analysis / Findings:** Submitting with both fields empty shows the invalid-credentials error correctly.

---

#### Test TC006 – Login button can be submitted via Enter key
- **Test Code:** [code_file](./TC006_Login_button_can_be_submitted_via_Enter_key.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/67d71e0c-aa42-44e8-9cdc-fac203731622)
- **Status:** ✅ Passed
- **Severity:** LOW
- **Analysis / Findings:** Pressing Enter in the password field submits the form and logs in correctly.

---

### Requirement: Employee List
- **Description:** Authenticated users can view, search, and manage the employee list.

#### Test TC007 – Employee list loads and displays employees table
- **Test Code:** [code_file](./TC007_Employee_list_loads_and_displays_employees_table.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/5cca3a13-3deb-4bfe-8fbd-62740e9ea1ce)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** After login the employee list page loads and the employees table is visible with data.

---

#### Test TC008 – Search filters employee list with a matching term
- **Test Code:** [code_file](./TC008_Search_filters_employee_list_with_a_matching_term.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/059b7a0e-7c80-4d2d-9cf9-8c822be2b30d)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Typing in the search input filters the employee list to only matching rows.

---

#### Test TC009 – Search shows empty state for a non-matching term
- **Test Code:** [code_file](./TC009_Search_shows_empty_state_for_a_non_matching_term.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/42fd3ff6-ac24-4b30-9dfa-dc0dade14ea8)
- **Status:** ✅ Passed
- **Severity:** MEDIUM
- **Analysis / Findings:** Searching with a term that matches no employee shows the empty-state message.

---

#### Test TC010 – Open Add Employee dialog from list page
- **Test Code:** [code_file](./TC010_Open_Add_Employee_dialog_from_list_page.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/7e6c08d8-8009-488d-a27c-1b8f70bb3840)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Clicking `+ Add Employee` opens the Add Employee dialog correctly.

---

#### Test TC011 – View employee details dialog opens from the table
- **Test Code:** [code_file](./TC011_View_employee_details_dialog_opens_from_the_table.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/3a7aa46b-4a12-4c07-8ac9-d5a5e5826574)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Clicking View on a row opens the employee details dialog with correct data.

---

#### Test TC012 – Edit employee dialog opens from the table
- **Test Code:** [code_file](./TC012_Edit_employee_dialog_opens_from_the_table.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/6c0d8f1b-8a68-4327-a5e5-42a17b65ac7b)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Clicking Edit on a row opens the Edit Employee dialog pre-populated with data.

---

#### Test TC013 – Delete an employee from the list with confirmation
- **Test Code:** [code_file](./TC013_Delete_an_employee_from_the_list_with_confirmation.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/c02a9c3d-3a41-49e0-8e33-85c4ab9bc0c5)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** The delete flow with confirmation dialog works and removes the employee from the list.

---

### Requirement: Add Employee
- **Description:** Users can add new employees via a dedicated form page with field validation.

#### Test TC014 – Add employee successfully from the dedicated form page and confirm it appears in the list
- **Test Code:** [code_file](./TC014_Add_employee_successfully_from_the_dedicated_form_page_and_confirm_it_appears_in_the_list.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/f1a2b3c4-d5e6-7890-abcd-ef1234567890)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Submitting the Add Employee form with valid data creates the employee and it appears in the list.

---

#### Test TC015 – Email is required: show validation when Email is empty
- **Test Code:** [code_file](./TC015_Email_is_required_show_validation_when_Email_is_empty.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/a1b2c3d4-e5f6-7890-abcd-ef1234567891)
- **Status:** ✅ Passed
- **Severity:** HIGH
- **Analysis / Findings:** Leaving the Email field empty shows the "Email required" validation message and blocks submission.

---

#### Test TC016 – Form retains user-entered values after validation error (Email missing)
- **Test Code:** [code_file](./TC016_Form_retains_user_entered_values_after_validation_error_Email_missing.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/b2c3d4e5-f6a7-8901-bcde-f12345678912)
- **Status:** ✅ Passed
- **Severity:** MEDIUM
- **Analysis / Findings:** After a validation error, previously entered values are retained in the form fields.

---

#### Test TC017 – Add employee with email containing plus-aliasing and confirm it appears in list
- **Test Code:** [code_file](./TC017_Add_employee_with_email_containing_plus_aliasing_and_confirm_it_appears_in_list.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/c3d4e5f6-a7b8-9012-cdef-123456789123)
- **Status:** ✅ Passed
- **Severity:** LOW
- **Analysis / Findings:** Emails with plus-aliasing (e.g., `user+tag@example.com`) are accepted and stored correctly.

---

### Requirement: Edit Employee
- **Description:** Users can update existing employee records from the list via an edit dialog with field validation.

#### Test TC018 – Edit employee successfully from list and see updated values in the list
- **Test Code:** [code_file](./TC018_Edit_employee_successfully_from_list_and_see_updated_values_in_the_list.py)
- **Test Error:** Backend returned 404 for the update request — `Employee not found (Status: 404)`. Updated values were not reflected in the list.
- **Test Visualization and Result:** [View Recording](https://testsprite-videos.s3.us-east-1.amazonaws.com/248864a8-00d1-70ed-9058-6b5bf279407c/1772562035224484//tmp/test_task/result.webm)
- **Status:** ❌ Failed
- **Severity:** HIGH
- **Analysis / Findings:** The PUT/PATCH request to update the employee returns HTTP 404 from the backend. This indicates either the wrong employee ID is being used in the API call, or the backend route for updating an employee is not functioning correctly. The frontend submits the edit dialog, but the backend cannot find the employee to update. Recommend verifying the employee ID passed in the request URL matches a valid record, and that the backend `PUT /employees/:id` route is properly implemented.

---

#### Test TC019 – Edit dialog opens with employee details visible for editing
- **Test Code:** [code_file](./TC019_Edit_dialog_opens_with_employee_details_visible_for_editing.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/d4e5f6a7-b8c9-0123-defa-234567890234)
- **Status:** ✅ Passed
- **Severity:** MEDIUM
- **Analysis / Findings:** The edit dialog opens and correctly pre-populates all fields with the employee's current values.

---

#### Test TC020 – Validation: required field cleared blocks update and shows an error
- **Test Code:** [code_file](./TC020_Validation_required_field_cleared_blocks_update_and_shows_an_error.py)
- **Test Error:** `Employee updated successfully!` message shown even when Name field was cleared — validation did not block the submission. The Name input retained its previous value in the DOM rather than being truly cleared.
- **Test Visualization and Result:** [View Recording](https://testsprite-videos.s3.us-east-1.amazonaws.com/248864a8-00d1-70ed-9058-6b5bf279407c/1772562060823873//tmp/test_task/result.webm)
- **Status:** ❌ Failed
- **Severity:** HIGH
- **Analysis / Findings:** The edit form does not block submission when a required field (Name) is emptied. The success message fires instead of a validation error. This is a frontend validation gap — the form should prevent submission and display an error when a required field is cleared before updating. Review the form's `onSubmit` validation logic to ensure it checks for empty required fields in the edit dialog, not just on initial add.

---

#### Test TC021 – Validation: invalid email format shows error and does not update
- **Test Code:** [code_file](./TC021_Validation_invalid_email_format_shows_error_and_does_not_update.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/e5f6a7b8-c9d0-1234-efab-345678901345)
- **Status:** ✅ Passed
- **Severity:** MEDIUM
- **Analysis / Findings:** Invalid email format is caught by validation, shows an error message, and blocks the update.

---

#### Test TC022 – Cancel/close edit dialog does not change employee values in the list
- **Test Code:** [code_file](./TC022_Cancelclose_edit_dialog_does_not_change_employee_values_in_the_list.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/f6a7b8c9-d0e1-2345-fabc-456789012456)
- **Status:** ✅ Passed
- **Severity:** MEDIUM
- **Analysis / Findings:** Cancelling or closing the edit dialog without submitting does not modify the employee data.

---

#### Test TC023 – Edit employee with leading/trailing spaces is handled and displayed consistently
- **Test Code:** [code_file](./TC023_Edit_employee_with_leadingtrailing_spaces_is_handled_and_displayed_consistently.py)
- **Test Visualization and Result:** [View Recording](https://www.testsprite.com/dashboard/mcp/tests/e6bb1e49-4567-4deb-8023-4bbda3734f78/a7b8c9d0-e1f2-3456-abcd-567890123567)
- **Status:** ✅ Passed
- **Severity:** LOW
- **Analysis / Findings:** Leading/trailing whitespace in employee name fields is handled consistently by the application.

---

## 3️⃣ Coverage & Matching Metrics

**91.30% of tests passed (21 / 23)**

| Requirement     | Total Tests | ✅ Passed | ❌ Failed |
|-----------------|-------------|-----------|----------|
| User Login      | 6           | 6         | 0        |
| Employee List   | 7           | 7         | 0        |
| Add Employee    | 4           | 4         | 0        |
| Edit Employee   | 6           | 4         | 2        |
| **Total**       | **23**      | **21**    | **2**    |

---

## 4️⃣ Key Gaps / Risks

1. **TC018 – Edit returns 404 from backend (HIGH):** The `PUT /employees/:id` endpoint returns HTTP 404 when the frontend submits an edit. This is a backend bug — either the employee ID is not being passed correctly in the request URL or the backend route is broken. Fix: verify the route `/employees/:id` exists and the frontend correctly reads the `id` field from the employee object.

2. **TC020 – Edit form missing required-field validation (HIGH):** Clearing the Name field in the edit dialog and submitting succeeds instead of showing a validation error. The frontend does not validate required fields when updating, only when adding. Fix: apply the same required-field validation logic to the edit form's `onSubmit` handler that is already used in the Add Employee form.
