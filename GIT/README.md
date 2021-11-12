# GIT Commands

## Basic Commands

### git config
```
git config –global user.name “[name]”
git config –global user.email “[email address]”
```
### git diff
```
git diff
git diff -staged
git diff [first branch] [second branch]
```
### git reset
```
git reset --hard
git reset [file]
git reset --hard [commit]
```
### git stash
```
git stash save
git stash pop
git stash list
git stash drop
```
### git tag
```
git tag
git tag -l '1.3.1*'                   #search tags
git tag -a v1.4 -m "my version 1.4"

git show v1.4

git tag -a v1.5 9fceb02               #from a commit

git push origin v1.5
git push origin --tags

git tag -d v1.4
git push origin :refs/tags/v1.4
git push --delete origin <tagname>
```
### Get remote origin
`git config --get remote.origin.url`
`git remote show origin`

## Migrating a repository i.e. BitBucket to Github

### Bare Clone
`git clone --bare https://external-host.com/extuser/repo.git`

`cd repo.git`

### Push the mirror to the new GitHub repository
`git push --mirror https://github.com/ghuser/repo.git`

### Cleanup: Remove the temporary local repository
`rm -rf repo.git`
