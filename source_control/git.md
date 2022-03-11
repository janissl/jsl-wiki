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
got push origin --delete <old_name>
```
