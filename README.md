# Pre-push linter script for Android projects

## What is this?
This is a script that runs a linter ([ktlint](https://pinterest.github.io/ktlint/latest/)) for Android projects and automatically formats code right before doing a git push.
Using this script formats only the changed files in a PR and makes a separate commit for it (if ktlint was able to run w/o errors).

## Who is this designed for?
Large codebases that have not yet setup a linter. The reason to use this is to avoid doing a one-time lint run across an entire codebase which will mess up git blame and could be a lot of work to fix all the errors.

## Installation instructions
1. Create a folder in your project in Android Studio at the top level called `scripts` if it doesn't exist already.
2. Save the [`pre-push`](https://github.com/adamc01/pre-push-linter/blob/main/pre-push) file in this repo to the scripts directory just created.
3. In your project-level `build.gradle` file, add the following code:
```
task installGitHook(type: Copy) {
    from new File(rootProject.rootDir, 'scripts/pre-push')
    into { new File(rootProject.rootDir, '.git/hooks') }
    fileMode 0777
}

tasks.getByPath(':app:preBuild').dependsOn installGitHook
```
After building the app gradle will place the script (and overwrite if already exists) in your .git/hooks directory.

## To skip the linter when pushing to git
Add `--no-verify` to your git command to skip the linter.  
e.g., `git push origin develop --no-verify`
