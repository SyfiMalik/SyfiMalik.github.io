# How I maintain my personal dotfiles on github 

So here I'm gonna show you how I store my encrypted dotfiles on github. 

## Tools required:

> keybase, kbfs, gnupg2, git and some brain :P

## How to:

I'm using Arch linux so assuming you're running Arch, and you have knowledge about how gpg works. You must have a gpg keypair. Create an account on https://keybase.io and https://github.com if you haven't yet.


```
# pacman -S kbfs keybase         # install them   
$ systemctl start kbfs           # start them
$ systemctl start keybase
$ keybase login                  # login to keybase
$ keybase git create "myConfigs"  # Create repo
```

if you already have a git repo and you wanna use that, just go to the repo dir and rm -rf .git dir.


```
$ cd "old repo"        # Go to old repo dir
$ rm -rf .git          # delete the .git (old git data)
$ git init             # Start new git repo 
$ git add .            # Add all data in the repo
$ git remote add origin keybase://private/"your keybase username"/myConfig
$ git commit -a -m "first commit"
$ git push --set-upstream origin master
```

Well done. 
            You just created a encrypted repo. Let's integrate it with github now.

Go to https://github.com/ and create a new empty repo. After creating, just clone it to your computer.

```
$ cd
$ git clone "your Github username"@github.com:"your Github username"/"your new created repo"
$ cd "your new created github repo(the one you just cloned)"
```

Configure git to allow keybase protocol:

```
$ git config --global --add protocol.keybase.allow always
```

While running these commands in your newly cloned github empty repo, we will add our encrypted keybase repo as a submodule to it.

```
$ git submodule add keybase://private/"your keybase username"/myConfigs
$ git add .
$ git commit -m "added submodule myConfigs"
$ git push --set-upstream origin master
```

Done. You're now secured. Let's check it out.

Just delete the repo from computer, logout from keybase and clone the repo again. You'll see nothing.

## How to install these configs on new system?

Download required tools, gnupg, keybase, git. Login to keybase, you may have to approve this new device from other logged device if you have another device logged in. Do that and do the following.

```
$ keybase login 
$ git clone "your github unencrypted repository"
$ cd "new cloned repository"
$ git config --global --add protocol.keybase.allow always
$ git submodule update --init 

```

That's it. Now you will have all your configs unencrypted in your new system.



If you loved the tutorial and want my configs, just sign my key and leave me an encrypted mail/message.

https://keybase.io/encrypt#syfimalik

or using command line you can obtain my key 

```
$ gpg --recv-keys 49D806F7
$ gpg --sign-key 49D806F7
$ gpg --send-key 49D806F7
```
