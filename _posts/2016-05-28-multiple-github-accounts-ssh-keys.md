---
layout: post
title:  "Multiple Github accounts & SSH keys"
date:   2016-05-28 15:57:45 -04:00
categories: Github, Git
---

You can't use the same SSH key for different GitHub accounts, but it's pretty easy to setup a different key for each one… This [Stack Overflow question][1] helped me figure most of it out, but not everything. So here's a recap.

## Create your keys

This [GitHub article][2] goes through the details on how to create a SSH key. You basically need to follow the instructions twice, just changing the email address and the file name where you want to save your key. For this example, let's say the other account is "other".

Once you've created both, you should have those files in `~/.ssh/`:

```
id_rsa
id_rsa.pub
id_rsa_other
id_rsa_other.pub
```

Then you need to go through the "Adding your SSH key to the ssh-agent" step in the Github article twice. Once for each key. To make sure it all went according to plan, you can run `ssh-add -l` to see a list of the added keys.

## SSH config file

Create a file called `config` in your `~/.ssh/` directory and add this to it:

```
# default account
Host github.com
    HostName github.com
    User git
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

# other account
Host other.github.com
    HostName github.com
    User git
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_other
```

## Git config file

Make sure you setup your repo config file to include the correct user info and the URL you setup in SSH config `Host`, so for a repo on the "other" account, it should look something like that:

```
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[user]
    name = other
    email = other@account.com
[remote "origin"]
    url = git@other.github.com:other/repo.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

Once that's done, you should be able to push to both accounts without any issues.

[1]:http://stackoverflow.com/questions/3225862/multiple-github-accounts-ssh-config
[2]:https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/
