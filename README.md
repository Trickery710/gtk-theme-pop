# gtk-theme-pop

*[![gtk-theme-pop](https://snapcraft.io/gtk-theme-pop/badge.svg)](https://snapcraft.io/gtk-theme-pop)
[![gtk-theme-pop](https://snapcraft.io/gtk-theme-pop/trending.svg?name=0)](https://snapcraft.io/gtk-theme-pop)*

Below you will find some instructions to help you contribute to this snap. The general workflow will be to submit PRs from your fork onto the "stable" branch. Once the pull request has been *submitted*, there is a GitHub action that will automatically launch a build of the snap that you can use for testing. And then once the PR has been *merged* the GitHub action will launch a build on launchpad that will be automatically uploaded to the snap store, in the candidate channel, for more extensive testing.

## How to contribute to this snap

### Initial setup
Here is the workflow for submitting a change to the stable branch, and getting it published in the snap store in the candidate channel. If this is your first time contributing to this snap, then there are a couple of things you need to do as a one-time setup to get ready to submit your first pull request:

1. [Fork the repository](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) into your own GitHub namespace.
2. [Clone your fork](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository).
3. In addition to your fork, you need to also add this remote repository. To make things a bit more intuitive, let's rename your fork's remote too (since "origin" is hardly descriptive):

```
git remote rename origin myfork
git remote add ubuntu https://github.com/ubuntu/gtk-theme-pop.git
git fetch --all
```

### Submitting changes in a pr

Once you're all setup for contributing, keep in mind that you want the git information to be all up-to-date. So if you haven't "fetched" all changes in a while, start with that:

```
git fetch --all -p
```

Now that your git metadata has been updated you are ready to create a bugfix branch, make your changes, and open a PR.

1. All pull requests should go to the stable branch so create your branch as a copy of the stable branch:

```
git checkout -b my-bugfix-branch ubuntu/stable
```

2. Make your desired changes and build a snap locally for testing:

```
snapcraft --use-lxd
```

3. After you are happy with your changes, commit them and push them to your fork:

```
git commit -a
git push myfork my-bugfix-branch
```

Once this branch has been pushed to your fork, you should update the local branch tracking so it tracks the branch pushed to your fork:

```
git branch -u myfork/my-bugfix-branch
```

4. When you feel they're ready for submitting to the main repository (stable branch), [open up a pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) from your `my-bugfix-branch` to the `ubuntu/stable` branch.
5. Once you've opened the pull request, it will automatically trigger the build-test action that will launch a build of the snap. You can watch the progress of the snap build from your pull request (Show all checks -> Details). Once the snap build has completed, you can find the built snap (to test with) under "Artifacts".
6. Someone from the team will review the open pull request and either merge it or start a discussion with you with additional changes or clarification needed.
7. Once the pull request has been merged into the stable branch, then on the next git mirror sync (every 4 hours), launchpad will trigger [a build of the snap that gets published](https://launchpad.net/~desktop-snappers/+snap/gtk-theme-pop) to the [snap store](https://snapcraft.io/gtk-theme-pop) into the *candidate* channel. After sufficient testing of the snap from the candidate channel, then the reviewer (a Collaborator of the snap in the store) will promote the snap to the stable branch in the snap store.
