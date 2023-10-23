## Setting Up Multiple GitHub Identities on the Same Computer

So you want to use the same computer to commit to repos in different accounts. But you can't, because if you try to add your public key to the second GitHub account, it says it's already in use.

1. Create a new identity file with `ssh-keygen` and name it something other than `id_rsa`
  - Here, we'll call the file `new_rsa` 
2. Change your `~/.ssh/config` file
```
Host new-git-host
  HostName github.com  # Or other organisation
  User git
  IdentityFile ~/.ssh/new_rsa
  IdentitiesOnly yes
```
3. Register identity (seems to be a Mac-only requirement?)
```
ssh-add ~/.ssh/new_rsa
```
4. Add token to github
5. [MAY BE UNNECESSARY but was suggested [here](https://stackoverflow.com/questions/7927750/specify-an-ssh-key-for-git-push-for-a-given-domain)] Add your identity to github
```
git remote add your-name-here git@new-git-host:repo-owner/repo-name.git
```
  - If you can't commit here:
      1. rename your `id_rsa` and `id_rsa.pub` files temporarily to something else
      2. rename your `new_rsa` and `new_rsa.pub` to `id_rsa` and `id_rsa.pub` respectively
      3. commit
      4. undo all renaming changes
5. Commit to the repo
