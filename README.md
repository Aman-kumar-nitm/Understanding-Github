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

now want to push something and then revert that changes