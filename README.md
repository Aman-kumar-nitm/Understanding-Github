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