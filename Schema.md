# KASPT Question Bank Schema

KASPT custom tests use two files:

```text
my_bank.jsonl
my_bank.answers.atk
```

- `my_bank.jsonl` contains the questions.
- `my_bank.answers.atk` is the packaged answer key.
- The answer key is first written as plaintext JSONL and then converted to `.atk` with `answerkey_tool.exe`.

## JSONL rules

JSONL means one complete JSON object per line.

- Do not wrap the file in `[` and `]`.
- Do not put commas between lines.
- Save it as UTF-8.
- Every `question_id` must be unique within that question file.
- The question and answer files must contain exactly the same set of `question_id` values.

## Common question fields

| Field | Required | Type | Description |
|---|---:|---|---|
| `question_id` | Yes | string | Unique ID within this bank. |
| `subject` | Yes | string | Subject used in analytics. |
| `question_type` | Yes | string | Supported type listed below. |
| `question` | Yes | string | Question prompt. |
| `topic` | No | string | Topic used in analytics. |
| `subtopic` | No | string | Optional finer category. |
| `marks` | No | number | Positive marks for a correct response. Default: `1`. |
| `negative_marking` | No | boolean | Enables or disables negative marking. |
| `negative_marks` | No | number | Non-negative penalty. A positive value enables negative marking when `negative_marking` is omitted. |
| `difficulty` | No | string | Label such as `Easy`, `Medium`, or `Hard`. |

## Supported question types

### MCQ — single correct

Use `"question_type":"MCQ_SINGLE"`. The legacy value `MCQ` is also accepted.

The `options` array is required and must contain 2 to 8 strings. Options are labelled `A`, `B`, `C`, and so on in array order.

Question:

```json
{"question_id":"S1","subject":"Science","topic":"Numbers","question_type":"MCQ_SINGLE","question":"Which number is prime?","options":["21","29","39","51"],"marks":1,"negative_marking":true,"negative_marks":0.25,"difficulty":"Easy"}
```

Plaintext answer:

```json
{"question_id":"S1","correct_answer":"B","solution":"29 is divisible only by 1 and 29."}
```

### MCQ — multiple correct with partial marks

Use `"question_type":"MCQ_MULTIPLE"`.

The `options` array is required and must contain 2 to 8 strings. Proportional partial credit is awarded only when at least one correct option and no wrong option is selected.

Question:

```json
{"question_id":"M1","subject":"Science","topic":"Energy","question_type":"MCQ_MULTIPLE","question":"Select all renewable energy sources.","options":["Solar","Coal","Wind","Natural gas"],"marks":4,"negative_marking":true,"negative_marks":1}
```

Plaintext answer:

```json
{"question_id":"M1","correct_answers":["A","C"],"solution":"Solar and wind are renewable energy sources."}
```

### MSQ — GATE style

Use `"question_type":"MSQ"`.

The `options` array is required and must contain 2 to 8 strings. The complete correct set must be selected; no partial credit is awarded.

Question:

```json
{"question_id":"G1","subject":"Mathematics","topic":"Geometry","question_type":"MSQ","question":"Select every true statement about a square.","options":["Its diagonals are equal","Its diagonals are perpendicular","Every rhombus is a square","All angles are right angles"],"marks":2,"negative_marking":false}
```

Plaintext answer:

```json
{"question_id":"G1","correct_answers":["A","B","D"],"solution":"A square has equal perpendicular diagonals and four right angles."}
```

### FITB — fill in the blank

Use `"question_type":"FITB"`. No `options` field is required.

Question:

```json
{"question_id":"F1","subject":"Biology","topic":"Cells","question_type":"FITB","question":"The powerhouse of the cell is the ____.","marks":1,"negative_marking":false}
```

Plaintext answer:

```json
{"question_id":"F1","accepted_answers":["mitochondrion","mitochondria"],"solution":"Mitochondria produce most cellular ATP."}
```

`correct_answer` may be used instead when only one spelling is accepted.

### NAT — numerical answer type

Use `"question_type":"NAT"`. No `options` field is required.

Question:

```json
{"question_id":"N1","subject":"Mathematics","topic":"Arithmetic","question_type":"NAT","question":"Enter 10 divided by 4.","marks":2,"negative_marking":false}
```

Plaintext answer:

```json
{"question_id":"N1","numeric_answer":2.5,"tolerance":0.001,"solution":"10 / 4 = 2.5."}
```

`tolerance` is optional, defaults to `0`, and cannot be negative.

### Match the following

Use `"question_type":"MATCH"`.

- `match_left` and `match_right` are required.
- Both arrays must have the same length.
- Each array must contain 2 to 4 strings.
- Left items are labelled `A`, `B`, `C`, `D`.
- Right items are numbered `1`, `2`, `3`, `4`.

Question:

```json
{"question_id":"T1","subject":"Physics","topic":"Units","question_type":"MATCH","question":"Match each quantity with its SI unit.","match_left":["Force","Power"],"match_right":["Watt","Newton"],"marks":2,"negative_marking":false}
```

Plaintext answer:

```json
{"question_id":"T1","correct_matches":["A-2","B-1"],"solution":"Force is measured in newtons and power in watts."}
```

Every left label and right number must be used exactly once.

## Plaintext answer-key fields

| Question type | Required field |
|---|---|
| `MCQ_SINGLE` | `correct_answer` containing one option letter |
| `MCQ_MULTIPLE` | `correct_answers` containing an array of option letters |
| `MSQ` | `correct_answers` containing the exact array of option letters |
| `FITB` | `accepted_answers`, or `correct_answer` for one accepted value |
| `NAT` | Numeric `numeric_answer`; optional numeric `tolerance` |
| `MATCH` | `correct_matches` containing mappings such as `A-2` |

All answer objects may include an optional `solution` string.

## Complete six-question example

`example.jsonl`:

```jsonl
{"question_id":"S1","subject":"Science","topic":"Numbers","question_type":"MCQ_SINGLE","question":"Which number is prime?","options":["21","29","39","51"],"marks":1,"negative_marking":true,"negative_marks":0.25}
{"question_id":"M1","subject":"Science","topic":"Energy","question_type":"MCQ_MULTIPLE","question":"Select all renewable energy sources.","options":["Solar","Coal","Wind","Natural gas"],"marks":4,"negative_marking":true,"negative_marks":1}
{"question_id":"G1","subject":"Mathematics","topic":"Geometry","question_type":"MSQ","question":"Select every true statement about a square.","options":["Its diagonals are equal","Its diagonals are perpendicular","Every rhombus is a square","All angles are right angles"],"marks":2,"negative_marking":false}
{"question_id":"F1","subject":"Biology","topic":"Cells","question_type":"FITB","question":"The powerhouse of the cell is the ____.","marks":1,"negative_marking":false}
{"question_id":"N1","subject":"Mathematics","topic":"Arithmetic","question_type":"NAT","question":"Enter 10 divided by 4.","marks":2,"negative_marking":false}
{"question_id":"T1","subject":"Physics","topic":"Units","question_type":"MATCH","question":"Match each quantity with its SI unit.","match_left":["Force","Power"],"match_right":["Watt","Newton"],"marks":2,"negative_marking":false}
```

`example.answers.plain.jsonl`:

```jsonl
{"question_id":"S1","correct_answer":"B","solution":"29 is divisible only by 1 and 29."}
{"question_id":"M1","correct_answers":["A","C"],"solution":"Solar and wind are renewable energy sources."}
{"question_id":"G1","correct_answers":["A","B","D"],"solution":"A square has equal perpendicular diagonals and four right angles."}
{"question_id":"F1","accepted_answers":["mitochondrion","mitochondria"],"solution":"Mitochondria produce most cellular ATP."}
{"question_id":"N1","numeric_answer":2.5,"tolerance":0.001,"solution":"10 / 4 = 2.5."}
{"question_id":"T1","correct_matches":["A-2","B-1"],"solution":"Force is measured in newtons and power in watts."}
```

## Packaging the answer key

Convert the plaintext answer file into the `.atk` file used by KASPT:

```powershell
.\answerkey_tool.exe example.answers.plain.jsonl example.answers.atk
```

Verify that the question file and packaged answer key match:

```powershell
.\answerkey_tool.exe --verify example.jsonl example.answers.atk
```

Keep `example.jsonl` and `example.answers.atk` together. When importing `example.jsonl`, KASPT automatically looks for `example.answers.atk`; if it is elsewhere, the application asks you to select it.

Do not distribute the plaintext answer file.

## Security note

The ATK1 answer-key transformation prevents accidental spoilers and casual editing. It is obfuscation, not strong cryptographic encryption, and should not be treated as protection for a high-stakes examination against a determined attacker.
