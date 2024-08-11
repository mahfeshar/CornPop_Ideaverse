---
up:
  - "[[Git - GitHub MOC]]"
related: 
created: 2024-06-27
---

## Merge Branches
First, you should go to master branch
```shell
git checkout master
```
Now we merge 
```shell
git merge emergency-fix
```
لو محصلش تغيير في ال master واحنا شغالين على التاني فهو هيعتبر ان دا تكملة ليه فيهجمعهم مع بعض وخلاص من غير أي مشاكل
## Merge Conflict
انما لو غيرت في ال branch الأصلي دا هيعملي conflict ويقولك مينفعش
```shell
git checkout master
git merge hello-world
Auto-merging index.html CONFLICT (content): 
Merge conflict in index.html 
Automatic merge failed; fix conflicts and then commit the result.
```
وعشان نعرف المشكلة فين تعالا نعمل status
```shell
git status
On branch master 
You have unmerged paths. 
	(fix conflicts and run "git commit") 
	(use "git merge --abort" to abort the merge) 

Changes to be committed: 
	new file: img_hello_git.jpg 
	new file: img_hello_world.jpg 

Unmerged paths: 
	(use "git add ..." to mark resolution) both modified: index.html
```

هيقولك ال conflict في فايل ايه بالظبط عشان كدا لازم تفتح الفايل دا يدوي وتحل ال conflict دا وبعد ما تحله وتجرب تاني
```shell
git add index.html
git status
All conflicts fixed but you are still merging.
```

تقدر دلوقتي تعمل commit وبعدها تمسح ال branch التاني عادي