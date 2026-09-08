# Project instructions

## Project
- This is a Drupal 10 project.
- Local environment: DDEV on WSL2.
- Project root: `/home/ghost/workspace/sklo`
- Drupal docroot: `web`
- Local URL: `https://sklo.ddev.site`
- PHP version: 8.4
- Web server: nginx-fpm
- Database: MariaDB.

## General rules
- Work only inside this project unless explicitly asked otherwise.
- Before making changes, inspect the existing implementation and follow the project's current conventions.
- Prefer the smallest safe change that solves the task.
- Do not refactor unrelated code.
- Do not modify generated or third-party code unless explicitly requested.

## Drupal rules
- Never edit Drupal core in `web/core`.
- Never edit Composer-installed dependencies in `vendor`.
- Do not edit contributed modules in `web/modules/contrib` unless explicitly requested.
- Do not edit contributed themes in `web/themes/contrib` unless explicitly requested.
- Custom functionality should normally live in:
  - `web/modules/custom`
  - `web/themes/custom`
- Follow Drupal 10 APIs and coding practices.
- Prefer dependency injection over direct service container access in application code where appropriate.
- Avoid deprecated Drupal APIs.
- Preserve existing configuration and site behavior unless the task explicitly requires changing them.

## DDEV
Use DDEV commands from the project root.

Preferred commands:
- `ddev drush ...`
- `ddev composer ...`
- `ddev exec ...`

Do not run a separate local PHP, Composer, Drush, database server, or web server when the same operation can be performed through DDEV.

## After PHP / Drupal code changes
Run appropriate validation when practical.

At minimum:
1. Check changed PHP files for syntax errors.
2. Run `ddev drush cr`.
3. Review errors produced by the command.

For PHP syntax checking, use DDEV, for example:
`ddev exec php -l <file>`

If the project has relevant automated tests or coding-standard tools, run the smallest relevant set.

## Composer
- Use `ddev composer`, not host Composer.
- Do not run `composer update` unless explicitly requested.
- Do not make broad dependency upgrades as part of an unrelated task.
- If a Composer dependency change is necessary, explain why before making a broad change.

## Database
- Do not delete, truncate, reset, import, or recreate the database unless explicitly requested.
- Do not run destructive SQL without explicit approval.
- Read-only database inspection is allowed when useful for diagnosing a problem.
- Prefer Drupal APIs and Drush over direct database changes.

## Configuration
- Do not import all Drupal configuration with `drush cim` unless explicitly requested.
- Do not export or overwrite configuration unrelated to the current task.
- If a task changes configuration, identify exactly which configuration objects are affected.

## Git
Before substantial changes, inspect the current working tree:
`git status --short`

Do not:
- discard existing user changes;
- use `git reset --hard`;
- force checkout files;
- amend commits;
- create commits;
- push;
unless explicitly requested.

After changes:
- inspect `git diff`;
- summarize which files were changed and why.

Treat pre-existing uncommitted changes as user work and preserve them.

## Safety
Ask before performing potentially destructive or irreversible actions, including:
- deleting files;
- destructive database operations;
- resetting Git state;
- replacing large sets of files;
- broad dependency upgrades;
- importing/restoring databases;
- changing DDEV project configuration in a way that may disrupt the environment.

## Task workflow
For normal development tasks:
1. Understand the request.
2. Locate the relevant custom code.
3. Inspect related implementation before editing.
4. Make the minimal necessary change.
5. Validate the changed code.
6. Run `ddev drush cr` when appropriate.
7. Inspect `git diff`.
8. Report:
   - what was changed;
   - which files were changed;
   - what validation was run;
   - whether anything remains uncertain.

If there is uncertainty about project-specific behavior, inspect the code or configuration rather than guessing.