---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---

## Working with Git Branches
a `branch` is a new/separate version of the main repository.
Branches allow you to work on different parts of a project without impacting the main branch.
When the work is complete, a branch can be merged with the main project.
You can even switch between branches and work on different projects without them interfering with each other.
Branching in Git is very lightweight and fast!
## New Git Branch
### new branch
Create new branch:
```shell
git branch hello-world
```
To confirm that I created a new branch
```shell
git branch
hello-world-images 
* master
```
but the working branch is master (the default one)
### Checkout
Moving us **from** the current `branch`, **to** the one specified at the end of the command
```shell
git checkout hello-world
Switched to branch 'hello-world-images'
```

**Note:** Using the `-b` option on `checkout` will create a new branch, and move to it, if it does not exist

### delete
To delete branch
```shell
git branch -d emergency-fix
```

## Emergency Branch

Now imagine that we are not yet done with hello-world-images, but we need to fix an error on master.
I don't want to mess with master directly, and I do not want to mess with hello-world-images, since it is not done yet.
So we create a new branch to deal with the emergency:
```shell
git checkout -b emergency-fix
Switched to a new branch 'emergency-fix'
```
Now, we need to know about [[Git Branch Merge]]