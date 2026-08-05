# KASPT 1.0.0 Experimental

**KASPT — Knowledge Assessment Software with Performance Tracking** is a local-first Windows application for taking tests, reviewing mistakes, recording reflections, and analysing performance by subject, topic, question file, and individual response.

## Download

Download and run `KASPT-1.0.0-exp.exe` from this release.

This is an experimental Windows build. The installer may trigger a Windows security prompt because it is not currently code-signed. Only run a copy obtained from the official KASPT release page.

## Highlights

- MCQ single-correct and multiple-correct questions
- GATE-style MSQ questions
- Fill in the blank, numerical-answer and match-the-following questions
- Optional per-question negative marking
- Pre-solution confidence and difficulty review
- Post-solution classification, revision flags and written reflections
- Subject-wise and topic-wise offline analytics
- File-first review browser with a continuously scrollable question list
- Automatic or manual interface scaling from 25% to 200%
- Eight selectable global fonts
- Separate local databases for every profile
- Temporary no-save profile for trying the application

## Privacy and saved data

KASPT does not require an account or internet connection. Profiles, responses, timing information and reflections are stored in:

```text
<installation folder>\Profiles\<profile folder>\performance.db
```

Uploading `performance.db` to an AI service is optional and causes that profile data to leave the computer. Review the service's privacy terms before uploading it.

## Documentation

See [USER_GUIDE.md](USER_GUIDE.md) for installation, test-taking, analytics, backup and uninstall instructions.

## Experimental release notice

Back up the `Profiles` folder before important upgrades. Bug reports should include the KASPT version, Windows version, display scaling percentage and steps required to reproduce the problem. Do not publish a real `performance.db` with a bug report unless you intend to disclose its contents.

KASPT is distributed free of charge for use. Copyright is retained by its developer. All rights reserved.

## Release verification

At the time of packaging, KASPT passed all available tests and a Microsoft Defender scan. No known malware or critical problems were detected.
