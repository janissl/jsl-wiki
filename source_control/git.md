git commands
============

### Check URI of a remote repository

```shell
git remote get-url --all origin
```

### Update URI of a remote repository

```shell
git remote set-url origin <new.git.url>
```

### Rename a branch

```shell
git checkout <old_name>
git branch -m <new_name>
git push origin -u <new_name>
git push origin --delete <old_name>
```

### Revert merge commit
```shell

git checkout <destination_branch>
git cat-file -p <merge_commit_hash>
git revert -m {1,2} <merge_commit_hash>

# Example:
# You merged feature_branch into main_branch, however, you later decided to put feature_branch out of main_branch for some reason.
# Your merge commit have the following hash: 5e6af5c.
#
# You have the following output from the 'git cat-file' command:
# 
# tree 4f2dec72fad21af8c6399e5ef173791635fedfe7
# parent 7e361681c46e93854cd3d752e551f6a281eea828
# parent c49b012481061ef65ef2826b25a9c2a8cdacb12a
#
# You want to detach c49b012 (the last commit in feature_branch as parent 2) from 5e6af5c 
# and keep 7e36168 (parent 1) before 5e6af5c in the main_branch.
# Then your commands will be as follows:

git checkout master_branch
git cat-file -p 5e6af5c
git revert -m 1 5e6af5c
```

### Resolve conflict of feature branch with main branch before merge

```shell
git checkout feature_branch
git pull origin main_branch

# Correct the code and save the file(s).

git add <filename>
git commit [-m '<message>']
git push origin feature_branch
```

### Restore missing files and folders
```shell
# NOTE: this will also restore modified files!

git checkout .
```

### Restore a local branch

Remove uncommited changes:
```shell
git reset --hard
```

Return to a particular commit:
```shell
git reset --hard <commit_hash>
```

From a local backup:
```shell
git reset --hard <branch_backup>
```

From a remote branch:
```shell
git fetch origin
git reset --hard origin/<branch_name> 
```
