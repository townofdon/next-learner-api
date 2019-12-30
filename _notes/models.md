
# Models

Note - models subject to change and probably will fall out of sync from this doc pretty quickly.
The database schema is ALWAYS the source of truth with regards to models. This doc was created
during the database planning phase and should be treated with a high degree of skepticism.

## Globals

- All models assume an auto-incrementing ID or UUID strategy for distinctness.
- All models have timestamp cols (`created_at`, `updated_at`).

## Model List

- `ContactProfile`
  - `name_first {string}`
  - `name_last {string}`
  - `name_middle {string}`
  - `name_other {string}`
  - `nickname {string}`
- `ContactProfileAddress`
  - `contact_profile_id {ID}` JOIN
  - `street_line_1 {string}`
  - `street_line_2 {string}`
  - `zip {string}`
  - `city {string}`
  - `state {string}`
- `ContactProfilePhoneNumber`
  - `contact_profile_id {ID}` JOIN
  - `value {string}`
  - `type {enum}` `home|work|other` default `home`
  - `type_other_description {string}`
- `ContactProfileEmail`
  - `contact_profile_id {ID}` JOIN
  - `value {string}`
  - `type {enum}` `home|work|other` default `home`
  - `type_other_description {string}`
- `User`
  - `contact_profile_id {ID}` JOIN
  - `role {enum}` `teacher|student|school_admin|system_admin`
  - `date_created {date}`
  - `date_updated {date}`
  - `name_first {string}`
  - `name_last {string}`
  - `name_middle {string}`
  - `name_other {string}`
- `Classroom`
  - `name {string}` - ex. "Spring 09"
  - `teacher_user_id {id}` JOIN
  - `semester_id {id}` JOIN
  - `name {string}`
  - `date_start {date}` - school_year / semester query will query by this col
  - `date_stop {date}` - school_year / semester query will query by this col
- `Test`
  - can be a test or an assignment - anything that is gradable
  - `author_id {id}` JOIN
  - `classroom_id {id}` JOIN - required if `is_template === false`
  - `is_template {bool}` - template tests/assignments are read-only and can be copied to a semester
  - `allow_retake {bool}`
  - `num_allowed_retakes {number}` default `1`
  - `name {string}`
- `TestQuestion`
  - `test_id {id}` JOIN
  - `is_active {bool}`
  - `type` `multi_select_one|multi_select_many|short_answer`
  - `score_weight {number}` - default `100`
  - `text {string}`
- `TestQuestionItem`
  - `test_question_id {id}` JOIN
  - `text {string}`
  - `image_url {string}`
  - `block_size_sm {number}` - always a percentage - default `100`
  - `block_size_md {number}` - always a percentage - default `100`
  - `block_size_lg {number}` - always a percentage - default `100`
  - `block_size_xl {number}` - always a percentage - default `100`
- `TestAnswer`
  - `test_question_id {id}` JOIN
  - `is_correct {bool}`
  - `content {string}`
  - `explanation_if_correct {string}`
  - `explanation_if_wrong {string}`
- `StudentTest`
  - `test_id {id}` JOIN
  - `student_id {id}` JOIN
  - VIRTUAL `score` - always an aggregate of individual answers - needs to be a cached column
- `StudentTestAnswer`
  - `student_test_id {id}` JOIN
  - `test_answer_id {id}` JOIN
  - `text {string}`
  - `score {number}`
  - `score_weight {number}` - assign to parent `TestQuestion` val onCreate - default `100`