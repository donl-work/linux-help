Reset Last commit 

```
# remove last commit this will put all changes to stash

git reset --soft HEAD~1

#push branch

git push origin -f
```

Reset file

```
git checkout -- file/path

```

how-to-use-git-merge-squash

Note: this will create a new commit and merge with master and you wont see a mege

Say your bug fix branch is called bugfix and you want to merge it into master:

```
git checkout master
git merge --squash bugfix
git commit
```


Rebase

```
git checkout feature
## rebase develop to your branch
git rebase develop

... add stuff and commit git add . && git commit -m "f2 2"

git checkout develop
git rebase feature


```
