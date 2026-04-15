# Test Cases for AI-Powered Quiz & Study Assistant Platform

This document lists test cases in simple English for the project described in `product_requirements.md`.
Each test case has an ID, a short title, purpose, basic steps, expected result, and a suggested priority.

---

## How to read these tests
- ID: short code to reference the test (e.g., QC = Quiz Case, AI = AI Chatbot, UM = User Management).
- Steps: simple, human-readable steps to reproduce.
- Expected result: what should happen for the test to pass.
- Priority: High / Medium / Low.

---

## Quiz System

QC-01 — Create quiz (teacher)
- Purpose: Verify a teacher can create a quiz with questions and save it.
- Steps: Login as a teacher → Open "Create Quiz" → Enter title and description → Add multiple question types (MCQ, short answer, coding) → Save quiz.
- Expected result: Quiz is saved and appears in the teacher's quiz list; questions persist and can be edited.
- Priority: High

QC-02 — Required fields and validation
- Purpose: Ensure validation prevents creating invalid quizzes.
- Steps: Login as teacher → Try to save a quiz with an empty title or an empty question → Observe validation messages.
- Expected result: The UI shows a clear validation error and prevents saving until fields are fixed.
- Priority: High

QC-03 — Take quiz (student)
- Purpose: Confirm students can open and take a quiz.
- Steps: Login as a student → Open an available quiz → Answer questions → Submit quiz.
- Expected result: Answers are accepted and submission is acknowledged. Student is shown a submission confirmation.
- Priority: High

QC-04 — Automatic grading (MCQ)
- Purpose: Verify automatic grading works for auto-gradable question types.
- Steps: Teacher creates MCQ questions with correct answers → Student completes and submits quiz → Check results.
- Expected result: System calculates score automatically for MCQs and displays it to the student (or the teacher dashboard) according to grading rules.
- Priority: High

QC-05 — Partial and manual grading (short answer / coding)
- Purpose: Ensure short answer/coding questions can be graded and show results after grading.
- Steps: Teacher creates short answer or coding questions → Student submits → Teacher grades answers (manual or with assisted scoring) → Student views graded result.
- Expected result: Grader can assign scores/comments; student sees final graded score and comments.
- Priority: Medium

QC-06 — No AI hints during quiz
- Purpose: Ensure AI hints are disabled while a student is actively taking a quiz.
- Steps: Start taking a quiz → Attempt to open or ask the AI chatbot for hints during the quiz session → Observe behavior.
- Expected result: AI hint requests are blocked/disabled while the quiz is active; UI explains why.
- Priority: High

QC-07 — Network interruption during submission
- Purpose: Verify submission resilience to network issues.
- Steps: Start quiz → Finish answers → On submit, simulate network loss → Restore network.
- Expected result: The system retries submission or preserves answers and allows resubmission without data loss.
- Priority: Medium

QC-08 — Duplicate submission prevention
- Purpose: Make sure the same submission cannot be processed twice.
- Steps: Rapidly click Submit multiple times or trigger duplicate submit requests (simulate race) → Check stored results.
- Expected result: Only one submission is accepted and duplicates are ignored or rejected safely.
- Priority: Medium

QC-09 — Timer and integrity (optional)
- Purpose: Ensure quiz timers work and integrity features function.
- Steps: Create a timed quiz → Student starts quiz → Let timer expire or manipulate time → Check result handling and any anti-cheat flags.
- Expected result: Timer enforcement works, and integrity checks log or prevent suspicious activity as configured.
- Priority: Medium


## AI Chatbot Tutor

AI-01 — Post-quiz explanation for wrong answers
- Purpose: Verify the AI explains incorrect answers after submission.
- Steps: Student completes quiz with at least one wrong answer → Submit quiz → Ask AI to explain incorrect answers in the post-quiz view.
- Expected result: AI returns clear, step-by-step explanations for each incorrect answer; explanation is relevant and concise.
- Priority: High

AI-02 — Generate practice questions
- Purpose: Confirm AI can generate follow-up practice questions based on performance.
- Steps: Student requests "generate practice" after reviewing results → Provide desired number and difficulty → AI returns questions.
- Expected result: AI returns the requested number of practice questions, labeled by difficulty and with correct answers/solutions available after attempt.
- Priority: High

AI-03 — Recommend study topics
- Purpose: Ensure AI suggests topics for improvement based on quiz performance.
- Steps: Student finishes quiz → Open recommendations → AI analyzes wrong answers and returns recommended topics and resources.
- Expected result: AI lists targeted topics and brief reasons for recommendation; suggestions are actionable.
- Priority: Medium

AI-04 — Respecting AI assistance configuration
- Purpose: Test AI behavior settings (strict / balanced / helpful) and hint availability toggles.
- Steps: Teacher or student toggles AI level → Request an explanation or hint after quiz → Observe response tone and depth.
- Expected result: AI response style matches configured level: minimal for strict, helpful and stepwise for helpful, balanced in-between.
- Priority: Medium

AI-05 — No AI hints during active quiz (enforced)
- Purpose: Double-check that settings and system policy prevent hints during the quiz.
- Steps: Start quiz with AI level set to helpful → Attempt hint → System should block it during quiz.
- Expected result: Attempts to get hints during the quiz are rejected even if settings would normally allow hints outside the quiz.
- Priority: High

AI-06 — Prompt injection and safety checks
- Purpose: Ensure AI ignores or safely handles malicious input and never exposes system prompts or secrets.
- Steps: Send crafted inputs that attempt to override instructions or request private data via AI chat → Observe AI response and logs.
- Expected result: AI refuses to follow malicious instructions and returns a safe, generic refusal or sanitized response; system logs the attempt.
- Priority: High

AI-07 — AI response quality and accuracy check
- Purpose: Validate that AI responses meet quality standards (clear, accurate, not misleading).
- Steps: For a sample of quiz topics, request explanations and solutions → Review correctness and clarity against authoritative answers.
- Expected result: Explanations are accurate, cite reasoning, and do not contain factual errors. Flag any low-quality responses for review.
- Priority: Medium


## Feedback System

FB-01 — Show detailed explanations in UI
- Purpose: Verify the feedback UI shows detailed explanations and supports scrolling/copying.
- Steps: After quiz grading, open feedback → Inspect explanation text, examples, and references.
- Expected result: Full explanations are visible, properly formatted, and do not truncate important information.
- Priority: Medium

FB-02 — Suggest areas of improvement
- Purpose: Ensure suggestions are shown and can be saved to a study plan.
- Steps: View post-quiz recommendations → Save suggestions to personal plan → Open plan later.
- Expected result: Suggestions are saved and appear in the student's study plan with correct references.
- Priority: Low

FB-03 — Instructor feedback flow
- Purpose: Confirm that teacher comments and feedback are delivered and visible to students.
- Steps: Teacher adds feedback/comments to student submission → Student views feedback.
- Expected result: Student sees teacher feedback with timestamps and context.
- Priority: Medium


## User Management

UM-01 — Sign up and email verification
- Purpose: Verify account creation and verification flows.
- Steps: Register new account with email/password → Check email for verification link → Click link → Confirm account activation.
- Expected result: Account is created in unverified state until verification link is clicked; clicking verifies and allows full use.
- Priority: High

UM-02 — Login with email/password
- Purpose: Ensure standard login works for all roles.
- Steps: Login with valid credentials → Access role-specific dashboard.
- Expected result: Successful login and correct landing page for the user's role.
- Priority: High

UM-03 — Google login (OAuth)
- Purpose: Verify third-party sign-in works.
- Steps: Choose "Sign in with Google" → Complete OAuth flow → Confirm account linked or created.
- Expected result: User is logged in and an account record exists; subsequent logins reuse the account.
- Priority: Medium

UM-04 — Roles and RBAC
- Purpose: Confirm role-based permissions (student, teacher, admin).
- Steps: Login as student and attempt teacher-only actions (create quiz) → Login as teacher and attempt admin-only actions.
- Expected result: Unauthorized actions are blocked with clear messages; authorized roles can perform their actions.
- Priority: High

UM-05 — Password reset
- Purpose: Verify password reset email and flow.
- Steps: Trigger "Forgot password" → Receive reset link → Change password → Login with new password.
- Expected result: Password updates successfully and old password no longer works.
- Priority: Medium

UM-06 — Account deletion and data export (privacy)
- Purpose: Ensure user can request data export or deletion as per policy.
- Steps: Request data export → Receive archive → Request account deletion → Confirm deletion.
- Expected result: Export contains user data; deletion deactivates or removes account per policy.
- Priority: Low


## Data & Storage

DM-01 — Persistence of quizzes and results
- Purpose: Verify quiz definitions and student results are stored permanently.
- Steps: Create quiz and have students submit → Check DB or UI for stored quiz and results after logout and login.
- Expected result: Data persists and is accessible to permitted roles.
- Priority: High

DM-02 — Temporary AI chat history
- Purpose: Confirm chat history is temporary/session-based where required.
- Steps: Start AI session → Chat a few messages → End session or wait expiration → Check stored chat history.
- Expected result: Chat history is ephemeral or stored according to configuration; old sessions are purged as expected.
- Priority: Medium

DM-03 — Data retention and backups
- Purpose: Ensure backups and retention rules are functioning.
- Steps: Verify backup jobs and retention configuration (admin area or infra check) → Restore sample dataset.
- Expected result: Backups exist and restore process recovers data.
- Priority: Low


## Testing Strategy (meta test cases)

TS-UNIT-01 — Scoring logic unit tests
- Purpose: Unit-test scoring functions for MCQ, partial credit, negative marking, and edge cases.
- Steps: Run unit tests with representative inputs, including empty answers and boundary scores.
- Expected result: Functions return correct numeric scores for all cases.
- Priority: High

TS-UNIT-02 — Question validation unit tests
- Purpose: Validate question schema and validation rules.
- Steps: Run tests that create valid and invalid question objects.
- Expected result: Invalid questions are rejected; valid ones accepted.
- Priority: High

TS-INTEGRATION-01 — Quiz system + AI chatbot
- Purpose: Ensure the quiz API and AI service work together (post-quiz flow).
- Steps: Simulate quiz completion → Trigger AI explanations via API → Check response and saved feedback.
- Expected result: API calls succeed and data flows correctly between services.
- Priority: High

TS-E2E-01 — End-to-end happy path
- Purpose: Full-flow test from signup to AI feedback.
- Steps: Create teacher account → Create quiz → Create student account → Student takes quiz → Submit → Request AI explanation → Verify outputs.
- Expected result: All steps succeed end-to-end and the student receives explanations.
- Priority: High

TS-API-01 — AI response schema and validation
- Purpose: Validate AI responses conform to expected schema (no secrets, correct fields).
- Steps: Call AI endpoint with test prompts → Inspect response for required fields and safety tokens.
- Expected result: Responses have expected fields and no disallowed content.
- Priority: High

TS-LOAD-01 — Concurrency and load test for AI
- Purpose: Simulate many users requesting AI feedback concurrently.
- Steps: Use a load test tool to simulate X simultaneous users requesting AI explanations → Monitor latency and error rates.
- Expected result: System maintains acceptable latency and error rates under target load; graceful degradation beyond capacity.
- Priority: Medium

TS-SEC-01 — Authentication and authorization tests
- Purpose: Ensure endpoints are protected and role enforcement works.
- Steps: Attempt unauthorized API requests, test JWT expiry, replay attacks, and role escalation attempts.
- Expected result: Unauthorized requests are rejected; tokens are validated and logged.
- Priority: High

TS-SEC-02 — Prompt injection and content filtering tests
- Purpose: Verify defenses against prompt injection in AI inputs.
- Steps: Send crafted malicious prompts to AI endpoints and check output and mitigation logs.
- Expected result: System sanitizes inputs or refuses unsafe requests; logs and alerts are generated.
- Priority: High

TS-UX-01 — Readability and helpfulness user test
- Purpose: Have human testers rate AI replies for clarity and usefulness.
- Steps: Prepare sample quizzes, collect AI explanations, gather ratings from testers across levels.
- Expected result: Average ratings meet quality thresholds; issues logged for improvement.
- Priority: Low


## Edge cases and negative tests (select highlights)
- Try creating thousands of questions in one quiz and confirm the UI and storage handle it gracefully.
- Submit answers with extremely long text or malformed input and verify sanitization.
- Test with slow or intermittent network for both quiz and AI flows.
- Attempt SQL/XSS-like payloads in quiz content and user profiles to check security filters.

---

## Acceptance criteria (short)
- High-priority tests must pass before MVP release: quiz creation/taking, auto-grading, no AI hints during active quiz, post-quiz AI explanations, authentication, and role enforcement.
- Medium/low tests should be scheduled for the next iterations.

---

Files created/edited
- `test_cases.md` — this file: simple English test cases and priorities.


