# KASPT User Guide

Version 1.0.0 Experimental

## 1. Installation

1. Download `KAST-1.0.0-exp.exe`.
2. Close any running copy of KASPT.
3. Run the installer.
4. Select a dedicated writable folder, such as `C:\Users\YourName\KASPT` or `E:\KASPT`.
5. The installer places `KASPT.exe`, `Uninstall KASPT.exe`, question data and the `Profiles` folder inside that exact location.

The installer creates Start-menu entries. It does not place the executable on the desktop.

To upgrade, run the newer installer and select the existing KASPT installation folder. Existing profiles are retained.

## 2. Profiles

At startup, KASPT detects saved profiles from the `Profiles` folder beside `KASPT.exe`.

- Select **Create new profile** to enter a name and creation date.
- Select an existing profile to continue its learning history.
- Select **Try without saving** to use a temporary profile. Temporary tests do not write responses or analytics.

Each saved profile has its own `performance.db`, so histories remain separate.

## 3. Appearance and display scaling

Select **Appearance** from the profile, home or analytics screen.

- **Auto** fits the interface to the available screen.
- Manual scaling accepts values from 25% to 200%.
- The slider and percentage presets provide quick adjustments.
- Available fonts are Cambria, Palatino, Georgia, Segoe UI, Times New Roman, Book Antiqua, Garamond and Constantia.

Requests larger than the current window can display are safely capped. Increase the window size or maximise KASPT to permit a larger effective scale.

## 4. Starting a test

From the profile home screen:

- **Run PCMB trial** starts the included 60-question Class 10 Physics, Chemistry, Mathematics and Biology test.
- **Try all question types** starts a short demonstration covering every supported interaction.
- **Import JSONL bank** lets you choose a custom question file. Its matching encrypted `.answers.atk` file must be available.

Supported types are:

- MCQ — single correct
- MCQ — multiple correct with proportional partial credit when no wrong option is selected
- MSQ — GATE style, requiring the exact complete answer set
- FITB — fill in the blank
- NAT — numerical answer with optional tolerance
- Match the following

Negative marking can be enabled or disabled independently for each question.

## 5. Question workflow

Every question follows three stages.

### Before solving

Record perceived difficulty, confidence and the expected outcome. The question remains visible while this review is completed.

### Answering

Select options or type the required answer. Questions may be marked for later review. Timing is recorded automatically.

### After the solution

After submission, inspect the correct answer and solution, classify what caused the result, mark whether the solution is understood, optionally add the question to the revision queue, and write a custom reflection.

Important transitions are saved immediately for persistent profiles.

## 6. Analytics

Select **Open analysis** from the profile home screen.

### Basic analysis

The basic view shows completed tests, marks earned, accuracy, recorded time, subject performance and topic performance.

### Reviews and reflections

1. Open **Reviews & reflections**.
2. Select a question file. Each file card shows question count, test count, accuracy and revision items.
3. Select a question from the left side.
4. Use the mouse wheel or blue scrollbar to move continuously through every question in the selected file.
5. Review the prompt, chosen answer, correct answer, timing, pre-solution assessment, post-solution outcome and saved reflection.
6. Select **All question files** to return to the file library.

This file-first layout prevents very large histories from becoming one enormous sequence of question pages.

## 7. Backup and AI analysis

The complete profile is stored at:

```text
<installation folder>\Profiles\<profile folder>\performance.db
```

To back up a profile, close KASPT and copy its entire profile folder to another safe location.

Some AI tools can inspect SQLite databases. A user may intentionally upload `performance.db`, but it can contain the profile name, question text, selected and correct answers, timing, confidence, revision status and private written reflections. Uploading it changes the local-only privacy model, so do this only with a trusted service.

## 8. Uninstallation

Close KASPT and run `Uninstall KASPT.exe`, use the Start-menu uninstall shortcut, or remove KASPT through Windows Installed Apps.

The uninstaller asks whether saved profiles should also be removed:

- **Yes** removes KASPT and profiles.
- **No** removes the application but keeps the `Profiles` folder.
- **Cancel** performs no removal.

Back up important profiles before choosing to delete them.
