# Git Stash

`git` is a powerful and complex CLI that manages versions of your code. This lesson explores using `git stash`.

## The Manual

It is helpful to utilize [`git` documentation](https://git-scm.com/doc) often as you grow as a developer. Sometimes it is even easier to launch `git` documentation in your shell session. Let's do this right now for `git stash`, using the `--help` option. You can pass the `--help` option to any `git` command for more information.

```
git stash --help
```

Take a few minutes to read about some of the ways one can pass additional options and configuration to `git stash`.

---

## Interruptions

It could be an emergency to open up a bugfix PR, or it may be time to meet with your team, or perhaps you are simply working on two different bodies of work at once. Regardless of the circumstance, there are many reasons why you may have to stop what you are working on to go work on something else. This is where `git stash` is useful. (When `git stash` if not followed by another command, it behaves as `git stash push`.)

## Stashing changes

For example, I am currently writing the `README.md` for this lesson. When I run `git status`, I get:

```bash
$ git status
On branch sample_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
  modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

But I have to stop. I have not yet added a `CODE_OF_CONDUCT.md` to this repository, and that is much more important. Since I am only half way through writing this section, I really do not want to make a new commit. In another scenario, I may even have broken code right now, and I really do not want to make a commit and lose reference to where I am.

So I will use `git stash` instead.

```bash
$ git stash
Saved working directory and index state WIP on sample_branch: 2a5860b Initial commit
```

Now `git status` returns no changed files. I am free to open up a new branch, add my `CODE_OF_CONDUCT.md`, and push it up into this repository.

Whew!!!!!!!

... so now what?

## Retrieving the stash

Let us start by checking what is in the stash:

```bash
$ git stash list
stash@{0}: WIP on sample_branch: 2a5860b Initial commit
```

`git stash list` will list all the changesets I have "stashed" in this repository. Since this was the first and only time, there is only one reference. But what is that commit SHA doing in there (since I didn't add a commit)?

That commit reference is the last commit that was created before I used the `git stash` command.

---

From here I have two main options on how to get my changes back.

1. `git stash pop` will take my changeset from the top of my stash and apply them. It will remove them from the stash when the command is run.
1. `git stash apply` will also take my changeset from the top of my stash and apply them. However, it will leave a copy of that changeset in the stash.

Most of the time we do not need to keep a copy of our changes in the stash. So I will use `git stash pop` and remove the changeset from the stash list and get them back into my working tree.

```bash
$ git stash pop
On branch sample_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
  modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (7894ab788f57539683f4d98e98932fb3762b59a4)
```

And I'm back in action.

## Resources

- [Useful tricks you might not know about git stash](https://www.freecodecamp.org/news/useful-tricks-you-might-not-know-about-git-stash-e8a9490f0a1a/)
