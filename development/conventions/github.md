# Pushing Code to Github

## Introduction

Scenario: You fixed the damn bug and make some sweet changes to the code that basically allows user to do awesome things! 

That's great! We should always celebrate the mini victories whenever possible. Dance like no one is watching (while you push the code to Github and wait for Travis CI to run the tests...)!

But how does the other team members know what exactly what was your new pull request about? Perhaps even before reading the description on your PR?

## 1. Determine the type of PR

One of the way Benri adopt in making pull requests is first to determine what kind of code change are we making in this PR.

Is it a : 

- Feature *def: yea! you're the man*
- Chore *def: does not explicitly add value nor impact end users but is necessary*
- Bug *def: okay, one bug down*

## 2. Set Meaningful Branch Name

After settling on the type of PR, let's try to keep the branch name meaningful and indicative of what code changes lay inside.

For instance, we found a bug in Snakebite where emails are not validated. Lets go ahead and fix this, whilst creating a new branch to work on.

```
$ git checkout master
$ git pull origin master

....

$ git checkout -b fix-validate-emails

Switched to a new branch 'fix-validate-emails'

... make some commits ...
... push ...

```

By going with the convention: `[type of PR]-[short-description]`, we can have a systematic bird-eye's view on the PRs we have in each repository :)


## 3. Add labels to the PR

This next step would be recommended, as it basically tells the review what prioroty level this PR is.

Take a look at the available labels on the SnakeBite or Adam repositories, and you should see `P 0`, `P 1` and `P 2` labels. They basically mean:

- P 0: top priority: we should get this fixed or delivered to users ASAP
- P 1: critical priority: this is rather important; we should try to get this added in within the next 5 working days
- P 2: nothing critical but it should be pushed or merged into the main code, within 2 weeks or so.

## Conclusion

With this, let's try to keep things tidy on Github.
Happy coding!
