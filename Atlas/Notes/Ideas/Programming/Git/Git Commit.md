---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---


## Git Commit
Since we have finished our work, we are ready move from `stage` to `commit` for our repo.
Git considers each `commit` change point or "save point"
When we `commit`, we should **always** include a **message**.
```shell
git commit -m "First message here"
```

## Git Commit without Stage
بعض الأحيان بتعمل تغييرات بسيطة مش بتحتاج انك تروح staging environment
The `-a` option will automatically stage every changed, already tracked file.

```shell
git commit -a -m "Updated index.html with a new line"
```

من غير ما أعمل add

**Warning:** Skipping the Staging Environment is not generally recommended.
Skipping the stage step can sometimes make you include unwanted changes.

## Git Commit Log
To view the history of commits for a repository, you can use the `log` command:
```shell
git log 
commit 09f4acd3f8836b7f6fc44ad9e012f82faf861803 (HEAD -> master) 
Author: w3schools-test 
Date: Fri Mar 26 09:35:54 2021 +0100 
	Updated index.html with a new line 
commit 221ec6e10aeedbfd02b85264087cd9adc18e4b26 
Author: w3schools-test 
Date: Fri Mar 26 09:13:07 2021 +0100 
	First release of Hello World!
```