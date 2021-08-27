# Development Workflow

## Table of Contents

* [Development Workflow](#development-workflow)
  * [Issues](#issues)
  * [Branches](#branches)
  * [Pull Requests (PR)](#pull-requests--pr-)
  * [Projects](#projects)
  * [Teams](#teams)
  * [Workflow Summary](#workflow-summary)

## Issues

Create an issue when:

* You find a bug: `bug`
* You have an idea for a feature: `feature`
* You have an idea that adds functionality to a feature: `enhancement`
* You have an idea to clean up some code: `refactoring`
* You have an idea to optimize some code: `optimization`
* You have an idea to improve UI/UX: `design`

**NOTE:**

* Issues can have different labels based on their type and the words like `this` correspond to their label names
* Issues can also be designated milestones which can correspond to particular sprints
* Issues can be added at any time but will be addressed as the need arises
* There will be a separate branch created for the issue when it's ready to be addressed

**REPORTING BUGS:**

* Include screenshots of visual error
* Include screenshots of console error
* Describe what actions you were performing when it happened
* Indicate when it happened (date + time + website version)
* Indicate where it happened (url)

## Branches

All repositories will have the following branches:

* `main`: this is the production branch that is currently deployed and live
* `dev`: this is the development branch with new features (which will be merged with the master branch for the next release)
* `fix`: this is the development branch with quick fixes for the main branch (fixes once commited, will be merged into the main branch and dev branch if necessary)

**IMPORTANT:** Never commit directly to the main and dev branch. They can be affected only by merging pull requests into them.

In addition to these three core branches all other branches will each address an issue at hand

NOTE:

* There will be a pull request created for each branch once it's ready to be reviewed
* All branches (except `fix`) MUST be deleted after their pull request has been successfully merged.
* No branch (except `fix`) can have more than one pull request.

## Pull Requests (PR)

When opening a PR for a branch the developer believes:

* they have addressed the requirements of the feature at hand to the best of their abilities
* the branch is ready to be reviewed by their peers for feedback on functionality and code quality

On opening a PR the developer should:

* Assign at least one team member to review their PR
* Wait for comments from the reviewer
* Dicuss and make changes as requested by the reviewer
* Wait for the reviewer to approve the pull request
* Merge the pull request into the `dev` branch
* Delete the merged branch

## Projects

* A project is a kanban board that Github provides to track issues and pull requests
* Useful for keeping a track of status and overall progress
* Separate projects could be used for each sprint

## Teams

* A simple way to isolate team members working in a particular division
* Enhances communication by preventing conversations from being diluted across the organization
* Easier to manage permissions and designate repositories at a team level

---

## Workflow Summary

```
1:1:1 ratio of issues, branches, and pull requests

issue -> branch -> pull request

Each issue is addressed only by one branch
Each branch only addresses one issue
Each branch has only one pull request opened in its lifetime
```

1. Pick an existing issue
2. Create a new branch from the `dev` branch to work on that issue
3. Commit all changes for that issue only to that branch
4. Once the issue has been addressed, open a pull request for that branch
5. Assign at least one other team member as a reviewer (preferably someone who's worked on that part of the code before)
6. If a reviewer has requested changes, discuss and make the corresponding changes if necessary until everyone is satisfied
7. Once all reviewers have approved the pull request, go ahead and merge the pull request into the `dev` branch and delete the pull request branch

*Once we are ready to release the next version of the software, the `dev` branch will be tested and then merged into the `main` branch, after which the code will be deployed into production*
