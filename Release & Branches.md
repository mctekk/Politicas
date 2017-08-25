# Branch Naming

## Primary

We'll be using three main branches.
<table>
  <thead>
    <tr>
      <th>Branch</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>development</td>
      <td>This is the version where changes and new features are integrated to. (Connects to a development database.)</td>
    </tr>
    <tr>
      <td>staging</td>
      <td>This is the version used for testing purposes before any code is pushed into production. (Connects to the production database.)</td>
    </tr>
    <tr>
      <td>production</td>
      <td>This is the production version. (Connects to a production database.)</td>
    </tr>
   
  </tbody>
</table>

Any additional branches will be added as per requirement per project.

## Secondary

Secondary branches are those that poses importance for the project; such as new features, major code changes and application wide bug fixes. The life span of these branches should not be greater than 1 month and must be deleted by their creators with prior notification to the Project Manager.

### Branch naming conventions

Examples:
- sprint-1 (code corresponding to sprint 1)
- feature-reports (new reports feature being developed)
- feature-login (user authentication being developed)
- feature-site (landing page for the project)

## Temporary

Temporary branches should be named after the action being performed in them. These are to be worked locally and should only be uploaded by the developer in case they need to save the code (for example, if the developer hasn't finished his task and has to leave the office).

Examples:

Correction to errors in reports
- fix-reports (general fixes to reports)
- fix-reports-sellers (fixes to reports related to sellers)
- fix-reports-buyers (fixes to reports related to buyers)

Branches should be named clearly as to indicate the purpose of their creation.

Examples of names that shouldn't be used:
- not-working
- bug-reported
- fixes

## Merges to Primary Branches

Merges going into the primary branches are to be performed in the following way.

**Merges from secondary branches into development**

Example:
```sh
(development)$ git merge feature-reports
```

**Merges from *development* into *staging***

Example:
```sh
(staging)$ git merge development
```

**Merge from *staging* into *master*** *(Only Project Manager)*

Example:
```sh
(master)$ git merge staging
```

## Bug Fixes and Patches in *staging*

Errors discovered in *staging* by end users are to be resolved directly by branching *staging*. This is an exception to pushes into primary branches. Branch names must have the prefix *hotfix-* so that these are easily identified as corrections to *staging*.

*Steps:*
1. Creating a branch from *staging*
```sh
(staging)$ git branch hotfix-something
```

2. Correct and merge the branch created from *staging*
```sh
(staging)$ git merge hotfix-something
```

3. Merge fixes into *master* and into *development*
```sh
(master)$ git merge staging 
(development)$ git merge staging 
```

## Important Changes

If the application will suffer drastic changes a new branch must be created. This new branch will be named *"&lt;branch&gt;-pre-/&lt;branch&gt;-post-"* in order to recover any changes, should it be necessary.

Examples:
```
development-pre-vue
development-post-mandrill
```

## Messages in commits

When committing a concise description of the changes have to be added. If these changes are tied to a task in JIRA a relationship can be defined by adding the task key separated by a dash with spaces ( - ) before the description.

>Getting in the habit of creating quality commit messages makes using and collaborating with Git a lot easier. As a general rule, your messages should start with a single line that’s no more than about 50 characters and that describes the changeset concisely, followed by a blank line, followed by a more detailed explanation. The Git project requires that the more detailed explanation include your motivation for the change and contrast its implementation with previous behavior – this is a good guideline to follow. It’s also a good idea to use the imperative present tense in these messages. In other words, use commands. Instead of "I added tests for" or "Adding tests for," use "Add tests for." 

_**Source:** [Contributing to a Project](https://git-scm.com/book/ch5-2.html)_

Examples:
```
(development)$ git commit -m "PRJ-151 - Correcting problems with login."
```

# Versioning

We will be working with Semantic Versioning 2.0.0 ([semver](http://semver.org) [MAJOR.MINOR.PATCH])

1. MAJOR version when you make incompatible API changes,
2. MINOR version when you add functionality in a backwards-compatible manner, and
3. PATCH version when you make backwards-compatible bug fixes.

These will be assigned to project releases.

Examples:
* 1.0.0 - First alpha release of the project.
* 1.0.1 - Quick changes / bug fixes
* 1.1.0 - New feature
* 1.2.5 - New feature and bug fixes

Releases with versioning will be published at the end of each sprint, unless any specific conditions prevent from doing so.

# FAQ

#### Who can push changes into production (*master*)?
Project Managers or assigned personnel are the only ones allowed to push changes into production.

#### Can emergency fixes be pushed into production without the presence of the Project Manager?
* Emergency fixes should NEVER be pushed into production. All changes must go through *development* or *staging* (in case of hotfixes).
* The responsibility of having these changes pushed into production fall entirely under the Project Manager. Should the PM not be available you can seek help from someone else with the authority to do suck tasks in order to reach a solution.

#### I have conflicts with a branch because someone else uploaded one the same name, what should I do?
Change the name of your branch by adding a suffix **bk**_(backend)_ or **ft**_(frontend)_ while maintaining the already established branch naming guidelines.

Example:
```sh
git branch -m feature-reports feature-reports-bk
```

#### What happens if I upload a temporary branch?
Any uploaded temporary branches must be deleted in order to avoid having an overwhelming amount of branches in the online repository.
