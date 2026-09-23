# CMPE 272 Jenkins GitHub Project

This repository is used to demonstrate Jenkins integration, GitHub project management, and automated build triggering.

## Jenkins Integration

This repository is integrated with Jenkins for continuous integration. Jenkins checks the GitHub repository every five minutes and runs a build when changes are detected.

### Setup

- Jenkins 2.568.3 running locally as a Windows service at `http://localhost:8080`
- Git plugin (5.10.1) and GitHub plugin installed
- Job: `HW4-GitHub-Project` (Freestyle project)
  - Source Code Management: Git
  - Repository URL: `https://github.com/juileegiramkar/cmpe_272_HW_Jenkins_Github`
  - Branch Specifier: `*/main`
  - Build step: Windows batch command that prints a confirmation message and lists the checked-out files

### Build Trigger

The job uses **Poll SCM** with the schedule `H/5 * * * *`. Every five minutes, Jenkins runs `git ls-remote` against this repository. If `main` has a new commit, Jenkins starts a build, and the build page shows it as "Started by an SCM change". The job's **Git Polling Log** records each check.

A GitHub webhook would start builds right after a push instead of every five minutes. But GitHub must be able to reach the Jenkins server to send a webhook, and this Jenkins only runs on `localhost`. Polling works without making Jenkins public.

## GitHub Project

The work for this assignment is tracked in the GitHub Project **HW4 Jenkins GitHub Project** (owned by @juileegiramkar). The project includes:

- The issues from this repository, plus draft issues for follow-up ideas
- An **Iteration** field with one-week iterations
- A **Priority** single-select field (High, Medium, Low)
- A **Priority** table view grouped by priority
- A **Board** view with Todo, In Progress, and Done columns
- Built-in workflows:
  - Items added to the project get Status Todo
  - Closed issues and merged pull requests move to Done
  - New open issues in this repository are added to the project automatically
