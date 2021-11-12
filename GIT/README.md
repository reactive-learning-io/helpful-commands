
# Migrating a repository i.e. BitBucket to Github

## Bare Clone
`git clone --bare https://external-host.com/extuser/repo.git`

`cd repo.git`

### Push the mirror to the new GitHub repository
`git push --mirror https://github.com/ghuser/repo.git`

### Cleanup: Remove the temporary local repository
`rm -rf repo.git`