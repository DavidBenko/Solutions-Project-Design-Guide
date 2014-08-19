AnyPresence Solutions Project Design Guide
=====================

This guide describes a set of AnyPresence Solutions deliverable design practice. 

Our goals here are consistency and focusing on business logic while avoiding design bikeshedding. We’re looking for a good, consistent, well-documented way to design projects, not necessarily the only/ideal way.

Code Style and Best Practices
---------
**AnyPresence** develops on a number of platforms and arcitechures and utilizes many different programming languages to best complete the task at hand. Below is a list of style guides for each language, to which each **AnyPresence**-designed application should strive to uphold.

- [CoffeeScript](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md)
- [Java](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md)
- [JavaScript](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/javascript-style.md)
- [Objective-C](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md)

Project Collaboration
---------

**AnyPresence** uses git and [GitHub.com](http://github.com) to store and version project code. Repositories are separated by platform for each project and are registered under each respective client's GitHub account. 

#### Basic Design Pattern

##### Main Branches
At the core, the development model is greatly inspired by existing models out there. The central repo holds two main branches with an infinite lifetime:
- `master`
- `development`

The `master` branch at `origin` should be familiar to every Git user. Parallel to the `master` branch, another branch exists called `develop`.

We consider `origin/master` to be the main branch where the source code of `HEAD` always reflects a production-ready state.

We consider `origin/develop` to be the main branch where the source code of `HEAD` always reflects a state with the latest delivered development changes for the next release. Some would call this the "integration branch". This is where any automatic nightly builds are built from.

When the source code in the `develop` branch reaches a stable point and is ready to be released, all of the changes should be merged back into `master` via a pull request and then tagged with a release number. How this is done in detail will be discussed further on.

Therefore, each time when changes are merged back into `master`, this is a new production release by definition. We tend to be very strict at this, so that theoretically, we could use a Git hook script to automatically build and roll-out our software to our production servers everytime there was a commit on master.

##### Supporting branches

Next to the main branches `master` and `develop`, our development model uses a variety of supporting branches to aid parallel development between team members, ease tracking of features, prepare for production releases and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.

The different types of branches we may use are:
- Feature branches
- Release branches
- Hotfix branches

###### Feature branches
May branch off from: `develop`, must merge back into: `develop`. Branch naming convention: anything except `master`, `develop`, `release-*`, or `hotfix-*`.

- Creating a feature branch
```shell
$ git checkout -b myfeature develop
Switched to a new branch "myfeature"
```

###### Release branches
May branch off from: `develop`, must merge back into: `develop` and `master`. Branch naming convention: `release-*`.

- Creating a feature branch
```shell
$ git checkout -b release-1.2 develop
Switched to a new branch "release-1.2"
..
  Bump version number in code
..
$ git commit -a -m "Bumped version number to 1.2"
[release-1.2 74d9424] Bumped version number to 1.2
1 files changed, 1 insertions(+), 1 deletions(-)
```

###### Hotfix branches
May branch off from: `master`, must merge back into: `develop` and `master`. Branch naming convention: `hotfix-*`.

- Creating a feature branch
```shell
$ git checkout -b hotfix-1.2.1 master
Switched to a new branch "hotfix-1.2.1"
..
  Perform hotfix & bump version number in code
..
$ git commit -a -m "Bumped version number to 1.2.1"
[hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1
1 files changed, 1 insertions(+), 1 deletions(-)
```

#### Commit Messages and Completing Tickets

##### Commit message formats
Commit messages should be short, consise explanations about what was changed in the commit. The first line should always be 50 characters or less and that it should be followed by a blank line. 

- A good commit message example is: `Redirect user to the requested page after login`
- A bad commit message example is: `Fix login bug`

A good commit message will explain to a reader the changes that were made, but doesn't have to sound like a robot wrote it.

##### Completing tickets using commit messages
**AnyPresence** repositories are integrated with [Pivotal Tracker](https://pivotaltracker.com) using GitHub's post-recieve hooks. GitHub integration supports all of the same keywords syntax and functionality described above for [SCM Post-Commit Message Syntax](https://www.pivotaltracker.com/help/api?version=v3#scm_post_commit_message_syntax). The comments created by GitHub integration will also include the URL of the associated commit. 

For example, if Scotty uses the following message when committing:
```shell
[#12345677 #12345678] Tracking IP using Visual Basic GUI
```
...it will result in the following comment being added to Pivotal Tracker stories `12345677` and `12345678`, and the stories will be started if they were not yet started:
```shell
Commit: Scotty
54321

[#12345677 #12345678] Tracking IP using Visual Basic GUI
```

To automatically finish a story by using a commit message, include **fixed**, **completed** or **finished** in the square brackets in addition to the story ID. You may also use different cases or forms of these verbs, such as **Fix** or **FIXES**, and they may appear before or after the story ID. Note: For features, this will put the story in the `finished` state. For chores, it will put the story in the `accepted` state. For example:

```shell
[Fixes #12345678] Encryptions now sufficiently rerouted
```

