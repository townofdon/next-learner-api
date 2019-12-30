# Initial Thoughts

Yes, I'm reinventing the wheel. This app stems from a desire to:

1. Learn Rails
2. Address inadequecies in Blackboard that my wife, a teacher, has pointed out
3. Offer this as a free and open-source option for people
  - If this app catches on, I'll add PayPal donate buttons everywhere and beg for donations
  - Alternatively, this would be fantastic to offer to investors to monetize, e.g. sell the app down the road

## Big Objectives:

### Classroom

- TEACHER can add grades for assignments / tests taken
  - this must be streamlined and an easy, super-simple interface to use
  - supports uploading attachments out-of-the-box
  - can attach items to A) the overall assignment, B) individual student's assignments / tests
  - teacher uses the companion app to easily scan images, etc. and auto-attach to an assignment / test
- STUDENT can take tests / do assignments
  - basic quizes
  - multiple choice
  - long answer
  - an answer key can be added before or afterwards for quizes
  - easy to upload attachments for A) overall quiz, or B) individual questions
- TEACHER can add an attachment to an item:
  - direct upload (Amazon S3) - file picker or drag-and-drop
  - url (for images) - copyright covered under Fair Use
  - supported attachment types:
    - image
    - video
    - audio
    - pdf
    - doc (txt, docx, doc, rtf, etc.) - (automatically convert docs to pdf??)
- TEACHER can quickly create assignments and quizzes using pre-built templates
  - quizzes are gamified
    - option to show correct/incorrect immediately
    - option to allow editing an existing question (can limit the number of total corrections)
    - option to allow student to see their score after taking a quiz
  - option to add explanations for why a certain answer is correct
  - subtle animations
    - next question slides in from the right
- STUDENT is able to take a quiz in an accessible way
  - text reader automatically enabled for all questions
  - text transcripts automatically enabled for audio speech
  - colors and animations are accessible

### Classroom / School Integration

- TEACHER can see semester / school-year for each assignment if connected to a school
  - items (assignments, etc) are auto-connected to the matching school-year and semester

### School Admin

- SCHOOL ADMIN can add/remove/update school years and semesters
- SCHOOL ADMIN can see at a glance various metrics of the school
  - number of tests taken by date range
  - average score per test
  - student engagement, satisfaction survey
