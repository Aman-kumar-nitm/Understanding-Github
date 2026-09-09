# Understanding-Github
#### git push origin main => push my local main to remote main
#### git push origin feature/login => push my local feature/login to remote feature/login
### git push <remote> <local-branch>:<remote-branch>
#### git push origin main:feature/login
#### git pull origin main

##### Hi checking git diff
##### You cannot git checkout feature/login before staging all of your changes no changes added to commit (use "git add" and/or "git commit -a")


##### Understanding git diff => What have I changed in my working tree that I have NOT staged yet (compare stage with current working dir) 
##### git diff --staged  => What have I staged that is different from my last commit (compare stage with last commit)


## Understanding git merge <branch-name> and git cherry-pick <commit-C>
##### In local we have two branch main and feature/login => Currently both are at same step => git checkout feature/login => Do some changes => Stage it and commit it Dont Push => Now git checkout main => as expected it wont have those changes and even remote repo does not have it => to bring it in main two option 1. Push those changes from /feature/login to remote repo then pull it in main 2. git merge feature/login 
##### Lets say feature/login locally has two commit c and d and inside main we want only upto c not d => git cherry-pick <commit-C>


###### This one is just to See Cherry pick as another commit this e3e199ff4ad4c1052fed32f2596c4ca6e29f5573 and this 0f8d0e1d14bd1f20653e1ce5b5fdab1019cff922 is commit id used while cherry pick git cherry pick e3e199ff4ad4c1052fed32f2596c4ca6e29f5573


#### git log helps to see commits and git show <commit-id> helps to see changes 
#### git blame somefile.js helps to see who made changes in that file then we can use git show <commit-id> to investigate more

## Undoing Things
### git restore 
#### git restore <file-name> this will turn the file into staged state
#### git restore --staged <file-name> this will bring back file from staged to unchanged 

### git reset
#### Changed something committed locally now don't want that commit in history and want to move back to prev commit like current a->b->c we want to delete c completely and roll back to b 
#### git reset git reset --hard HEAD~1 => this command can destroy uncommitted work

### git revert
#### lets say change something push it to remote(main) now a->b->c where c is changed push to remote(main) => we want that this commit is not right but as we pushed we cannot remove it so we can prepare a new commit by reversing all the changes made in c means we are going back to b (same content) and want to push this again as new commit R
#### git revert b3eb4a7d1e32ec43953a14159b529fbad37a393e and then git push origin feature/login:main it will be like a->b->c->r and r will be as same as b

### Creating Branch
##### git branch <branch-name>
##### git switch <branch-name>
##### git switch -c feature/login
##### git checkout <branch-name>  it does two thing switch the branch along with restore files as git restore (take staged back into changed and changed to last staged/committed)


## Git merge
##### Fast Forward Merge => No new merge commit is required. Main is there a->b->c and feature/login has few changes on top of it a->b->c->d->e so inside main we can do git merge feature/login and it will be a->b->c->d->e and both main and feature/login will be pointing here

##### Diverged Branches Merge 
a->b->c
        /   \
        d   e
        f   g
    Now when we merge it will create one new commit 
    f g
    \ /
     h
     

#### git merge --abort while resolving commit before committing it will turn into going previous commit
#### Lets say merge has happened If it hasn't been pushed and you're comfortable rewriting your local history: git reset --hard HEAD~1 => will move your head to last commit top of which merging started
#### If the merge was already pushed/shared git revert -m 1 <merge-commit-id>  => it says create a commit that undoes the changes brought into main by this merge.
##### what done is 
##### 1. create one backup1 branch then write some thing and commit similarly create backup2 branch write something and commit 
##### 3. in backup1 git merge backup2 create one merge conflict try to solve in editor don't commit => if run git merge --abort will throw you back to code as backup1 had
##### 4. if committed and ran git reset --hard HEAD~1 inside backup1 will throw you back to last commit of backup1 backup2 wont know this is merged
##### 5. if merged and committed and pushed then inside backup1 git revert -m 1 <merge-commit-id> will result into creation of one new commit with content as last commit before merging backup1 



## Understanding Remote
##### So what happen there is one remote main and one local main and our .git (locally) keep one remote main as named origin/main which stores status of our remote main seen last time. sometime our github main gets committed so many times by other developer and we don't know even our local .git does not know to let .git know what is state on remote main we run <git fetch origin> fetch says: "Go to the remote and tell me what changed. Download the new Git data, but don't modify my current branch." 

### Example what i did i edited readme from github so that our local wont know that remote main has some commits then 
D:\Github_Understanding>git switch main
Switched to branch 'main'
Your branch is behind 'origin/main' by 3 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)

D:\Github_Understanding>git fetch origin     
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.25 KiB | 63.00 KiB/s, done.
From https://github.com/Aman-kumar-nitm/Understanding-Github
   06fec92..c8986f6  main       -> origin/main

D:\Github_Understanding>git status
On branch main
Your branch is behind 'origin/main' by 4 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean

D:\Github_Understanding>

#### See Here first local remote main only knew 3 commits our local main is behind but then git fetch origin told no there is one more commit that is staying on remote main 