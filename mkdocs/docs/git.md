### *Git commands*
- When want to change the commit, use `amend` command.  
`git status`    
`git add .`   
`git commit --amend -m "Your comment"`  
`git push origin HEAD -f` 

- When want to squach last N commits, use **squash** command.  
`git rebase -i HEAD~N`    
Choose the commits that you want to squach, and put squash command at the beginning of the commits. For example, the last 4 commits below will be squashed into first commit **01d1124**.

    ```
    pick/reword   01d1124 commit 1.    
    fixme 6340aaa commit 2.
    fixme ebfd367 commit 3.
    fixme 30e0ccb commit 4.
    ``` 
  
    Once this is done and saved, another editor pops up, you can also edit the commit message there if you want to.   
Save and exit, use the following command to push the squached commit.  
`git push origin HEAD -f` 
 


- Jump back to the last commit using a `commit-id` and push it to the remote branch.   
`git reset --hard f145f6f`  
`git push origin -f` 


- Undo the last commit  
`git reset --soft HEAD~1`  
If you don't want to keep these changes, simply use the `--hard `flag. Be sure to only do this when you're sure you don't need these changes anymore.  
`git reset --hard HEAD~1`


- Remove the merge just now  
`git fetch origin`  
`git reset --hard origin`


- git reverte  
`git checkout master`  
`git pull --rebase origin master`
`git checkout -b revert_pull_request_1`
`git revert -m 1 merged-commit-id`
`git push origin revert_pull_request_1`
 
 
- Create branch   
`git pull`  
`git checkout -branch branchName`  
`git push origin branchName`  


- Delete branch from local and remote   
`git branch -delete branchName`  
`git push origin --delete branchName`


- Resolve Conflicts  
**Step 1**. Checkout the source branch and merge in the changes from the target branch.  
`git merge --abort`  (If exist uncommited files)   
`git checkout feature/branchName`   
`git pull origin master`  
**Step 2**. After the merge conflicts are resolved, stage the changes accordingly, commit the changes and push.  
`git commit`  
`git push origin HEAD`   


- Rename remote branch  
**Step 1a**. Rename your local branch.
If you are on the branch you want to rename:
`git branch -m new-name`  
**Step 1b**. If you are on a different branch:
`git branch -m old-name new-name`    
**Step 2**. Delete the old-name remote branch and push the new-name local branch.
`git push origin :old-name new-name`  
**Step 3**. Reset the upstream branch for the new-name local branch.
`git push origin -u new-name`


- Remove the last commit  
`git reset --hard HEAD^`  
`git push origin -f`  


- Output logs
    - Output every log in one line  
    `git log --oneline`
    - Search by keywords  
    `git log --grep keywords`

---
### **Git short command** 
- Show commit history   
`git reflog`

- Show graphical history viewer   
`gitk`


---
