# Test Summary — Test Summary Report

> **Instructions**: This is a **Quality Assurance** activity — the team assesses the overall software quality, not just lists bugs.

---

## 1. Group Information

| Item | Information |
|-----|----------|
| **Group** | Group 24 |
| **Class** | ICT |
| **Report Date** | 07/06/2026 |
| **Test System** | https://stqa.rbc.vn — v1.0 |

---

## 2. Test Results Overview

| Metric | Value |
|--------|---------|
| Total Test Cases | 39 |
| Pass | 30 |
| Fail | 9 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | 76.92% |
| **Bugs Found** | 8 |

### Distribution by Functional Group

| Functional Group | TC | Pass | Fail | Bug | Assessment |
|---------------|-----|------|------|-----|---------|
| Login | 7 | 7 | 0 | 0 | Stable. Login works correctly for valid, invalid, and empty input cases. |
| Borrow Book | 6 | 4 | 2 | 2 | Partially stable. Basic borrow restrictions work, but important business rules are violated. |
| View Book List | 3 | 3 | 0 | 0 | Stable. Book information and book status are displayed correctly. |
| Search and Filter Books | 7 | 6 | 1 | 1 | Mostly stable. Search works correctly, but category filtering has a case-sensitivity issue. |
| Return Book | 4 | 2 | 2 | 2 | Needs improvement. The system misses overdue warning and has an access control problem. |
| Overdue Handling | 4 | 4 | 0 | 0 | Stable. The overdue checking function works correctly for tested cases. |
| Member Management | 4 | 1 | 3 | 3 | Weak. Email validation and duplicate email handling have several issues. |
| Borrow Record Lookup | 4 | 3 | 1 | 1 | Mostly stable, but member access control is not properly enforced. |

### Bug Distribution by Severity

| Severity | Count | Bug IDs |
|--------|---------|---------|
| High | 2 | BUG-02, BUG-05 |
| Medium | 6 | BUG-01, BUG-03, BUG-04, BUG-06, BUG-07, BUG-08 |
| Low | 0 | - |

---

## 3. Test Design Techniques Used

| Technique | Applied to Which REQ? | Number of TCs | Explanation of Application |
|----------|---------------------|---------------|------------------------|
| Equivalence Partitioning (EP) | REQ-01, REQ-02, REQ-03, REQ-04, REQ-05, REQ-07, REQ-08 | 25 | EP was used to divide inputs into valid and invalid partitions, such as valid/invalid login fields, [...]
| Boundary Value Analysis (BVA) | REQ-04, REQ-05, REQ-06 | 5 | BVA was used for boundary-related rules, such as the maximum limit of 3 borrowed books, overdue due dates, and records whose due date[...]
| Decision Table | REQ-01, REQ-04, REQ-05, REQ-06, REQ-07, REQ-08 | 13 | Decision Table was used for rules that depend on multiple conditions, such as login email/password combinations, book statu[...]

---

## 4. Software Quality Analysis

### 4.1. Strengths

- The login function is reliable. All login test cases passed, including valid login, wrong email, wrong password, empty email, empty password, and combined invalid input.
- The book list function works well. The system displays book information and book status correctly.
- The search function works correctly for title, author, lowercase keyword, uppercase keyword, and no-result cases.
- The overdue checking function works correctly when triggered by the librarian. The system updates overdue records and prevents normal members from accessing the overdue checking function.
- Basic borrow and return flows work in normal cases, such as borrowing an available book and returning the member's own borrowed book.

### 4.2. Weaknesses

- The system has a serious access control issue. A member can view and return another member's borrow record. This affects both Return Book and Borrow Record Lookup.
- The borrowing limit rule is not enforced correctly. A member who already has 3 active borrowed books can still borrow another book.
- Member Management has several email validation problems. The system rejects a valid email, accepts an invalid email, and displays the wrong message for duplicate email.
- The system does not display an overdue warning when an overdue book is returned.
- Category filtering is case-sensitive, so valid lowercase category input may return no result.
- Some error messages are misleading, especially the suspended-member case where the system displays an expired-member message.

---

## 5. Bug Fix Priority Recommendations

> Priority Criteria: the team prioritizes fixing high-severity bugs first, especially bugs affecting data access rights, business rules [...]

| Priority | Bug | Severity | Priority Reason |
|--------|-----|---------|---------------|
| 1 | BUG-05 | High | This is the most serious issue because a member can view and return another member's borrowed book. It violates access control and can modify another user's data. |
| 2 | BUG-02 | High | The system allows a member to exceed the maximum borrowing limit of 3 books, which violates a core borrowing rule and affects inventory control. |
| 3 | BUG-06 | Medium | The librarian cannot add a new member with a valid email format, which blocks a normal member management workflow. |
| 4 | BUG-07 | Medium | The system accepts invalid email data, which reduces data quality and violates the email validation rule. |
| 5 | BUG-08 | Medium | The system displays the wrong error message for duplicate email, which can confuse the librarian and make the issue harder to correct. |
| 6 | BUG-04 | Medium | The system does not warn users when an overdue book is returned, which violates the overdue return requirement. |
| 7 | BUG-03 | Medium | Category filtering fails for lowercase input, reducing usability of the search/filter function. |
| 8 | BUG-01 | Medium | The system blocks suspended members correctly, but displays the wrong reason. This should be fixed to avoid confusion between suspended and expired accounts. |

---

## 6. Conclusion

Overall, the system is **not ready for release**.

Although several basic functions work correctly, such as login, viewing the book list, searching books, checking overdue records, and basic borrow/return flows, the system still contains importan[...]

The system should not be released until the high-severity issues are fixed, especially BUG-05 and BUG-02. After fixing these bugs, the team should rerun the related test cases and perform regress[...]

---

## 7. Lessons Learned

- Test cases should be designed directly from the SRS because the SRS is the main source of truth for expected results.
- Negative test cases are important because many serious bugs were found in invalid or restricted scenarios.
- Access control must be tested carefully, especially when the system has different roles such as librarian and member.
- Combining EP, BVA, and Decision Table helps cover different types of rules, such as input validation, boundary conditions, and role-based decisions.
- Screenshots and clear evidence make bug reports easier to understand and verify.

---

## 8. AI Usage Declaration

| AI Tool | Used For Which Section | How Did You Review/Edit |
|------------|-------------------|-----------------------------------|
| ChatGPT | Support writing and improving test cases, test execution, bug reports, and summary. | The group reviewed the generated content, compared it with the SRS, checked it against actual scr[...]
