## What is this?
This is a script that runs a linter (ktlint) for Android projects and automatically formats code right before doing a git push.
Using this script formats only the changed files in a PR and makes a separate commit for it (if ktlint was able to run w/o errors).

## Who is this designed for?
Large codebases that have not yet setup a linter. The reason to use this is to avoid doing a one-time lint run across an entire codebase which will mess up git blame and could be a lot of work to fix all the errors.

## Installation instructions
