---
layout: post
title: Git Tricks - Cleaning up your repo (git clean, git gc, git filter-branch)
tags: [git, tips]
date: 2013-05-06

section: Blog
---

# Git Tricks and Memory

## Memory or How I found the flash cards

In my travels around the internet, I ran across this stack of [web development flash cards](http://www.oxbridgenotes.co.uk/other/web_development_flashcards). The flash cards work with the [Anki](http://ankisrs.net/) flash card software.  Anki focuses on "__active recall testing and spaced repetition__."  After developing in PHP for 10+ years, I pretty much have most of the PHP API memorized. The same is not true for Ruby, so I am using [Jack Kinsella's](http://www.jackkinsella.ie/) stack of web development flash cards and the Anki program to bone up on my Ruby.  The card stack covers a batch of topics beyond Ruby, git being one of them.

The goal of this post is to firm up the lessons I have learned from studying the flash cards.

## Git Tricks for Removing files

Git is mostly thought of as something that you use to keep track of changes.  This post is focused on the git commands that you can use when you don't want git to remember something or need to change history.

### [git filter-branch](https://www.kernel.org/pub/software/scm/git/docs/git-filter-branch.html)

This is a feature I had never run across before.  It is able to walk through the history of a git branch and allow you to purge things from the history.  Why would you want to do this?   Isn't the history important?  Let's say you had accidentally included a bunch of log files in your repo.  The files are big and a waste of space and slow down every clone.  You can use `git filter-branch` to rewrite your branch to get those pesky log files out of git.

Filter out the contents of the log dir from the history of a branch:

<pre>
git filter-branch --tree-filter 'git rm --ignore-unmatch log/*.log' HEAD
</pre>

After filtering out the log files, it is a good idea to run `git gc --prune`.  You should read the section below about `git gc` before running the command.

### [git reset](https://www.kernel.org/pub/software/scm/git/docs/git-reset.html)

This command is powerful, but you can loose things so be careful.

If you want to move back in history and edit that last commit try:

<pre>
git reset --soft HEAD^
</pre>

This will take you back one commit and stage all the files for commit.

If you want to move back in history and discard all of your changes FOREVER.

<pre>
git reset --head HEAD^
</pre>

Wait, you want something back that you just deleted?  Check out the `git fsck` command below.

### [git clean](https://www.kernel.org/pub/software/scm/git/docs/git-clean.html)

To remove all the files that are not under version control use `git clean`.  This command is powerful, but very destructive because it is working on files that are not versioned by git.  I highly recommend the dry run `-n` option.  Why `-n` means dry run is beyond me.

Example workflow:

<pre>
git clean -n
# verify that you want to remove the files
git clean
</pre>

### [git fsck](https://www.kernel.org/pub/software/scm/git/docs/git-fsck.html)

fsck is an unix/linux command that stands for **F**ile **S**ystem **C**hec**K**.  The git version is designed to help you verify that your git database is in proper working order.  This command has lots of features, but the relevant command to this article is `git fsck --lost-found`.  This will "Write dangling objects into .git/lost-found/commit/ or .git/lost-found/other/, depending on type. If the object is a blob, the contents are written into the file, rather than its object name."

Dangling objects are those that have been disconnected from the git history tree.  Generally they get disconnected via actions like `git reset --hard`.  This will disconnect all the commits affected by the reset.  If you need one of those commits back you can use `git fsck --lost-found` to write the objects back to the disk, then cherry pick them back onto the git tree.

### [git gc](https://www.kernel.org/pub/software/scm/git/docs/git-gc.html)

I can't find what gc stands for, but I think it is **G**arbage **C**ollection.  This command cleans up your repo by packing and pruning your commits.  It has two phases: pack and prune.

**Pack** will compress the objects in the git tree.

**Prune** will remove dangling options.  Running prune will permanently delete the dangling commits.  It will mean you can't get them back with `git fsck`.

<pre>
git gc  #pack only
git gc --prune  #pack and prune
</pre>


## Conclusion

I hope the documentation of the less used commands is helpful.  Again, be careful because all of these commands can delete your work in some way.