# Contributing Guide

This document aims to describe the workflows and rules used for developing the projects on Github.
This includes but not limited to:

- guidelines how open issues about requested features or bugs
- how issues should be handled (labeling, when to close issues, etc.)
- general guidelines for how to handle pull requests (review, merge)

> __Note:__ This guideline only focus on describing how we use Github, for development related guides
please see our internal documentation.

## Roles

Every project/repository we manage on Github has three type of contributor.

### Developer

Developers are assigned to a project for a specific amount of time (ideally at least a full sprint length). 
Their main role is to:

- contribute code to the project based on the assigned task
- define/write subtasks when requested by project lead
- review PRs of other developers

### Project Lead

The project lead is a mixed management and technical position, it's an experienced (senior) developer overseeing the
status of the project at all times. Optimally there is a single project lead from start to end and his/her main role is to:

- take part in meetings and translate business requirements into technical issues
- plan the technical aspects of the project (with review of a lead developer)
- organize the work with the developers (tasks, meetings, estimations)
- write epics and issues for the developers
- review the code of other developers working on the project
- may or may not contribute code to the project

### Tester

Testers are (internal or external) responsible for testing features marked as ready and provide feedback for the developers.
This role is a mixed one, sometimes the "tester" will be project lead or the customer for smaller projects. Their main role is to:

- test features or fixes marked as ready for testing (and close them if accepted)
- provide feedback about the tested features to the project lead or developers (depending on the situation)

## Issues and tasks

### Opening issues

Before opening an issue please make sure, you have:

- read the documentation
- searched open issues for an existing issue with the same topic
- search closed issues for a solution or feedback

If you haven't found any _related open issue_, please open a new one. A well-written issue has the following traits:

- follows the issue template
- contains the reasoning or description of the feature or fix
- contains a minimal, inlined code example showcasing the problem of the proposed feature
- includes links to prior discussion if you have found any
- uses proper English, if you are not a native speaker (neither most of us) and you have grammar mistakes that are not a problem,
but take your time and write the description as good as you can, low effort posts may be closed without further comment

### Issue life-cycle

To be written: how we assign labels to issues and some graph probably

### Labelling issues

We use a well-defined list of labels to organize the issues opened. Labels are grouped into different categories
identified by their prefix. Below you can find the detailed list of labels we use for issue management
and their purpose.

#### Type labels

Every opened issue has a type, assigned after creation. It is uncommon to change the type label on an issue but it
can happen. We have the following types:

<details>
<summary>List of all type labels (click to open)</summary><br/>

`type: epic`  
A special container ticket tracking the progress of larger blocks of work. This kind of issue can be only closed by
a project lead. This type of label has no estimation.

`type: feature`  
Issues requesting new features with a clear initial definition of what that feature should be. The proposal may be
changed during the discussion before the implementation.

`type: fix`  
Reports of broken functionality about existing functionality.

`type: discussion`  
Issues where we can start iterating over ideas that are not yet exactly defined. The output of a discussion
ticket should be one or more new epic or feature request tickets after an agreement is reached on what the given
functionality should be. This type of label has no estimation.

`type: docs`  
Issues about adding documentation about a fix or feature. This documentation can have many form: guide in our internal
documentation, project documentation, API documentation, Q&A style doc in StackOverflow Teams.

`type: build`  
Issues about the project tooling not related to the source code.

`type: perf`  
Issues about increasing the performance of some functionality what works properly just not fast enough.

`type: refactor`  
Issues about improving code quality without changing functionality.

`type: test`  
Issues about extending or adding missing test for existing functionality.

</details>

#### Status labels

During an issue's life-cycle it must always have a single `status: *` label which reflects the current state of the issue.
Currently, we differentiate between the following statuses:

<details>
<summary>List of all status labels  (click to open)</summary><br/>

`status: in progress`  
Issue or PR with the assignee actively working on it.

`status: in review`  
Issues or PRs which are currently awaiting review

`status: merged`  
The issue has been fixed and merged into `develop` but not yet released.

`status: ready for testing`  
The issue has been fixed and merged into `develop` or `master`, and released. The `environment: *` label will signal
which environment this feature or fix is released.

`status: done / resolved`
Issue has been completed, no further action is needed, the issue can be closed.

`status: blocked`  
The task in the given issue is blocked by some other work tracked in a different issue. When this label added the
blocking issue should be referenced in a comment on the issue.  

`status: superset by another`  
The task is already tracked in a different issue. When adding this label a reference should be added as a comment to
the issue tracking the task.

`status: needs triage`  
Typically bug reports will be marked as needs-triage until a someone verifies the issue
and posts a minimal reproduction use-case as an __inline code snippet__ to be used as a reference.

`status: cannot reproduce`  
This label is assigned when the bug report cannot be reproduced by the developer(s). An issue marked
with this label can be closed only after it was discussed with the project lead.

`status: expired / unknown`  
Issues which has been closed because they are not relevant anymore or contains outdated information.

`status: wontfix`  
The issue won't be fixed as the observed functionality is by design.

`status: on hold`  
This is a special label assigned by the project lead and no-one can work on the given task until this label is removed
by the project lead.

</details>

#### Scope labels

Scope labels are project-specific and defined for every project. They represent major parts of the given project.
Some examples would be: `scope: core` or `scope: auth`.

#### Effort and complexity labels

These labels are assigned during the estimation of issues. The `effort<x>: *` labels describe the ideal time required
for the task to be completed. This estimation should include everything needed to finish the task, so meeting and
code reviews as well but not deployment. The complexity of a ticket signals how likely the developer will encounter an
unforeseen obstacle during implementation.

#### Estimation group labels

These labels are used only by the project manager and links our internal tickets to the estimation sent to the customer.
For example we may send an estimation for the customer to implement the required authentication method in x days as a
single entry in the external estimation, but that task will consists multiple sub-tasks in our internal tracking.

#### Flag labels

These labels can be assigned to issues or PRs to indicate additional work.

<details>
<summary>List of all flag labels  (click to open)</summary><br/>

`flag: estimation needed`  
Most common flag, every created task has this label as they must be estimated before implementation can start.

`flag: refactor needed`  
This flag can be assigned to PRs signaling that the implementation is not acceptable and should be reworked before being merged.

`flag: business review needed`  
The issue __requires further discussion before implementation__ as it doesn't clarify the business requirements
well enough.

`flag: technical review needed`  
The issue __requires further discussion before implementation__ as it doesn't meet technical or some other
requirement.

`flag: docs improvement needed`  
This label is assigned by the project lead, when the issue is too vague to start implementation and requires
additional clarification from the developer. (Sub-tasks are written by developers in some cases.)

`flag: breaking change`  
The issue or PR contains a breaking change that requires a major version bump.

`flag: incident report`  
The issue contains a description and post-mortem about an issue in production what affected the customers.

`flag: schema modification`  
The issue requires changes to the DB structure. (This label may not be used in smaller projects.)

`flag: technical debt`  
The issue is about removing some technical debt.

</details>

## Contributing code

In general, any code to be accepted into the default branch must confront the following criteria:

- the proposed changes should be discussed prior to implementation
- the proposed changes should have a related tracking issue which is referenced in the PR
- the required checks on the PR must pass (preferably the optional checks also)
- must have at least two accepted code review from _developers_ or a single accepted review from _project lead_
- the provided code must be tested properly
- the change should include documentation changes if applicable  

### Discussion before implementation

One of the most important rules of code contribution is to __discuss your changes in advance__! If you have not
completed a similar task before and not 100% sure of how the problem should be solved it's better to ask early instead
of creating something which has to be re-done. This statement is especially true for colleagues who just joined.  

In short, most PRs will be blocked immediately if it contains a new implementation of something we have a standard way
of doing.

### Opening PRs and code reviews

When you have created an implementation for a feature that has been discussed and approved by the project lead, you need
to open a PR against the default (`develop`) branch on the repository. Every opened PR should

- follow the PR template
- reference it's tracking issue

_Note_: If you are an outside contributor for an open source project we suggest to enable the setting in the PR which
allows the _maintainers_ to push to the given branch. This will allow them to push quick fixes to the branch before
merging instead of asking you to do it.  

After you have created the PR it will be reviewed by one or more developers. They may request some extra changes to
be made. When all reviewers approved the PR will get merged and included in the next release.

### Commit guidelines

We use the lite version [Angular commit message guidelines][angular-commit-guidelines] for our commit messages.
This means every commit must confront the header format:

```text
<type>(<scope>): <short summary>
  │       │             │
  │       │             └─⫸ Summary in present tense. Not capitalized. No period at the end.
  │       │
  │       └─⫸ Commit Scope: defined by the project contributing guidelines
  │
  └─⫸ Commit Type: build|ci|docs|feat|fix|perf|refactor|style|test
```

The `<type>` and `<summary>` fields are mandatory, the (`<scope>`) field is optional.

> __Note:__ The project-specific scopes can be found in the project-specific contribution guides.  

The `<type>` must be one of the following values:

- `feat`: A new feature
- `fix`: A bug fix
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `test`: Adding missing tests or correcting existing tests
- `docs`: Documentation only changes
- `perf`: A code change that improves performance
- `build`: Changes that affect the build system or external dependencies
- `ci`: Changes to our CI configuration files and scripts

### Disallowed code contributions

Some areas are managed centrally through the organization and don't accept code contributions from developers. 
This doesn't mean you cannot open issues to propose or discuss changes to these areas, but the code
itself will be added by a _lead developer_ most of the time. Proposed changes to these areas must have strong reasoning
on why they should be changed.

These areas currently include:

- our CI configuration
- some of our used dev dependencies:
  - testing framework and it's configuration (Jest)
  - code coverage tool and it's configuration (Codecov)
  - code formatting and it's configuration (Prettier)
  - our linter and it's configuration (ESLint)

### Merging PRs

In every repository two merge option is enabled: squash and merge.

- if a PR has a single commit or the changes across commits are logically grouped use squash
- if a PR has multiple commits which are not logically grouped together use a merge commit

When merging please make sure to use the following merge commit message format:

```text
merge: <summary of changes> (#<GH issue number>)
```

## Releasing

Most repository is configured to release a new version from the project when a Github Release is created from a tag.
This means any member with push access can create a release.

> __Note:__ The actual NPM publish is made by a bot from the source code on Github so invalid versions cannot be
released by any _maintainer_ without merging those changes into the `master` branch first. (What would be discovered.)

Before a release the following steps must be done:

- decide what version bump this release needs (patch, minor, major)
- changelog is added in a comment for the given release (issues w/ `status: merged`)
  - the commit should be named `docs: add changelog for <x>.<x>.<x>`
  - the commit should contain only the changelog change
- the version number is raised in `package.json`
  - the commit should be named `build: bump version to <x>.<x>.<x>`
  - the commit should contain only the version bump change
- a new PR is opened from `develop` into `master`
  - the PR should be titled `release: <x>.<x>.<x>`
  - after review, the PR __should be merged with a merge commit__ named `merge: release <x>.<x>.<x>`
- the git tag with the same version is added to the merge commit (this can be done locally or on Github)
  - the git tag must have the `v` prefix and the version number, eg: `v1.4.2`
- a release is created from the git tag on Github
- the maintainer who merged the release PR should wait and see if the CD task successfully releases the project to NPM
- all issues w/ `status: merged` label released in this version should be closed as done

[angular-commit-guidelines]: https://github.com/angular/angular/blob/master/CONTRIBUTING.md#-commit-message-format