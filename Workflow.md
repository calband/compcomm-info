# Comp-Comm Workflow

Regardless of the project you're working on, we will always have generally the same workflow with how we make changes to the project. The workflow for contributing to a project is as follows:

1. **Assign** yourself to an issue.
1. **Branch** off from `master`
1. **Commit** changes and **push** to Github
1. Create a **pull request** and make changes according to comments

## Assigning Issues

The issues page on Github lists all of the things that need to get done for a given project. When you contribute to a project, you'll generally be fixing one of these issues (if not, either make an issue or skip this section). In order to claim the issue and make sure no one else works on it, [assign](https://help.github.com/articles/assigning-issues-and-pull-requests-to-other-github-users/) yourself to the issue.

## Branch

In order to maintain the `master` branch as a working and complete implementation, branch off to a new branch to make changes and commit freely without worrying about breaking the master code. The new branch name should be of the format `yourname__your_branch_name` or something similar. That is, your name (first or last, whichever uniquely defines you) followed by two underscores, then your branch name (underscore separated, hyphen separated, or camel case are all fine).

Before making a new branch, first check out `master` and pull from Github to make sure you're editing from an up to date version of the code.

```
git checkout master
git pull origin master
```

Then, to make a new branch and navigate to it, you can either use

```
git branch <branch name>
git checkout <branch name>
```

or combine the two steps with

```
git checkout -b <branch name>
```

## Making Changes and Pushing

After creating and checking out your new branch, you can now make changes. Work on your feature and test it locally. Commit often in case you wish to revert back to an old change and to clearly log your steps for other developers. After you make your changes, use `git push origin <branch name>` to push your changes to Github.

## Pull Request

After you feel like your changes are ready to be merged into the code, make a [pull request](https://help.github.com/articles/using-pull-requests/) on the Github repository. In the description, include the issue being resolved ("Fixing #312") and any additional information about the pull request you'd like to mention. Generally, one pull request should fix one issue, but there are exceptions for fixing related issues or small issues.

Then someone (usually the Computer Coordinator) will review your code, making comments on your changes if need be. Then, once everything looks good, the pull request is ready to be merged! **Only** the Computer Coordinator should actually merge the pull request, unless they specifically say you or someone else can merge the pull request.

### Merge Conflicts

Sometimes, while you've made changes on your branch, someone else's branch has been merged to `master`, and they edited the same files you did. The pull request you've made will not allow you to merge, instead notifying you there's a merge conflict with the `master` branch. What you'll have to do is checkout the `master` branch, pull to get the latest copy, then merge and resolve conflicts with your branch.

```
git checkout master
git pull origin master
git checkout <your branch>
git merge master # merge conflicts
<resolve conflicts>
<commit and push>
```

## Conclusion

After your changes have been merged to `master`, then you can go back to the issues page and start over! If you're feeling ambitious, you can make multiple branches and create multiple pull requests at once, but try to limit your pull requests to 3 at a time, to prevent excessive pull request reviewing.
